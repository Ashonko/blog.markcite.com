---
title: "How to load local HTML file in Flutter WebView"
date: 2020-05-18T21:01:34+06:00
featureImage: images/blog/tutorials/flutter/how-to-load-local-html-file-in-flutter-webview/small.jpg
postImage: images/blog/tutorials/flutter/how-to-load-local-html-file-in-flutter-webview/feature.jpg
---

### Background!
My wife joined the internship program in a Medical College Hospital yesterday. This morning she showed me a PDF file of a hand note for the treatment protocols in Obstetric Department. She said to me that do you have any better version of that?

Well, during my internship program, I wrote some treatment protocols in a word file. So I thought why not make an HTML app from these word files and pack them into a WebView of a Flutter project to make an Android app for my wife. But to my surprise, I found that working with local HTML files in Flutter WebView is really painful. There are lots of packages for displaying web pages in Flutter but very few of them works with local files to show them offline. Some of them don’t even load local file and others load only one file but doesn’t load any other asset. So, it just becomes a plain page with no practical interactions. After searching for a few hours I even thought that I shall make this app in Java that I already knew and had worked with different WebView dependencies before. But my heart was saying, “Keep trying your loving Dart. It’ll not miss in the 9th time.”

Here in this post, I’ll describe how I solved this problem and how you can also local your local HTML app in Flutter WebView.

### Requirements!
- **[Flutter InAppWebView Plugin](https://pub.dev/packages/flutter_inappwebview)**. (Among all the plugins that I have tried, it is the best for showing your local HTML app.)
- **Dart SDK**: “>=2.7.0 <3.0.0”
- **Flutter**: “>=1.12.13+hotfix.5”
- **Android minSdkVersion**: 17 
- Your **HTML app**

Update your Dart SDK and Flutter if you are using old versions. It’s important as it will not allow work with the InAppWebView Plugin. Run ```flutter doctor -v``` in the terminal to see the version of your Dart SDK and Flutter and update if necessary.

### Set Up!
After you have created a new flutter project, you need to set up your ```pubspec.yaml``` file and put your HTML app in the asset directory.

**Copy the HTML app**: Create an ```assets``` directory in the root folder and paste your entire HTML app inside that folder.

**Setting up ```pubspec.yaml``` file**: Add ```flutter_inappwebview``` plugin in the dependencies.
{{< highlight go "linenos=table,linenostart=1" >}}
dependencies:
  flutter:
    sdk: flutter
  flutter_inappwebview:
{{< / highlight >}}

Then declare all the folders and ```index.html``` file directory as asset in ```pubspec.yaml```. Like my project, I had a **css** folder, a **js** folder and a folder named conditions. Remember that you must mention all the folders here.
{{< highlight go "linenos=table,linenostart=1" >}}
assets:
    - assets/index.html
    - assets/css/
    - assets/images/
    - assets/js/
    - assets/conditions/
{{< / highlight >}}

### The Code!
What you will do basically is you’ll create a local server inside the app and it’ll run the HTML app there in the WebView. Let’s look at the ```main.dart``` file and its entire code:
{{< highlight go "linenos=table,linenostart=1" >}}
import 'package:flutter/material.dart';
import 'package:flutter_inappwebview/flutter_inappwebview.dart';

InAppLocalhostServer localhostServer = new InAppLocalhostServer();

Future main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await localhostServer.start();
  runApp(new MyApp());
}

class MyApp extends StatelessWidget {
  @override
  Widget build(BuildContext context) {
    return MaterialApp(
      debugShowCheckedModeBanner: false,
      title: 'Hi! There!!',
      theme: ThemeData(
        primarySwatch: Colors.blue,
      ),
      home: MyHomePage(),
    );
  }
}

class MyHomePage extends StatefulWidget {
  @override
  _MyHomePageState createState() => _MyHomePageState();
}

class _MyHomePageState extends State < MyHomePage > {
  InAppWebViewController webView;

  @override
  Widget build(BuildContext context) {
    return WillPopScope(
      onWillPop: () async {
        if (await webView.canGoBack()) {
          webView.goBack();
          return false;
        }
        return true;
      },
      child: Scaffold(
        body: Container(
          child: Column(children: < Widget > [
            Expanded(
              child: Container(
                margin: const EdgeInsets.only(top: 30.0),
                  child: InAppWebView(
                    initialUrl: "http://localhost:8080/assets/index.html",
                    onWebViewCreated: (InAppWebViewController controller) {
                      webView = controller;
                    },
                  ),
              ),
            )
          ])
        ),
      ),
    );
  }

  @override
  void dispose() {
    localhostServer.close();
    super.dispose();
  }
}
{{< / highlight >}}

### Let's break it down (a bit):
In the main section, we shall first start the server and will also command to close the server when the function ends.
{{< highlight go "linenos=table,linenostart=4" >}}
InAppLocalhostServer localhostServer = new InAppLocalhostServer();

Future main() async {
  WidgetsFlutterBinding.ensureInitialized();
  await localhostServer.start();
  runApp(new MyApp());
}

//... ...

class _MyHomePageState extends State < MyHomePage > {

//... ...

  @override
  void dispose() {
    localhostServer.close();
    super.dispose();
  }
}
{{< / highlight >}}

Then, let’s create the ```WebView``` in the ```body```:
{{< highlight go "linenos=table,linenostart=50" >}}
InAppWebView(
  initialUrl: "http://localhost:8080/assets/index.html",
  onWebViewCreated: (InAppWebViewController controller) {
    webView = controller;
  },
),
{{< / highlight >}}
You can see that our initial URL starts with a ```localhost``` address, that means we are using local server and then we have pointed it to our root file of our HTML app.

You may have noticed that we have wrapped our build in a ```WillPopScope``` widget. It’s because, inside it, we have looked at the history and see whether the web page can go back. It can, it’ll go back when we press the back button and if not, it’ll simply exit the app.
{{< highlight go "linenos=table,linenostart=36" >}}
WillPopScope(
      onWillPop: () async {
        if (await webView.canGoBack()) {
          webView.goBack();
          return false;
        }
        return true;
      },
      //... ...
    );
{{< / highlight >}}
So, there you have it. Now you know how you can load your HTML app easily in your Flutter project.