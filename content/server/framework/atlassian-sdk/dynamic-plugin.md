---
aliases:
- /server/framework/atlassian-sdk/852157.html
- /server/framework/atlassian-sdk/852157.md
category: devguide
confluence_id: 852157
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852157
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852157
date: '2017-12-08'
legacy_title: Dynamic Plugin (Glossary Entry)
platform: server
product: atlassian-sdk
subcategory: other
title: Dynamic plugin
---
# Dynamic plugin

A dynamic plugin is one that can be loaded into an application and used without restarting the application. There are two types of dynamic plugins:

-   Some version 1 dynamic plugins, that can be deployed via the web UI, available only in Confluence.
-   Version 2 plugins, that are dynamically deployed on an internal <a href="http://osgi.org/" class="external-link">OSGi</a> container to provide a consistent set of features and behaviours, regardless of the application the plugin is running on. Version 2 plugins have to be specifically declared as such, using the `plugins-version="2"` attribute in `atlassian-plugin.xml`.

Read about dynamically reinstalling/deploying plugins during plugin development using CLI in the Atlassian Plugin SDK.

A non-dynamic plugin is called a <a href="/server/framework/atlassian-sdk/static-plugin" class="createlink">static plugin</a>.

##### RELATED TOPICS

<a href="/server/framework/atlassian-sdk/plugin-framework-glossary/">Plugin Framework Glossary</a>  
[Plugin Framework](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Plugin+Framework)

