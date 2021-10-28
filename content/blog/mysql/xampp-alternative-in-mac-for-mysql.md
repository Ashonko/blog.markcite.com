---
title: "Xampp Alternative in Mac for Mysql: Devilbox"
date: 2021-10-24T18:53:47+06:00
featureImage: images/blog/tutorials/mysql/devilbox/feature-small.png
postImage: images/blog/tutorials/mysql/devilbox/feature-large.png
---
For a very long time, I have been using [XAMPP](https://www.apachefriends.org/) as my local environment to create applications. XAMPP uses MariaDB which is almost similar to MySQL but here is the catch, **almost**. It came to my notice when I started to work with JSON. MariaDB had announced that it would provide the support for JSON in their [official blog](https://mariadb.com/resources/blog/json-with-mariadb-10-2/) back in 2019. But as off 2021, still they haven't added the JSON support completely, instead try to go through the route by converting JSON column into **longtext** which doesn't deliver the full capability of JSON.
I have been looking for a solution to use MySQL in XAMPP but as I have found that, it is not difficult to do in Windows machines, but haven't found any resource to make it work in Mac. Then I installed the [MAMP for Mac](https://www.mamp.info/en/mac/) and again, found that it uses the MySQL, but an older version 5.7 which had limited query support for JSON. Additionally, I didnlt find any way to update the MySQL in MAMP. So I had to abandon it again.

### [Devilbox](http://devilbox.org/)
I came across **Devilbox** and wanted to give it a try. It's most promising feature that I love is that I am in control of creating my own development environment based on the tools and versions in my live server. But the problem was that, there are very few resources on the internet to make it run. Long story short, I have finally did it. In the nest section, I shall describe step by step how you can work with Devilbox too.

### Installing Devilbox in Mac
- The very fast thing you should do is that you download and install [Docker Desktop](https://www.docker.com/products/docker-desktop) in your machine. It will save a lot of time later on.
- After you have installed Docker, it's time to install the Devilbox now. Open your Terminal and go to your desired directory where you want to install Devilbox. Then run the following command. It shall clone it to your local directory form github.
{{< highlight shell >}}
git clone https://github.com/cytopia/devilbox
{{< / highlight >}}
- You need to create an `.env` file from the terminal with the following command.
command. It shall clone it to your local directory form github.
{{< highlight shell >}}
cp env-example .env
{{< / highlight >}}
- Now open the Devilbox folder with VS Code and there you will find the `.env` file. You need to do some modifications in it.
  - First, uncomment the database and php versions that you do not need and remove the `#` from the versions that you want.
  - Go back to the terminal and type `id -u`. Note down the returned user id.
  - Then type `id -g`. Note down the returned group id.
  - Now go back to the `.env` file and change the values of the following with your values:
{{< highlight env >}}
NEW_UID=1001
NEW_GID=1002
{{< / highlight >}}
- Now to download all the programmes that you have selected, run the following command in the terminal. It may take some time and depending on the number of documents it pulls.
{{< highlight shell >}}
docker-compose up
{{< / highlight >}}
- Once done, go back to your Docker Desktop application and you'll find that devilbox is running. From the next time, you may start and stop devilbox from docker. You won't need to go back to terminal. However, to run specific containers, you may run from the terminal the following command
{{< highlight env >}}
docker-compose up httpd php mysql
{{< / highlight >}}

Good job. You have finished installing. Now go to [http://localhost](http://localhost) or [http://127.0.0.1](http://127.0.0.1) and you'll find that Devilbox is up and running.

### Creating your app AKA "Virtual Host" for Devilbox
To create an app, you need to follow this instruction.
- Go to the folder where you have installed Devilbox and create a folder named `www` inside. 
- In the `www` folder, create another folder that would be your first project. For example `project-1`.
- Inside that folder, create another folder named `htdocs`.
- Now go to your [http://localhost](http://localhost) and in the **Virtual Hosts** menu, see your `project-1` probably showing an error that `No Host DNS record found.` And is saying to add a record. To do that,
  - Go to terminal and write:
{{< highlight env >}}
sudo vi /etc/hosts
{{< / highlight >}}
  - It will open the DNS entry in VIM editor. To edit the entry, type `:a` and hit **return***. Then paste the showed entry in the **Virtual Hosts** menu, for example, `127.0.0.1 project-1.loc`.
  - Then press **esc** button and to save and get out of the VIM editor, type `:x` and hit **return**.
- Now, refresh the **Virtual Hosts** page and you'll find that your project is running. Keep your app files in the `project-1>htdocs` folder and you are good to go.
- To visit your web app `project-1`, go to [http://project-1.loc](http://project-1.loc) and you'll be able to see your `project-1` web-app.

### Connecting to MySQL database
To connect to MySQL database, try the following. Note that the `DB_SERVER` name is not `localhost`, it should be `127.0.0.1`:
{{< highlight php "linenos=table,linenostart=1" >}}
define('DB_SERVER', '127.0.0.1');
define('DB_USERNAME', 'root');
define('DB_PASSWORD', '');
define('DB_NAME', 'dbname');

$mysqli = new mysqli(DB_SERVER, DB_USERNAME, DB_PASSWORD, DB_NAME);
{{< / highlight >}}

The process is not very complicated but once all the set-ups are done, you'll be able to have the full potential of Devilbox.

### Start Devilbox from Terminal
To start devilbox from the terminal, use the following command:
{{< highlight env >}}
docker-compose up -d httpd php mysql
{{< / highlight >}}

#### More resources:
- [Official documentation on installing Devilbox](https://devilbox.readthedocs.io/en/latest/getting-started/install-the-devilbox.html)
- [Guideline to change a version](https://devilbox.readthedocs.io/en/latest/getting-started/change-container-versions.html)