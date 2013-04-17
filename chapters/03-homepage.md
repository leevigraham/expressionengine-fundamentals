Creating a Homepage
===================

In this chapter we're going to:

* Create a new channel for the homepage (bear with me)
* Create a new custom field group and custom fields
* Create a homepage template
* Add SEO meta to the homepage
* Running content experiements on multiple homepages

Creating a homepage channel
---------------------------

For those of you who have experience with ExpressionEngine you might be thinking "Homepage channel" WTF is this guy on. Creating a homepage channel, and therefore multiple homepage channel entries has the following benefits:

* Custom fields just for the homepage. Allow site admins to change parts of the homepage that would normally difficult to change. Yes there are snippets and global variables but that means your site admins need to learn another user interface
* Schedule homepage updates with publish dates for things like holidays and other special events.
* Run content experiments using different homepages

Create a channel with the following attributes:

* Full Channel Name: `Homepage`
* Short Name: `homepage`

Then edit the channel preferences and set the following attributes:

* Channel URL: `/`
* Enable Entry Versioning: `Yes` - Trust me, one day you'll need to roll back a change. This will save you.
* Allow comments in this channel?: `no`
* Display Rich Formatting Buttons: `no`

Creating homepage custom fields
-------------------------------

Creating the Homepage channel was straight forward now let's create the homeage custom field group and custom fields and assign them to the channel.

Create a new custom field group with the following attributes:

* Group Name: `Homepage`

Now add the following custom fields:

1. Content:
	* Label: `Content`
	* Short Name: `cf_homepage_content`
	* Type: `Textarea (Rich Text)`

Then assign the custom field group to the channel.

### Custom field naming conventions 

Why `cf_homepage_content`? Naming conventions are an important part of creating any system especially when there are multiple developers. 

I use the following naming convention for all my custom fields:

	cf_ + channel_short_name + _ + field_name

* cf_ is short for 'Custom Field'. Later on we'll look at Global Variables ('gv_') and Snippets ('sn_')
* channel_short_name: In this case `homepage`
* field_name: In this case `content`

### One custom field group per channel

Follow the "one custom field group per channel rule" and you'll save yourself a lot of pain in the future. Don't be tempted to try and share a custom field group. Inevitably channel content will diverge and you'll have to explain to a content administrator why some fields work in some channels and not in others.

But what about [Publish Page Layouts](http://ellislab.com/expressionengine/user-guide/cp/content/publish_page_layouts.html)? We'll you could try and hide un-needed custom fields but they will stil be available in the templates which will cause issues for developers.

So say it out loud "one custom field group per channel" - no exceptions.

Creating homepage templates
---------------------------

Generally I follow "one template group per channel" but in this case we'll make an exception.

Create a new template group with the following attributes:

* Template Group Name: `site`
* Make the index template in this group your site's home page?: `yes`




