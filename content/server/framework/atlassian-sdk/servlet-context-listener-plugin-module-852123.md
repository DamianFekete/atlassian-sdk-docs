---
aliases:
- /server/framework/atlassian-sdk/servlet-context-listener-plugin-module-852123.html
- /server/framework/atlassian-sdk/servlet-context-listener-plugin-module-852123.md
category: reference
confluence_id: 852123
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852123
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852123
legacy_url: https://developer.atlassian.com/docs/getting-started/plugin-modules/servlet-context-listener-plugin-module
new_url: /server/framework/atlassian-sdk/servlet-context-listener-plugin-module
platform: server
product: atlassian-sdk
subcategory: modules
title: Servlet Context Listener plugin module
---
# Servlet Context Listener plugin module

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p><a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852134">Atlassian Plugin Framework 2.1</a> and later.<br />
<em>Note</em>: The Servlet Context Listener plugin module described below is available only for OSGi-based plugins using version 2.1 or later of the Plugin Framework.</p></td>
</tr>
</tbody>
</table>

 

 

## Purpose of this Module Type

Servlet Context Listener plugin modules allow you to deploy Java Servlet context listeners as a part of your plugin. This helps you to integrate easily with frameworks that use context listeners for initialisation.

## Configuration

The root element for the Servlet Context Listener plugin module is **`servlet-context-listener`**. It allows the following attributes and child elements for configuration:

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
<td><p>The class which implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>. </p>
<p>The servlet context listener Java class. Must implement <code>javax.servlet.ServletContextListener</code>.</p></td>
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
 
<p>I.e. the identifier of the context listener.</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module. </p>
<p>I.e. the human-readable name of the listener.</p>
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

-   description - The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body. I.e. the description of the listener.

## Example

Here is an example `atlassian-plugin.xml` file containing a single servlet context listener:

``` xml
<atlassian-plugin name="Hello World Listener" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic Servlet context listener module test - says "Hello World!"</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <servlet-context-listener name="Hello World Listener" key="helloWorld" class="com.example.myplugins.helloworld.HelloWorldListener">
        <description>Initialises the Hello World plugin.</description>
    </servlet-context-listener>
</atlassian-plugin>
```

## Notes

Some information to be aware of when developing or configuring a Servlet Context Listener plugin module:

-   The servlet context you listen for will not be created on web application startup. Instead, it will be created the first time a servlet or filter in your plugin is accessed after each time it is enabled, triggering a new instance of your listener followed by the calling of the listener's `contextCreated()` method. This means that if you disable a plugin containing a listener and re-enable it again, the following will happen:
    1.  The `contextDestroyed()` method will be called on your listener after the plugin was disabled.
    2.  A new servlet context will be created after the plugin was re-enabled.
    3.  Your listener will be instantiated.
    4.  The method `contextCreated()` on your listener will be called.

##### RELATED TOPICS

[Plugin Modules](/server/framework/atlassian-sdk/plugin-modules)



































































