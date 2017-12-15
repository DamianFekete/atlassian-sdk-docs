---
aliases:
- /server/framework/atlassian-sdk/using-the-osgi-browser-8946139.html
- /server/framework/atlassian-sdk/using-the-osgi-browser-8946139.md
category: devguide
confluence_id: 8946139
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8946139
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8946139
date: '2017-12-08'
guides: guides
legacy_title: Using the OSGi Browser
platform: server
product: atlassian-sdk
subcategory: learning
title: Using the OSGi Browser
---
# Using the OSGi Browser

The Universal Plugin Manager (UPM) provides a ton of really useful information to plugin developers on its **OSGi tab**. The OSGi tab is a "hidden" feature which is not visible by default because it is not relevant for the average system administrator.

**The OSGi tab is available in UPM 1.3 and later.**

For more information about OSGi and its use in the Atlassian Plugin Framework, please read about <a href="/server/framework/atlassian-sdk/osgi-spring-and-the-plugin-framework" class="createlink">OSGi, Spring and the Plugin Framework</a>.

## How to enable the OSGi tab

{{% note %}}

Use the Atlassian Plugin SDK

The OSGi tab is automatically visible when using the Atlassian Plugin SDK.

{{% /note %}}

There are two easy ways to enable the OSGi tab:

-   Start your product with the `atlassian.dev.mode` flag set to true
-   Visit `/plugins/servlet/upm#osgi` in your web browser

A cookie is stored upon loading the tab for the first time, marking the tab as visible for future use.

## Browsing the OSGi tab

Listed on the OSGi tab is a collection of installed OSGi bundles. The bundles are represented by their ID and key (which matches their plugin key).

Expanding an OSGi bundle reveals a great deal of information, including the bundle's version and symbolic name.

Additionally, depending on the information present in the bundle's manifest, you may or may not see the following expandable areas:

-   Bundle-ClassPath
-   Bundle-NativeCode
-   Bundle-RequiredExecutionEnvironment
-   Dynamic-ImportPackage
-   Export-Package
-   Fragment-Host
-   Ignore-Package
-   Import-Package
-   Private-Package
-   Require-Bundle

Each of these expandable areas, when appropriate, will link to other bundles which relate to the bundle in use.

## Using the OSGi tab to resolve plugin deployment errors

In addition to viewing useful bundle information, the OSGi tab is an excellent resource for debugging plugin deployment errors.

For example, if you see a `ClassNotFoundException` thrown upon plugin startup:

1.  Locate and expand your plugin's bundle on the OSGi tab.
2.  Expand the `Import-Package` section.
3.  Check for red packages. Packages are marked red to indicate that they could not be resolved. This would quite possibly prevent your plugin from being enabled.

Additionally, it is possible that you are importing the right packages but of the wrong versions. With the OSGi tab you can determine exactly which version of each package is in use, and from which bundle the package is provided.

##### RELATED TOPICS

<a href="/server/framework/atlassian-sdk/osgi-spring-and-the-plugin-framework" class="createlink">OSGi, Spring and the Plugin Framework</a>  
[Developing for the Marketplace](https://developer.atlassian.com/display/MARKET/Developing+for+the+Marketplace)
