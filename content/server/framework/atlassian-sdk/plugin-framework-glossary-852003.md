---
title: Plugin Framework Glossary 852003
aliases:
    - /server/framework/atlassian-sdk/plugin-framework-glossary-852003.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852003
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852003
confluence_id: 852003
platform:
product:
category:
subcategory:
---
# Plugin Framework glossary

Below is a list of all entries in the glossary, plus the first few lines of content. Click the link on an entry to see the full text.

-   [Trusted Application Authentication (Glossary Entry)](/server/framework/atlassian-sdk/2818272.html) -- Trusted application authentication (or 'trusted apps') is an Atlassian-developed mechanism allowing two applications to exchange information on behalf of a logged-in user. For example, an administrator can configure JIRA http://www.atlassian.com/software/jira and Confluence http://www.atlassian.com/software/confluence to communicate in a trusted way, so that Confluence can request information from JIRA on behalf of the currently logged-in user. JIRA will not ask the user to log in again or to su
-   [Bundle (Glossary Entry)](/server/framework/atlassian-sdk/852005.html) -- A bundle is a JAR file with special OSGi entries in its manifest and containing classes, resources, and other JARs.
-   [Complex Plugin (Glossary Entry)](/server/framework/atlassian-sdk/852127.html) -- A 'complex' plugin is a plugin written for a single Atlassian application. The plugin has one or more dependencies on other plugins or on external libraries not provided by the host application, and may have other plugins that depend on it.
-   [Cross-Product Plugin (Glossary Entry)](/server/framework/atlassian-sdk/852128.html) -- A 'cross-product' plugin is a plugin that can be installed into more than one of the Atlassian applications, where the plugin code (and perhaps configuration) is the same for all relevant applications.
-   [Dynamic Plugin (Glossary Entry)](/server/framework/atlassian-sdk/852157.html) -- A dynamic plugin is one that can be loaded into an application and used without restarting the application. There are two types of dynamic plugins:
-   [Lifecycle (Glossary Entry)](/server/framework/atlassian-sdk/851979.html) -- A lifecycle is the sequence of states a bundle goes through: uninstalled, installed, resolved, starting, stopping, active.
-   [Plugin (Glossary Entry)](/server/framework/atlassian-sdk/851969.html)
-   [Service (Glossary Entry)](/server/framework/atlassian-sdk/851977.html) -- A service is an object instance exposed under the one or more interfaces that it implements and a map of properties.
-   [Service Registry (Glossary Entry)](/server/framework/atlassian-sdk/851982.html) -- A service registry is a map of one or more interfaces bound to object instances, with a set of properties attached to it.
-   [Simple Plugin (Glossary Entry)](/server/framework/atlassian-sdk/852115.html) -- A 'simple' plugin is a self-contained plugin written for a single Atlassian application only. The plugin has no dependencies other than those already provided by the host application. No other plugins depend on this plugin.
-   [Static Plugin (Glossary Entry)](/server/framework/atlassian-sdk/852149.html) -- A static plugin is one that requires a restart of the application after installing the plugin. Static plugins are deployed in WEB-INF/lib.
-   [Version 1 or Version 2 Plugin (Glossary Entry)](/server/framework/atlassian-sdk/851971.html)

##### RELATED TOPICS

[OSGi, Spring and the Plugin Framework](/server/framework/atlassian-sdk/852146.html)  
[Plugin Framework](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Plugin+Framework)

























