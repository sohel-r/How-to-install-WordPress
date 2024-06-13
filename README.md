How to install WordPress
WordPress is well-known for its ease of installation. Under most circumstances, installing WordPress is a very simple process and takes less than five minutes to complete. Many web hosts now offer tools (e.g. Fantastico) to automatically install WordPress for you. However, if you wish to install WordPress yourself, the following guide will help.
Things to Know Before Installing WordPress
Before you begin the install, there are a few things you need to have and do. Refer the article Before You Install.
If you need multiple WordPress instances, refer Installing Multiple WordPress Instances.
Basic Instructions
Here’s the quick version of the instructions for those who are already comfortable with performing such installations. More detailed instructions follow.
1.	Download and unzip the WordPress package if you haven’t already.
2.	Create a database for WordPress on your web server, as well as a MySQL (or MariaDB) user who has all privileges for accessing and modifying it.
3.	(Optional) Find and rename wp-config-sample.php to wp-config.php, then edit the file (see Editing wp-config.php) and add your database information.
Note: If you are not comfortable with renaming files, step 3 is optional and you can skip it as the install program will create the wp-config.php file for you.
4.	Upload the WordPress files to the desired location on your web server:
o	If you want to integrate WordPress into the root of your domain (e.g. https://example.com/), move or upload all contents of the unzipped WordPress directory (excluding the WordPress directory itself) into the root directory of your web server.
o	If you want to have your WordPress installation in its own subdirectory on your website (e.g. https://example.com/blog/), create the blog directory on your server and upload the contents of the unzipped WordPress package to the directory via FTP.
o	Note: If your FTP client has an option to convert file names to lower case, make sure it’s disabled.
5.	Run the WordPress installation script by accessing the URL in a web browser. This should be the URL where you uploaded the WordPress files.
– If you installed WordPress in the root directory, you should visit: https://example.com/
– If you installed WordPress in its own subdirectory called blog, for example, you should visit: https://example.com/blog/
That’s it! WordPress should now be installed.
Detailed instructions
Step 1: Download and Extract
Download and unzip the WordPress package from wordpress.org/download/.
•	If you will be uploading WordPress to a remote web server, download the WordPress package to your computer with a web browser and unzip the package.
•	If you will be using FTP, skip to the next step – uploading files is covered later.
•	If you have shell access to your web server, and are comfortable using console-based tools, you may wish to download WordPress directly to your web server using wget (or lynx or another console-based web browser) if you want to avoid FTPing:
o	wget https://wordpress.org/latest.tar.gz
o	Then extract the package using:
o	tar -xzvf latest.tar.gz
The WordPress package will extract into a folder called wordpress in the same directory that you downloaded latest.tar.gz.
Step 2: Download and Extract
If you are using a hosting provider, you may already have a WordPress database set up for you, or there may be an automated setup solution to do so. Check your hosting provider’s support pages or your control panel for clues about whether or not you’ll need to create one manually.
If you determine that you’ll need to create one manually, follow the instructions for Using phpMyAdmin below to create your WordPress username and database. For other tools such as Plesk, cPanel and Using the MySQL Client, refer the article Creating Database for WordPress.
If you have only one database and it is already in use, you can install WordPress in it – just make sure to have a distinctive prefix for your tables to avoid over-writing any existing database tables.
Using phpMyAdmin
If your web server has phpMyAdmin installed, you may follow these instructions to create your WordPress username and database. If you work on your own computer, on most Linux distributions you can install PhpMyAdmin automatically.
Note: These instructions are written for phpMyAdmin 4.4; the phpMyAdmin user interface can vary slightly between versions.
1.	If a database relating to WordPress does not already exist in the Database dropdown on the left, create one:
1.	Choose a name for your WordPress database: ‘wordpress‘ or ‘blog‘ are good, but most hosting services (especially shared hosting) will require a name beginning with your username and an underscore, so, even if you work on your own computer, we advise that you check your hosting service requirements so that you can follow them on your own server and be able to transfer your database without modification. Enter the chosen database name in the Create database field and choose the best collation for your language and encoding. In most cases it’s better to choose in the “utf8_” series and, if you don’t find your language, to choose “utf8mb4_general_ci” (Refer this article about upgrading to utf8mb4).
 
2.	Click the phpMyAdmin icon in the upper left to return to the main page, then click the Users tab. If a user relating to WordPress does not already exist in the list of users, create one:
 
1.	Click Add user.
2.	Choose a username for WordPress (‘wordpress‘ is good) and enter it in the User name field. (Be sure Use text field: is selected from the dropdown.)
3.	Choose a secure password (ideally containing a combination of upper- and lower-case letters, numbers, and symbols), and enter it in the Password field. (Be sure Use text field: is selected from the dropdown.) Re-enter the password in the Re-type field.
4.	Write down the username and password you chose.
5.	Leave all options under Global privileges at their defaults.
6.	Click Go.
7.	Return to the Users screen and click the Edit privileges icon on the user you’ve just created for WordPress.
8.	In the Database-specific privileges section, select the database you’ve just created for WordPress under the Add privileges to the following database dropdown, and click Go.
9.	The page will refresh with privileges for that database. Click Check All to select all privileges, and click Go.
10.	On the resulting page, make note of the host name listed after Server: at the top of the page. (This will usually be localhost.)
 
Step 3: Set up wp-config.php
You can either create and edit the wp-config.php file yourself, or you can skip this step and let WordPress try to do this itself when you run the installation script (step 5). (you’ll still need to tell WordPress your database information).
(For more extensive details, and step by step instructions for creating the configuration file and your secret key for password security, please see Editing wp-config.php).
Return to where you extracted the WordPress package in Step 1, rename the file wp-config-sample.php to wp-config.php, and open it in a text editor.
Enter your database information under the section labeled
 // ** MySQL settings - You can get this info from your web host ** //
DB_NAME
The name of the database you created for WordPress in Step 2.
DB_USER
The username you created for WordPress in Step 2.
DB_PASSWORD
The password you chose for the WordPress username in Step 2.
DB_HOST
The hostname you determined in Step 2 (usually localhost, but not always; see some possible DB_HOST values). If a port, socket, or pipe is necessary, append a colon (:) and then the relevant information to the hostname.
DB_CHARSET
The database character set, normally should not be changed (see Editing wp-config.php).
DB_COLLATE
The database collation should normally be left blank (see Editing wp-config.php).
Enter your secret key values under the section labeled
/* Authentication Unique Keys and Salts. */
Save the wp-config.php file.
Step 4: Upload the files
Now you will need to decide where on your domain you’d like your WordPress-powered site to appear:
– In the root directory of your website. (For example, https://example.com/)
– In a subdirectory of your website. (For example, https://example.com/blog/)
Note: The location of your root web directory in the filesystem on your web server will vary across hosting providers and operating systems. Check with your hosting provider or system administrator if you do not know where this is.
In the Root Directory
•	If you need to upload your files to your web server, use an FTP client to upload all the contents of the wordpress directory (but not the directory itself) into the root directory of your website.
If your files are already on your web server, and you are using shell access to install WordPress, move all of the contents of the wordpress directory (but not the directory itself) into the root directory of your website.
In a Subdirectory
•	If you need to upload your files to your web server, rename the wordpress directory to your desired name, then use an FTP client to upload the directory to your desired location within the root directory of your website.
•	If your files are already on your web server, and you are using shell access to install WordPress, move the wordpress directory to your desired location within the root directory of your website, and rename the directory to your desired name.
Step 5: Run the Install Script
Point a web browser to start the installation script.
•	If you placed the WordPress files in the root directory, you should visit: https://example.com/wp-admin/install.php
•	If you placed the WordPress files in a subdirectory called blog, for example, you should visit: https://example.com/blog/wp-admin/install.php
Setup configuration file
If WordPress can’t find the wp-config.php file, it will tell you and offer to try to create and edit the file itself. (You can also do this directly by loading wp-admin/setup-config.php in your web browser.) WordPress will ask you the database details and write them to a new wp-config.php file. If this works, you can go ahead with the installation; otherwise, go back and create, edit, and upload the wp-config.php file yourself (step 3).
 
Finishing installation
The following screenshots show how the installation progresses. Notice that in entering the details screen, you enter your site title, your desired user name, your choice of a password (twice), and your e-mail address. Also displayed is a check-box asking if you would like your blog to appear in search engines like Google and DuckDuckGo. Leave the box unchecked if you would like your blog to be visible to everyone, including search engines, and check the box if you want to block search engines, but allow normal visitors. Note all this information can be changed later in your Administration Screen.
 
If you successfully install the WordPress, login prompt will be displayed.
Install script troubleshooting
– If you get an error about the database when you run the install script:
– Go back to Step 2 and Step 3, and make sure you entered all the correct database information into wp-config.php.
– Make sure you granted your WordPress user permission to access your WordPress database in Step 3.
– Make sure the database server is running.
Installing WordPress at popular Hosting Companies
installing WordPress at Atlantic.net
Install WordPress On A Ubuntu 14.04 LTS
You can also install WordPress on Ubuntu with one click WordPress Hosting on Atlantic.Net.
Installing WordPress at AWS
•	Installatron WordPress Installatron WordPress is a pre-configured and ready-to-launch image that contains a WordPress website and Installatron’s WordPress management tools.
•	Architecting a Highly Scalable WordPress Site in AWS A guide for building a more expensive, highly scalable AWS implementation using Amazon’s Relational Data Store (RDS) et al.
Installing WordPress at DigitalOcean
•	How to install WordPress on Ubuntu 14.04
Installing WordPress at Linode
•	Manage Web Content with WordPress Install WordPress on a Debian Server with a LAMP Stack
You can also install WordPress on Ubuntu with one click using this StackScript on Linode.
Installing WordPress at iPage Hosting
•	This is a great step by step tutorial by IStartBlogging on how to setup your blog the smart way with iPage Hosting.
In less than 5 minutes from now, you will have your blog ready on your domain. You will install WordPress on your own domain as an Automated Process with ONE Click WordPress Installation feature from iPage hosting.
Installing WordPress at Microsoft Azure
•	Installing WordPress on Microsoft Azure is as simple as a few clicks. A hosting space and MySQL database will be created and configured, so you’re ready to start creating within a matter of seconds.
•	Running into some issues and need to troubleshoot your WordPress site on Azure? Follow this handy Troubleshooting guide for WordPress on Azure
•	There is a full listing of resources on how to learn more about WordPress on Microsoft Azure!
Common installation problems
The following are some of the most common installation problems. For more information and troubleshooting for problems with your WordPress installation, check out FAQ Installation and FAQ Troubleshooting.
I see a directory listing rather than a web page.
The web server needs to be told to view index.php by default. In Apache, use the DirectoryIndex index.php directive. The simplest option is to create a file named .htaccess in the installed directory and place the directive there. Another option is to add the directive to the web server’s configuration files.
I see lots of Headers already sent errors. How do I fix this?
You probably introduced a syntax error in editing wp-config.php.
1.	Download wp-config.php (if you don’t have shell access).
2.	Open it in a text editor.
3.	Check that the first line contains nothing but , and that there is no text after it (not even whitespace).
4.	If your text editor saves as Unicode, make sure it adds no byte order mark (BOM). Most Unicode-enabled text editors do not inform the user whether or not it adds a BOM to files; if so, try using a different text editor.
5.	Save the file, upload it again if necessary, and reload the page in your browser.
My page comes out gibberish. When I look at the source I see a lot of “<?php ?>” tags.
If the <?php ?> tags are being sent to the browser, it means your PHP is not working properly. All PHP code is supposed to be executed before the server sends the resulting HTML to your web browser. (That’s why it’s called a preprocessor.) Make sure your web server meets the requirements to run WordPress, that PHP is installed and configured properly, or contact your hosting provider or system administrator for assistance.
I keep getting an Error connecting to database message but I’m sure my configuration is correct.
Try resetting your MySQL password manually. If you have access to MySQL via shell, try issuing:
SET PASSWORD FOR 'wordpressusername'@'hostname' = OLD_PASSWORD('password');
If you do not have shell access, you should be able to simply enter the above into an SQL query in phpMyAdmin. Failing that, you may need to use your host’s control panel to reset the password for your database user.
I keep getting an Your PHP installation appears to be missing the MySQL extension which is required by WordPress message but I’m sure my configuration is correct.
Check to make sure that your configuration of your web-server is correct and that the MySQL plugin is getting loaded correctly by your web-server program. Sometimes this issue requires everything in the path all the way from the web-server down to the MySQL installation to be checked and verified to be fully operational. Incorrect configuration files or settings are often the cause of this issue.
My image/MP3 uploads aren’t working.
If you use the Rich Text Editor on a blog that’s installed in a subdirectory, and drag a newly uploaded image into the editor field, the image may vanish a couple seconds later. This is due to a problem with TinyMCE (the rich text editor) not getting enough information during the drag operation to construct the path to the image or other file correctly. The solution is to NOT drag uploaded images into the editor. Instead, click and hold on the image and select Send to Editor.

![image](https://github.com/sohel-r/How-to-install-WordPress/assets/79723101/7cef4414-c600-403b-b727-8a1693573149)

