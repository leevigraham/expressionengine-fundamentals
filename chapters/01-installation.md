Installing ExpressionEngine
===========================

This section describes how to modify the default folder structure in order secure your installation and bootstrap configuration for multiple development environments before running the installation wizard.

To start 

1. download the latest version of ExpressionEngine 2
2. unzip 
3. in terminal cd into the unzipped folder

```bash
cd unzipped_folder_path
```

Folder structure
----------------

Now we need to modify our folder structure before running the install wizard.

```bash
# Create a folder which will become our document root
mkdir public_html

# Move admin.php into public_html so it's accessible
mv admin.php public_html/

# Move index.php into public_html so it's accessible
mv index.php public_html/

# Move themes into public_html so it's accessible
mv themes/ public_html/

# Move images into public_html so it's accessible
mv images/ public_html/

# Move uploads into public_html so it's accessible
mv public_html/images/uploads/ public_html/

# Create subfolders to seperate member uploads and content admin uploads
mkdir public_html/uploads/member
mkdir public_html/uploads/content

# Move member upload folders into member folder
mv public_html/images/member_photos/ public_html/uploads/member/photos/
mv public_html/images/avatars/ public_html/uploads/member/
mv public_html/images/pm_attachments/ public_html/uploads/member/
mv public_html/images/signature_attachments/ public_html/uploads/member/

# Move bundled third_party addons into the root
# This makes upgrading system files easier in the future
mv system/expressionengine/third_party/ ./

# Create a placeholder folder for the site theme
mkdir public_html/themes/site_themes/default

# Create a placeholder folder for the site templates
mkdir -p views/templates
```

Folder / file permissions
--------------------------------

Set the following files to 666:

* `system/expressionengine/config/config.php`
* `system/expressionengine/config/database.php`
* `views/templates`

Set the following folders to 777:

* `system/expressionengine/cache/`
* `public_html/images/*`
* `public_html/uploads/*`

config_bootstrap.php
--------------------

NSM Config Bootstrap is a single file that allows you to:

* configure all aspects of your EE install including thrid party addons
* create multiple environment configurations
* define global variables
* define file paths

Install `config_bootstrap.php` by [following the documentation](http://ee-garage.com/nsm-config-bootstrap#toc-installation).

The default `config_bootstrap.php` assumes the folder structure modified by the script above.

Database Configuration
----------------------

Before we run the installation wizard you'll need to create a database and add the details to the `config_bootstrap.php` file.

Given we've configured the domain name to be `http://local.ee-book.com` you'll need to add your DB details [to the `local` environment configuration](https://gist.github.com/leevigraham/e0a7fb4e00bba0350705#file-config_bootstrap_v2-php-L120). 

System path configuration
-------------------------

We've moved our folders around which means we need to tell EE where to look for it's system folders.

1. Open `/public_html/admin.php` & `/public_html/index.php`
2. Change `$system_path = './system';` to `$system_path = '../system';` (Extra dot)

Configuring your webserver
--------------------------

Create a new apache virtual host with the following details:

* Domain Name: `http://local.ee-book.com`
* Local Path: `path_to_your_folder/public_html`

Installation wizard
-------------------

To install EE visit `http://local.ee-book.com/admin.php` and follow the instructions.

Don't forget to remove `/system/installer` after the install runs.

```bash
sudo rm -R system/installer
```

Next
----

Let's get to know the ExpressionEngine CP (Control Panel).
