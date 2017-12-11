---
aliases:
- /server/framework/atlassian-sdk/lifecycle-of-a-bundle-852035.html
- /server/framework/atlassian-sdk/lifecycle-of-a-bundle-852035.md
category: devguide
confluence_id: 852035
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852035
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852035
date: '2017-12-11'
guides: guides
legacy_title: Lifecycle of a Bundle
platform: server
product: atlassian-sdk
subcategory: learning
title: Lifecycle of a bundle
---
# Lifecycle of a bundle

OSGi is a dynamic platform. This means that bundles may be installed, started, updated, stopped, and uninstalled at any time during the running of the framework.

The table below shows the possible states of an OSGi bundle and how these map to the plugin states.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Status of OSGi Bundle</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>INSTALLED</p></td>
<td><p>The bundle has been installed into the OSGi container, but some of the bundle's dependencies have not yet been met. The bundle requires packages that have not been exported by any currently installed bundle.</p>
<p><strong>Plugin status: Disabled.</strong></p></td>
</tr>
<tr class="even">
<td><p>RESOLVED</p></td>
<td><p>The bundle is installed, and the OSGi system has connected up all the dependencies at a class level and made sure they are all resolved. The bundle is ready to be started. If a bundle is started and all of the bundle's dependencies are met, the bundle skips this state.</p>
<p><strong>Plugin status: Disabled.</strong></p></td>
</tr>
<tr class="odd">
<td><p>STARTING</p></td>
<td><p>A temporary state that the bundle goes through while the bundle is starting, after all dependencies have been resolved.</p>
<p><strong>Plugin status: Disabled.</strong></p></td>
</tr>
<tr class="even">
<td><p>ACTIVE</p></td>
<td><p>The bundle is running.</p>
<p><strong>Plugin status:</strong> <strong>Disabled</strong> while Spring is doing its stuff. Spring scans the Spring configuration and builds the context,</p>
<p>then hands the context to the plugin. The plugin needs the context in order to create instances of each plugin module.<br />
<strong>Enabled</strong> once Spring has handed the context to the plugin.</p></td>
</tr>
<tr class="odd">
<td><p>STOPPING</p></td>
<td><p>A temporary state that the bundle goes through while the bundle is stopping.</p>
<p><strong>Plugin status: Disabled.</strong></p></td>
</tr>
<tr class="even">
<td><p>UNINSTALLED</p></td>
<td><p>The bundle has been removed from the OSGi container.</p>
<p><strong>Plugin status: Disabled.</strong></p></td>
</tr>
</tbody>
</table>

##### RELATED TOPICS

[Behind the Scenes in the Plugin Framework](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Behind+the+Scenes+in+the+Plugin+Framework)  
[Common Coding Tasks](/server/framework/atlassian-sdk/common-coding-tasks)




















































































































































































































































































































































































