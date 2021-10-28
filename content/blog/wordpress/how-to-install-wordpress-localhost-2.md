---
title: "How to Install Wordpress On Localhost"
date: 2021-10-27T23:41:09+06:00
featureImage: images/blog/tutorials/wordpress/install-localhost/feature-small.png
postImage: images/blog/tutorials/wordpress/install-localhost/feature-large.png
---
In this tutorial, we shall discuss how you can install Wordpress in your local server. In this post, I assume that you already have a local server set up using XAMPP or Devilbox. [Click here](https://blog.markcite.com/blog/mysql/xampp-alternative-in-mac-for-mysql/) if you want to see how to set up Devilbox in your mac.

### Download the Wordpress latest version
First you need to download the latest version of Wordpress. Go the [this link](https://wordpress.org/download/) to download the latest ZIP folder.

### Create database
Go to your PhpMyAdmin and create a new database.

### Installation
- Copy and extract the downloaded ZIP file in the `htdocs` folder of your localhost.
- Go to the folder location in browser. For example in my case, `http://localhost/wptest/`.
- Click the `Let's Go` button.
- Give the database name that you have just created in PhpMyAdmin.
- Username is usually `root`.
- Password is usually blank.
- Database host is usually `localhost`.
- Keep the table prefix as it is and click `Submit`.
- You may see a warning saying `Unable to write to wp-config.php file.`. To solve this, create a file named `wp-config.php` in the root folder of your Wordpress installation and paste the given code and save it. Then click `Install`.
- In the next page give the **Site Title**, **Username**, **Password** and other necessary things. Then click, `Install WordPress` and you will see a success message and a page to log in.

**Congratulations** you have successfully installed WordPress in you localhost.

#### Troubleshoots
**Unable to connect to the filesystem. Please confirm your credentials**
This may occur if your Mac denies permission to the folder where you have kept the Wordpress files.
Go to `htdocs` and right click on the wordpress folder where you are attempting to install a plug-in or theme. Click `Get info`, scroll to the bottom, click on the `lock`, type in your password, and press enter. Click on the `Action` button at the bottom, select `Apply to enclosed items...` and then select `Okay`.