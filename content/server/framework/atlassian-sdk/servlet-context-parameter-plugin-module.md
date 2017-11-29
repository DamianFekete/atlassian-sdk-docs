---
aliases:
- /server/framework/atlassian-sdk/servlet-context-parameter-plugin-module-852120.html
- /server/framework/atlassian-sdk/servlet-context-parameter-plugin-module-852120.md
category: reference
confluence_id: 852120
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852120
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852120
legacy_url: https://developer.atlassian.com/docs/getting-started/plugin-modules/servlet-context-parameter-plugin-module
new_url: /server/framework/atlassian-sdk/servlet-context-parameter-plugin-module
platform: server
product: atlassian-sdk
subcategory: modules
title: Servlet Context Parameter plugin module
---
# Servlet Context Parameter plugin module

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p><a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852134">Atlassian Plugin Framework 2.1</a> and later.<br />
<em>Note</em>: The Servlet Context Parameter plugin module described below is available only for OSGi-based plugins using version 2.1 or later of the Plugin Framework.</p></td>
</tr>
</tbody>
</table>

 

 

## Purpose of this Module Type

Servlet Context Parameter plugin modules allow you to set parameters in the Java Servlet context shared by your plugin's servlets, filters, and listeners.

## Configuration

The root element for the Servlet Context Parameter plugin module is `servlet-context-param`. It allows the following attributes and child elements for configuration:

#### Attributes

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name*</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>class</p></td>
<td><p>The class which implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>.</p></td>
</tr>
<tr class="even">
<td><p>state</p>
<p> </p></td>
<td><p>Indicate whether the plugin module should be disabled by default (value='disabled') or enabled by default (value='enabled').</p>
<p><strong>Default:</strong> enabled.</p></td>
</tr>
<tr class="odd">
<td><p>i18n-name-key</p></td>
<td>The localisation key for the human-readable name of the plugin module.</td>
</tr>
<tr class="even">
<td><p>key</p></td>
<td><p>The unique identifier of the plugin module. You refer to this key to use the resource from other contexts in your plugin, such as from the plugin Java code or JavaScript resources.</p>
<p> </p>
<pre><code>&lt;component-import key=&quot;appProps&quot; interface=&quot;com.atlassian.sal.api.ApplicationProperties&quot;/&gt;</code></pre>
<p> </p>
<p>In the example, <code>appProps</code> is the key for this particular module declaration, for <code>component-import</code>, in this case.</p>
<p>I.e. The identifier of the context parameter.</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module. </p>
<p>I.e. The human-readable name of the context parameter.</p>
<p><strong>Default:</strong> the plugin key.</p></td>
</tr>
<tr class="even">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
</tbody>
</table>

**\*key attribute is required.**

#### Elements

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name*</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>description</p></td>
<td><p>The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body. </p>
<p>I.e. the description of the listener.</p></td>
</tr>
<tr class="even">
<td><p>param-name</p>
<p> </p></td>
<td><p>The servlet context parameter name.</p></td>
</tr>
<tr class="odd">
<td><p>param-value</p></td>
<td>The servlet context parameter value.</td>
</tr>
</tbody>
</table>

**\*param-name and param-value elements are required.**

## Example

Here is an example `atlassian-plugin.xml` file containing a single servlet context parameter:

``` xml
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

##### RELATED TOPICS

[Plugin Modules](/server/framework/atlassian-sdk/plugin-modules)





















































































































































