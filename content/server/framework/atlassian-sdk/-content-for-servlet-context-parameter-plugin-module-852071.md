---
title: Content for Servlet Context Parameter Plugin Module 852071
aliases:
    - /server/framework/atlassian-sdk/-content-for-servlet-context-parameter-plugin-module-852071.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852071
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852071
confluence_id: 852071
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Servlet Context Parameter Plugin Module

## Purpose of this Module Type

Servlet Context Parameter plugin modules allow you to set parameters in the Java Servlet context shared by your plugin's servlets, filters, and listeners.

## Configuration

The root element for the Servlet Context Parameter plugin module is `servlet-context-param`. It allows the following attributes and child elements for configuration:

#### Attributes

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name</p></th>
<th><p>Required</p></th>
<th><p>Description</p></th>
<th><p>Default</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>class</p></td>
<td><p> </p></td>
<td>The class which implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>.</td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>state</p></td>
<td><p> </p></td>
<td>Indicate whether the plugin module should be disabled by default (value='disabled') or enabled by default (value='enabled').</td>
<td><p>enabled</p></td>
</tr>
<tr class="odd">
<td><p>i18n-name-key</p></td>
<td><p> </p></td>
<td>The localisation key for the human-readable name of the plugin module.</td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>key</p></td>
<td><p>Yes</p></td>
<td><p>The unique identifier of the plugin module. You refer to this key to use the resource from other contexts in your plugin, such as from the plugin Java code or JavaScript resources.</p>
<div class="panel preformatted" style="border-width: 1px;">
<div class="panelContent preformattedContent">
<pre><code>&lt;component-import key=&quot;appProps&quot; interface=&quot;com.atlassian.sal.api.ApplicationProperties&quot;/&gt;</code></pre>
</div>
</div>
<p>In the example, <code>appProps</code> is the key for this particular module declaration, for <code>component-import</code>, in this case.</p>
I.e. The identifier of the context parameter.</td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p> </p></td>
<td><p>The human-readable name of the plugin module. I.e. The human-readable name of the context parameter.</p></td>
<td><p>The plugin key</p></td>
</tr>
<tr class="even">
<td><p>system</p></td>
<td><p> </p></td>
<td>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</td>
<td><p>false</p></td>
</tr>
</tbody>
</table>

#### Elements

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name</p></th>
<th><p>Required</p></th>
<th><p>Description</p></th>
<th><p>Default</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>description</p></td>
<td><p> </p></td>
<td><p>The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body. I.e. the description of the listener.</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>param-name</p></td>
<td><p>Yes</p></td>
<td><p>The servlet context parameter name.</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>param-value</p></td>
<td><p>Yes</p></td>
<td><p>The servlet context parameter value.</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>

## Example

Here is an example `atlassian-plugin.xml` file containing a single servlet context parameter:

``` javascript
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic Servlet context parameter module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <servlet-context-param key="helloWorld">
        <description>Sets the Hello World text.</description>
        <param-name>text</param-name>
        <param-value>Hello World!</param-value>
    </servlet-context-param>
</atlassian-plugin>
```

## Notes

Some information to be aware of when developing or configuring a Servlet Context Parameter plugin module:

-   This parameter will only be available to servlets, filters, and context listeners within your plugin.
















































































































































































































































































































