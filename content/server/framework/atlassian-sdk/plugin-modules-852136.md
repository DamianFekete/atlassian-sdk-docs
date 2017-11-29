---
title: Plugin Modules 852136
aliases:
    - /server/framework/atlassian-sdk/plugin-modules-852136.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852136
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852136
confluence_id: 852136
platform:
product:
category:
subcategory:
---
# Plugin modules

An Atlassian plugin can implement one or more plugin modules to affect the underlying Atlassian application. You can add modules to a plugin project using the Atlassian Plugin SDK. The atlas-create-&lt;app&gt;-plugin-module command lets you generate the initial plugin module code through a series of prompts. The module types you can create vary by target application. The modules listed below comprise the common module types; they apply across application types.  

Below is detailed information of each plugin module type.

#### Plugin Module Types in the Atlassian Platform

Plugin module types, as defined in this guide, are generally available in all Atlassian applications. But in some cases, an application may exclude support for a specific module type -- the plugin module descriptor is not loaded into the application and the module type is therefore not available. Please refer to the application's plugin guide for more information about which module types are supported.

-   [Plugin Module Index](/server/framework/atlassian-sdk/plugin-module-index-2818387.html)
-   [Component Import Plugin Module](/server/framework/atlassian-sdk/component-import-plugin-module-852117.html)
-   [Component Plugin Module](/server/framework/atlassian-sdk/component-plugin-module-852118.html)
-   [Module Type Plugin Module](/server/framework/atlassian-sdk/module-type-plugin-module-852019.html)
-   [Servlet Context Listener Plugin Module](/server/framework/atlassian-sdk/servlet-context-listener-plugin-module-852123.html)
-   [Servlet Context Parameter Plugin Module](/server/framework/atlassian-sdk/servlet-context-parameter-plugin-module-852120.html)
-   [Servlet Filter Plugin Module](/server/framework/atlassian-sdk/servlet-filter-plugin-module-852110.html)
-   [Servlet Plugin Module](/server/framework/atlassian-sdk/servlet-plugin-module-852096.html)
-   [Template Context Item Plugin Module](/server/framework/atlassian-sdk/template-context-item-plugin-module-852139.html)
-   [Web Item Plugin Module](/server/framework/atlassian-sdk/web-item-plugin-module-852014.html)
-   [Web Panel Plugin Module](/server/framework/atlassian-sdk/web-panel-plugin-module-852000.html)
-   [Web Panel Renderer Plugin Module](/server/framework/atlassian-sdk/web-panel-renderer-plugin-module-852106.html)
-   [Web Resource Plugin Module](/server/framework/atlassian-sdk/web-resource-plugin-module-852116.html)
-   [Web Resource Transformer Plugin Module](/server/framework/atlassian-sdk/web-resource-transformer-plugin-module-852002.html)
-   [Web Section Plugin Module](/server/framework/atlassian-sdk/web-section-plugin-module-852133.html)

<!-- -->

-   [REST Plugin Module](/server/framework/atlassian-sdk/rest-plugin-module-4915219.html)
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

























