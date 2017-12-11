---
aliases:
- /server/framework/atlassian-sdk/adding-a-configuration-ui-for-your-plugin-851988.html
- /server/framework/atlassian-sdk/adding-a-configuration-ui-for-your-plugin-851988.md
category: devguide
confluence_id: 851988
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851988
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851988
date: '2017-12-11'
guides: guides
legacy_title: Adding a Configuration UI for your Plugin
platform: server
product: atlassian-sdk
subcategory: learning
title: Adding a configuration UI for your plugin
---
# Adding a configuration UI for your plugin

 

## Purpose of the Configuration UI

A plugin can present configurable settings to Atlassian instance administrators. This is useful where your plugin requires configuration or user-specific settings to work.

Here are some examples of plugins which provide a configuration UI:

-   The <a href="https://plugins.atlassian.com/plugin/details/251" class="external-link">Google Maps plugin for Confluence</a> requires a Google API Key from Google, which needs to be configured on each server before it will work properly.
-   The <a href="https://plugins.atlassian.com/plugin/details/236" class="external-link">WebDAV plugin for Confluence</a> provides a configuration screen that is available both from the UPM and from a web item in the Administration menu.

In [Configuring the Plugin Descriptor](https://developer.atlassian.com/display/DOCS/Configuring+the+Plugin+Descriptor), we tell you how to create the XML descriptor file for your plugin. In [Plugin Modules](https://developer.atlassian.com/display/DOCS/Plugin+Modules), we tell you how to define the modules within your plugin. Below is information on defining the links to the configuration UI for your plugin.

## Adding a Configuration Link for the Entire Plugin

To add a configuration link for your plugin as a whole, place a single `param` element with the name `configure.url` within the `plugin-info` element at the top of the plugin descriptor:

``` xml
<plugin-info>
    <description>A macro which displays Google maps within a Confluence page.</description>
    <vendor name="Atlassian Software Systems Pty Ltd" url="http://www.atlassian.com/"/>
    <version>0.1</version>
    <param name="configure.url">/admin/plugins/gmaps/configurePlugin.action</param>
</plugin-info>
```

This `param` element causes a button with the Configure label to appear in the details view for the plugin in the 'Manage Add-ons' page. The URL value identifies the page the contains the configuration form. For more information about implementing a configuration UI, see the [Creating an Admin Configuration Form](https://developer.atlassian.com/display/DOCS/Creating+an+Admin+Configuration+Form) tutorial.

## Notes

-   Configuration links are relative to the application.
-   The configuration URL is a link to a separate page, which you have defined using one of the following:
    -   A new XWork action that you have defined via an XWork plugin module.
    -   Or a servlet defined via a [Servlet](https://developer.atlassian.com/display/DOCS/Servlet+Plugin+Module) plugin module.
-   Not all applications support configuration links, so you may need to create a web item link in the administration menu to link to your configuration page.








































































































































































































































































































































