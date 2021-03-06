---
aliases:
- /server/framework/atlassian-sdk/plugin-modules-852136.html
- /server/framework/atlassian-sdk/plugin-modules-852136.md
category: reference
confluence_id: 852136
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852136
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852136
date: '2017-12-08'
legacy_title: Plugin Modules
platform: server
product: atlassian-sdk
subcategory: modules
title: Plugin modules
---
# Plugin modules

An Atlassian plugin can implement one or more plugin modules to affect the underlying Atlassian application. You can add modules to a plugin project using the Atlassian Plugin SDK. The <code>atlas-create-&lt;app&gt;-plugin-module</code> command lets you generate the initial plugin module code through a series of prompts. The module types you can create vary by target application. The modules listed below comprise the common module types; they apply across application types.  

Below is detailed information of each plugin module type.

#### Plugin Module Types in the Atlassian Platform

Plugin module types, as defined in this guide, are generally available in all Atlassian applications. But in some cases, an application may exclude support for a specific module type -- the plugin module descriptor is not loaded into the application and the module type is therefore not available. Please refer to the application's plugin guide for more information about which module types are supported.

-   [Plugin Module Index](/server/framework/atlassian-sdk/plugin-module-index)
-   [Component Import Plugin Module](/server/framework/atlassian-sdk/component-import-plugin-module)
-   [Component Plugin Module](/server/framework/atlassian-sdk/component-plugin-module)
-   [Module Type Plugin Module](/server/framework/atlassian-sdk/module-type-plugin-module)
-   [Servlet Context Listener Plugin Module](/server/framework/atlassian-sdk/servlet-context-listener-plugin-module)
-   [Servlet Context Parameter Plugin Module](/server/framework/atlassian-sdk/servlet-context-parameter-plugin-module)
-   [Servlet Filter Plugin Module](/server/framework/atlassian-sdk/servlet-filter-plugin-module)
-   [Servlet Plugin Module](/server/framework/atlassian-sdk/servlet-plugin-module)
-   [Template Context Item Plugin Module](/server/framework/atlassian-sdk/template-context-item-plugin-module)
-   [Web Item Plugin Module](/server/framework/atlassian-sdk/web-item-plugin-module)
-   [Web Panel Plugin Module](/server/framework/atlassian-sdk/web-panel-plugin-module)
-   [Web Panel Renderer Plugin Module](/server/framework/atlassian-sdk/web-panel-renderer-plugin-module)
-   [Web Resource Plugin Module](/server/framework/atlassian-sdk/web-resource-plugin-module)
-   [Web Resource Transformer Plugin Module](/server/framework/atlassian-sdk/web-resource-transformer-plugin-module)
-   [Web Section Plugin Module](/server/framework/atlassian-sdk/web-section-plugin-module)
-   [REST Plugin Module](/server/framework/atlassian-sdk/rest-plugin-module)
-   [Gadget plugin module type](https://developer.atlassian.com/display/GADGETS/Packaging+your+Gadget+as+an+Atlassian+Plugin)
-   **Product-specific plugin modules** -- Product-specific plugin types are not documented here as they are usually unique to an Atlassian application. See the application's developer documentation for more information.

#### Application-specific plugin modules within a cross-product plugin

While developing a cross-product plugin, you may find yourself needing different implementations/components to be running in the various applications. This can be accomplished with the `application` attribute. The `application` attribute works on all plugin module descriptors.

For example, let's say we have a plugin that works in both JIRA and Confluence, but we want application-specific implementations to be used as components. We can declare the following in our `application-plugin.xml`:

``` xml
<component key="jiraPluginComponent" class="com.example.JiraPluginComponent" 
           interface="com.example.PluginComponent" application="jira" />
<component key="confluencePluginComponent" class="com.example.ConfluencePluginComponent"  
           interface="com.example.PluginComponent" application="confluence" />
```
