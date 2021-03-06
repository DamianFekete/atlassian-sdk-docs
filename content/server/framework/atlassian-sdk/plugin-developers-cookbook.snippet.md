---
aliases:
- /server/framework/atlassian-sdk/852028.html
- /server/framework/atlassian-sdk/852028.md
category: devguide
confluence_id: 852028
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852028
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852028
date: '2017-12-08'
legacy_title: Plugin Developer's Cookbook
platform: server
product: atlassian-sdk
subcategory: other
title: Plugin Developer's Cookbook
---
# Plugin Developer's Cookbook

This page is in DRAFT and is visible to **Atlassian staff only**.

This page contains a collection of guidelines on the more advanced facilities the plugin framework offers to plugin developers.

First we show a table comparing plugins of different complexities, and answering the question '**Do I need to xxx?**'. This information is for plugin developers who have heard of or read about all the capabilities and complexities that are available to an OSGi plugin, and then wonder how much of it they need to know. The Atlassian Plugin Framework takes care of most of the complexity for you, particularly if you are developing a simple plugin for a single product. Take a look at the table for a quick reference to what you need to do.

Then we list the more advanced things you may like to do, with links to the detailed information.

## Do I need to xxx?

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Do I need to...</p></th>
<th><p>Simple Plugin</p></th>
<th><p>Complex Plugin</p></th>
<th><p>Cross-Product Plugin</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Add <code>plugins-version=&quot;2&quot;</code> to the plugin descriptor?</p></td>
<td><p>yes</p></td>
<td><p>yes</p></td>
<td><p>yes</p></td>
</tr>
<tr class="even">
<td><p>Put my plugin JAR into <code>WEB-INF/lib</code>?</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Mess with the manifest?</p></td>
<td><p>no</p></td>
<td><p>maybe</p></td>
<td><p>yes</p></td>
</tr>
<tr class="even">
<td><p>Specify my own Spring config files in <code>META-INF/spring</code> folder?</p></td>
<td><p>no</p></td>
<td><p>maybe</p></td>
<td><p>maybe</p></td>
</tr>
<tr class="odd">
<td><p>Define a class path for dependent JARs, other than <code>META-INF\lib</code>?</p></td>
<td><p>no</p></td>
<td><p>no</p></td>
<td><p>maybe</p></td>
</tr>
<tr class="even">
<td><p>Add bundle instructions in <code>atlassian-plugin.xml</code>?</p></td>
<td><p>no</p></td>
<td><p>probably</p></td>
<td><p>yes, if not generating your own manifest</p></td>
</tr>
<tr class="odd">
<td><p>Modify the build process?</p></td>
<td><p>no</p></td>
<td><p>yes, if generating your own manifest</p></td>
<td><p>yes</p></td>
</tr>
<tr class="even">
<td><p>Use maven?</p></td>
<td><p>no</p></td>
<td><p>probably</p></td>
<td><p>yes</p></td>
</tr>
</tbody>
</table>

Definitions:

-   **Simple plugin** -- A 'simple' plugin is a self-contained plugin written for a single Atlassian application only. The plugin has no dependencies other than those already provided by the host application. No other plugins depend on this plugin.
-   **Complex plugin** -- A 'complex' plugin is a plugin written for a single Atlassian application. The plugin has one or more dependencies on other plugins or on external libraries not provided by the host application, and may have other plugins that depend on it.
-   **Cross-product plugin** -- A 'cross-product' plugin is a plugin that can be installed into more than one of the Atlassian applications, where the plugin code (and perhaps configuration) is the same for all relevant applications.

## Advanced Topics

-   [Declaring a Dependency on Another Plugin](/server/framework/atlassian-sdk/declaring-a-dependency-on-another-plugin.snippet)
-   [Declaring a Dependency on a Third-Party Package](/server/framework/atlassian-sdk/declaring-a-dependency-on-a-third-party-package.snippet)
-   [Defining an Extension Point in my Plugin](/server/framework/atlassian-sdk/defining-an-extension-point-in-my-plugin.snippet)
-   [Exposing a Service in my Plugin](/server/framework/atlassian-sdk/exposing-a-service-in-my-plugin.snippet)

##### RELATED TOPICS

[OSGi, Spring and the Plugin Framework](/server/framework/atlassian-sdk/osgi-spring-and-the-plugin-framework)  
[Common Coding Tasks](/server/framework/atlassian-sdk/common-coding-tasks)
