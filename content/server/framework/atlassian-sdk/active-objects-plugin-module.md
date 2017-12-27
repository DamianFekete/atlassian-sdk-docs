---
aliases:
- /server/framework/atlassian-sdk/active-objects-plugin-module-5669175.html
- /server/framework/atlassian-sdk/active-objects-plugin-module-5669175.md
category: devguide
confluence_id: 5669175
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669175
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669175
date: '2017-12-08'
guides: guides
legacy_title: Active Objects Plugin Module
platform: server
product: atlassian-sdk
subcategory: learning
title: Active Objects plugin module
---
# Active Objects plugin module

 

## Purpose of this Module Type

The Active Objects plugin module allows you to use the Active Objects service to persist data using the <a href="http://activeobjects.java.net" class="external-link">Active Objects library</a>.

## Configuration

The root element for the Active Objects plugin module is `ao`. It allows the following attributes and child elements for configuration:

#### Attributes

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 80%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>namespace</p></td>
<td><p>A namespace for the plugin module. If present, this value is used to generate unique portions of the AO table names (see <a href="/server/framework/atlassian-sdk/table-names">Table names</a>).</p>
<p>While not required, we recommend that you add a namespace value. If not present, an internal form of the plugin key is used, which can potentially change.</p>
<p>Note that changing the plugin key (or this namespace value) causes new tables to be created based on the new table names.</p>
<p><strong>Default:</strong> The plugin key.</p></td>
</tr>
<tr class="even">
<td><p>key</p></td>
<td><p>The identifier of the plugin module. This key must be unique within the plugin where it is defined.<br />
INFO: Sometimes, in other contexts, you may need to uniquely identify a module. Do this with the <strong>complete module key</strong>.</p>
<p>A module with key <code>fred</code> in a plugin with key <code>com.example.modules</code> will have a complete key of <code>com.example.modules:fred</code></p>
<p>which serves as the identifier of the component.</p>
<p><strong>Required.</strong></p>
<p><strong>Default:</strong> N/A.</p></td>
</tr>
<tr class="odd">
<td><p>i18n-name-key</p></td>
<td><p>The localisation key for the human-readable name of the plugin module.</p></td>
</tr>
<tr class="even">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module.</p>
<p><strong><strong>Default:</strong></strong> The plugin key.</p></td>
</tr>
</tbody>
</table>

#### Elements

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 80%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>entity</p></td>
<td><p>Fully qualified name of an entity to be managed by the module.</p>
<p><strong>Required.</strong></p>
<p><strong>Default:</strong> N/A.</p></td>
</tr>
<tr class="even">
<td><p>upgradeTask</p></td>
<td><p>Fully qualified name of an upgrade task to be run on activation of the module.</p>
<p><strong>Default:</strong> N/A.</p></td>
</tr>
<tr class="odd">
<td><p>description</p></td>
<td><p>The description of the plugin module.</p>
<p>The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body.</p></td>
</tr>
</tbody>
</table>

## Example

Here is an example `atlassian-plugin.xml` file containing a single public component:

**Module definition example**

``` xml
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
  <plugin-info>
    <description>A basic Active Objects module test</description>
    <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
    <version>1.0</version>
  </plugin-info>

  <ao key="ao-module">
    <description>The AO module for this plugin.</description>
    <entity>com.myapp.MyEntity</entity>
    <upgradeTask>com.myapp.upgrades.v1.Version1UpgradeTask</upgradeTask>
  </ao>
</atlassian-plugin>
```

## Notes

There is a document explaining how to [use the plugin](https://developer.atlassian.com/display/AO/Developing+your+plugin+with+Active+Objects).  
Also have a look at the sample <a href="https://bitbucket.org/atlassian_tutorial/ao-tutorial" class="external-link">Todo plugin</a> developed which is a simple example plugin using Active Object you can build upon.
