

Prelude
=======

@TODO

Target Audience
---------------

This book is targeted at novice to intermediate developers wishing to learn how to better structure their ExpressionEngine sites. An understanding of ExpressionEngine is required to get the most out of it, however we've tried to link to external resources where possible.

Acknowledgements
----------------

This book is inspired by [Developing Backbone.js Applications](https://github.com/addyosmani/backbone-fundamentals). The Panoc build code was taken directly from the Github Repo.

Credits
-------

@TODO

Reading
-------

@TODO

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

The ExpressionEngine Control Panel
==================================

Now that ExpressionEngine has been installed it's time to login. Here's the CP url: `http://local.ee-book.com/admin.php`

Customising the CP
------------------

The default CP is fine but thanks to the work of many third_party addon developers we can make it even better. Lets start with some simple tweaks that I consider *must have*.

### Override.css - $AUD 9.95

By Leevi Graham (Me): http://ee-garage.com/override-css

From the author:

> The default design of the default CP isn't to everyones tastes. Override.css is a stylesheet that takes the default CP theme and adds consistency, improved contrast and greater user experience for content managers and ExpressionEngine implementors. Choose one of 10 different colourways or easily generate your own.

Disclaimer: I wrote this addon.

### Module Nav - Free

By Brandon Kelly: http://devot-ee.com/add-ons/module-nav

From the author:

> Module Nav is an EE2 accessory that makes two changes to EE2’s top navigation: * Replaces the “Add-Ons” menu with a new “Modules” menu, populated with links to your modules’ CP backends * Moves the old “Add-Ons” menu into the “Admin” menu, under “Add-on Administration”

Note: If you get and error after installing checkout my [pull request](https://github.com/brandonkelly/module_nav/pull/3/files)

### Field Editor - $US 9.99

By Chris Newton: http://devot-ee.com/add-ons/field-editor

This addon is amazeballs and I can't live without it. It makes managing channel fields really easy and effecient.

From the author:

> Breathe new life into EE's channel fields editor! Adding & editing fields won't be a chore anymore. Field Editor adds powerful features to EE's standard field editor interface. Rather than laboriously clicking and editing each and every channel field or clicking and clicking and clicking to add new fields to a channel, you can now add, delete, re-order and manipulate your custom fields all in one simple interface.

### Developer - Free

By Ben Crocker: http://www.putyourlightson.net/developer

From the author:

> Developer is an accessory that allows EE site developers to quickly access the most essential sections of the control panel during site setup.

### Environment - Free

By Trevor Davis: http://devot-ee.com/add-ons/environment

From the author:

> Display which environment you are on at all times in the CP so you don't accidentally do something bad on the production environment.

There's nothing worse than for a split moment thinking you delete content on your production site. We've all done it. We'll probably do it again. This addon will at least give you a heads up.

### Zoo Flexible Admin - $US 22.00

By ExpressionEngine Zoo - http://devot-ee.com/add-ons/zoo-flexible-admin

From the author: 

> Make it easier for you and your clients to use the EE control panel. Zoo Flexible Admin lets you fully customize the control panel menu per membergroup. Insert custom links, rename, re-order and remove menu items in order to create a more intuitive menu. 

### More Addons

There's plenty more third_party addons for improving your CP experience like:

* [Draggable](http://devot-ee.com/add-ons/draggable) - $US 5.00
* [Zenbu](http://devot-ee.com/add-ons/zenbu) - $US 60.00
