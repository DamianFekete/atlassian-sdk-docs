---
aliases:
- /server/framework/atlassian-sdk/851971.html
- /server/framework/atlassian-sdk/851971.md
category: devguide
confluence_id: 851971
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851971
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851971
date: '2017-12-08'
legacy_title: Version 1 or Version 2 Plugin (Glossary Entry)
platform: server
product: atlassian-sdk
subcategory: other
title: Version 1 or version 2 plugin
---
# Version 1 or version 2 plugin

A plugin is a bundle of code, resources and configuration files that can be dropped into an Atlassian product to add new functionality or change the behaviour of existing features.

Every plugin is made up of one or more plugin modules. A single plugin may do many things, while a plugin module represents a single function of the plugin.

There are two versions of plugins in the Atlassian Plugin Framework:

-   **Version 1 plugins.** These may be static (deployed in `WEB-INF/lib`) or dynamic (via the web UI, only in Confluence) and should work the same as they did in version 1 of the Atlassian Plugin Framework. The capabilities and features available to version 1 plugins vary significantly across products.
-   **Version 2 plugins.** These plugins are dynamically deployed on an internal <a href="http://osgi.org" class="external-link">OSGi</a> container to provide a consistent set of features and behaviours, regardless of the application the plugin is running on. Version 2 plugins have to be specifically declared as such, using the `plugins-version="2"` attribute in `atlassian-plugin.xml`.

##### RELATED TOPICS

[Plugin Framework Glossary](/server/framework/atlassian-sdk/plugin-framework-glossary)  
[Plugin Framework](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Plugin+Framework)





































































































































































































