
# How to installing WordPress on macOS, Windows, or Linux


# How to install WordPress

The instructions provided  general steps for installing WordPress on any web server, including both remote servers and local development environments. They are applicable regardless of the operating system, so they can be used for installing WordPress on macOS, Windows, or Linux

## Before Installing WordPress

Before you begin the install, there are a few things you need to have and do. Refer the article [Before You Install](https://developer.wordpress.org/advanced-administration/before-install/).


## Basic Instructions

Here's the quick version of the instructions

1. Download and unzip the WordPress package if you haven't already.
2. Create a database for WordPress on your web server, as well as a [MySQL](https://wordpress.org/documentation/article/glossary/#mysql) (or MariaDB) user who has all privileges for accessing and modifying it.
3. (Optional) Find and rename `wp-config-sample.php` to `wp-config.php`, then edit the file [(see Editing wp-config.php)](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/) and add your database information.

**Note:** If you are not comfortable with renaming files, step 3 is optional and you can skip it as the install program will create the `wp-config.php` file for you.

4. Upload the WordPress files to the desired location on your web server:
    - If you want to integrate WordPress into the root of your domain move or upload all contents of the unzipped WordPress directory (excluding the WordPress directory itself) into the root directory of your web server.
    - If you want to have your WordPress installation in its own subdirectory on your website, create the blog directory on your server and upload the contents of the unzipped WordPress package to the directory via FTP.
    - **Note:** If your FTP client has an option to convert file names to lower case, make sure it's disabled.
5. Run the WordPress installation script by accessing the URL in a web browser. This should be the URL where you uploaded the WordPress files.


## Detailed instructions 

### Step 1: Download and Extract

Download and unzip the WordPress package from [wordpress.org/download/](https://wordpress.org/download/).

- If you will be uploading WordPress to a remote web server, download the WordPress package to your computer with a web browser and unzip the package.
- If you will be using FTP, skip to the next step – uploading files is covered later.
- If you have [shell](https://wordpress.org/documentation/article/glossary/#shell) access to your web server, and are comfortable using console-based tools, you may wish to download WordPress directly to your [web server](https://wordpress.org/documentation/article/glossary/#web-server) using wget (or lynx or another console-based web browser) if you want to avoid [FTPing](https://wordpress.org/documentation/article/glossary/#ftp):
    - wget https://wordpress.org/latest.tar.gz
    - Then extract the package using:
    - tar -xzvf latest.tar.gz

    The WordPress package will extract into a folder called wordpress in the same directory that you downloaded latest.tar.gz.

### Step 2: Download and Extract

If you are using a [hosting provider](https://wordpress.org/documentation/article/glossary/#hosting-provider), you may already have a WordPress database set up for you, or there may be an automated setup solution to do so. Check your hosting provider's support pages or your control panel for clues about whether or not you'll need to create one manually.

If you determine that you'll need to create one manually, follow the instructions for Using phpMyAdmin below to create your WordPress username and database. For other tools such as Plesk, cPanel and Using the MySQL Client, refer the article [Creating Database for WordPress.](https://developer.wordpress.org/advanced-administration/before-install/creating-database/)

If you have only one database and it is already in use, you can install WordPress in it – just make sure to have a distinctive prefix for your tables to avoid over-writing any existing database tables.

#### Using phpMyAdmin

If your web server has [phpMyAdmin](https://wordpress.org/documentation/article/glossary/#phpmyadmin) installed, you may follow these instructions to create your WordPress username and database. If you work on your own computer, on most Linux distributions you can install PhpMyAdmin automatically.

_**Note:** These instructions are written for phpMyAdmin 4.4; the phpMyAdmin user interface can vary slightly between versions._

1. If a database relating to WordPress does not already exist in   the **Database** dropdown on the left, create one:
  * Choose a name for your WordPress database: '`wordpress`' or '`blog`' are good, but most hosting services (especially shared hosting) will require a name beginning with your username and an underscore, so, even if you work on your own computer, we advise that you check your hosting service requirements so that you can follow them on your own server and be able to transfer your database without modification. Enter the chosen database name in the **Create database** field and choose the best collation for your language and encoding. In most cases it's better to choose in the "utf8_" series and, if you don't find your language, to choose "utf8mb4_general_ci" [(Refer this article about upgrading to utf8mb4)](https://make.wordpress.org/core/2015/04/02/the-utf8mb4-upgrade/).
    ![Creating a database in phpMyAdmin 4.4](https://wordpress.org/documentation/files/2018/10/phpMyAdmin_create_database_4.4.jpg)
2. Click the **phpMyAdmin** icon in the upper left to return to the main page, then click the **Users** tab. If a user relating to WordPress does not already exist in the list of users, create one:
    ![Create user in phpMyAdmin 4.4](https://codex.wordpress.org/images/2/26/users.jpg)
        a. Click **Add user**.
        b. Choose a username for WordPress ('`wordpress`' is good) and enter it in the **User name** field. (Be sure **Use text field**: is selected from the dropdown.)
        c. Choose a secure password (ideally containing a combination of upper- and lower-case letters, numbers, and symbols), and enter it in the **Password** field. (Be sure **Use text field**: is selected from the dropdown.) Re-enter the password in the **Re-type** field.
        d. Write down the username and password you chose.
        e. Leave all options under **Global privileges** at their defaults.
        f. Click **Go**.
        g. Return to the Users screen and click the **Edit privileges** icon on the user you've just created for WordPress.
        h. In the **Database-specific privileges** section, select the database you've just created for WordPress under the **Add privileges to the following database** dropdown, and click Go.
        i. The page will refresh with privileges for that database. Click **Check All** to select all privileges, and click **Go**.
        j. On the resulting page, make note of the host name listed after **Server**: at the top of the page. (This will usually be **localhost**.)

    ![Make sure the server is localhost](https://wordpress.org/documentation/files/2018/10/phpMyAdmin_server_info_4.4.jpg)


### Step 3: Set up wp-config.php
You can either create and edit the wp-config.php file yourself, or you can skip this step and let WordPress try to do this itself when you run the installation script (step 5). (you'll still need to tell WordPress your database information).

(For more extensive details, and step by step instructions for creating the configuration file and your secret key for password security, please see [Editing wp-config.php](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/)).

Return to where you extracted the WordPress package in Step 1, rename the file wp-config-sample.php to wp-config.php, and open it in a text editor.

[Enter your database information](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/#configure-database-settings) under the section labeled

```
 // ** MySQL settings - You can get this info from your web host ** //
```

**DB_NAME**
    The name of the database you created for WordPress in Step 2.
**DB_USER**
    The username you created for WordPress in Step 2.
**DB_PASSWORD** 
    The password you chose for the WordPress username in Step 2.
**DB_HOST** 
    The hostname you determined in Step 2 (usually localhost, but not always; see [some possible DB_HOST values](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/#set-database-host)). If a port, socket, or pipe is necessary, append a colon (:) and then the relevant information to the hostname.
**DB_CHARSET**
The database character set, normally should not be changed (see [Editing wp-config.php](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/)).
**DB_COLLATE**
The database collation should normally be left blank (see [Editing wp-config.php](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/)).

[Enter your secret key values](https://developer.wordpress.org/advanced-administration/wordpress/wp-config/) under the section labeled
```
/* Authentication Unique Keys and Salts. */
```
Save the `wp-config.php` file.

### Step 4: Upload the files

Now you will need to decide where on your domain you'd like your WordPress-powered site to appear:
- In the root directory of your website. 
- In a subdirectory of your website. 

_**Note:** The location of your root web directory in the filesystem on your [web server](https://wordpress.org/documentation/article/glossary/#web-server) will vary across [hosting providers](https://wordpress.org/documentation/article/glossary/#hosting-provider) and operating systems. Check with your hosting provider or system administrator if you do not know where this is._

#### In the Root Directory

- If you need to upload your files to your web server, use an [FTP](https://wordpress.org/documentation/article/glossary/#ftp) client to upload all the contents of the wordpress directory (but not the directory itself) into the root directory of your website.
If your files are already on your web server, and you are using [shell](https://wordpress.org/documentation/article/glossary/#shell) access to install WordPress, move all of the contents of the wordpress directory (but not the directory itself) into the root directory of your website.

#### In a Subdirectory

- If you need to upload your files to your web server, rename the wordpress directory to your desired name, then use an [FTP](https://wordpress.org/documentation/article/glossary/#ftp) client to upload the directory to your desired location within the root directory of your website.
- If your files are already on your web server, and you are using [shell](https://wordpress.org/documentation/article/glossary/#shell) access to install WordPress, move the wordpress directory to your desired location within the root directory of your website, and rename the directory to your desired name.

### Step 5: Run the Install Script

Point a web browser to start the installation script.



#### Setup configuration file

If WordPress can't find the wp-config.php file, it will tell you and offer to try to create and edit the file itself. (You can also do this directly by loading `wp-admin/setup-config.php` in your web browser.) WordPress will ask you the database details and write them to a new wp-config.php file. If this works, you can go ahead with the installation; otherwise, go back and [create, edit, and upload the wp-config.php file yourself (step 3).](https://developer.wordpress.org/advanced-administration/before-install/howto-install/#step-3-set-up-wp-config-php)

![The WordPress setup screen](https://wordpress.org/documentation/files/2018/10/install-step3_v47.png)

#### Finishing installation

The following screenshots show how the installation progresses. Notice that in entering the details screen, you enter your site title, your desired user name, your choice of a password (twice), and your e-mail address. Also displayed is a check-box asking if you would like your blog to appear in search engines like Google and DuckDuckGo. Leave the box unchecked if you would like your blog to be visible to everyone, including search engines, and check the box if you want to block search engines, but allow normal visitors. Note all this information can be changed later in your [Administration Screen](https://wordpress.org/documentation/article/administration-screens/).

![The WordPress installation screen](https://wordpress.org/documentation/files/2018/10/install-step5_v47.png)

If you successfully install the WordPress, login prompt will be displayed.







