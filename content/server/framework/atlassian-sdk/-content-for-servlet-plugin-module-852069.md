---
title: Content for Servlet Plugin Module 852069
aliases:
    - /server/framework/atlassian-sdk/-content-for-servlet-plugin-module-852069.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852069
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852069
confluence_id: 852069
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Servlet Plugin Module

## Purpose of this Module Type

Servlet plugin modules enable you to deploy Java servlets as a part of your plugins.

## Configuration

The root element for the Servlet plugin module is **`servlet`**. It allows the following attributes and child elements for configuration:

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
<td><p>The servlet Java class. Must be a subclass of <code>javax.servlet.http.HttpServlet</code>.</p>
<p>See the plugin framework guide to <a href="/server/framework/atlassian-sdk/creating-plugin-module-instances">creating plugin module instances</a>.</p></td>
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
<td>The unique identifier of the plugin module. You refer to this key to use the resource from other contexts in your plugin, such as from the plugin Java code or JavaScript resources.
<p> </p>
<pre><code>&lt;component-import key=&quot;appProps&quot; interface=&quot;com.atlassian.sal.api.ApplicationProperties&quot;/&gt;</code></pre>
<p> </p>
<p>In the example, <code>appProps</code> is the key for this particular module declaration, for <code>component-import</code>, in this case.</p>
I.e. the identifier of the servlet.</td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module. </p>
<p>I.e. the human-readable name of the servlet.</p>
<p><strong>Default:</strong> the plugin key.</p></td>
</tr>
<tr class="even">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
</tbody>
</table>

**\*class and key attributes are default.**

 

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
<p>I.e. the description of the servlet.</p></td>
</tr>
<tr class="even">
<td><p>init-param</p>
<p> </p></td>
<td><p>Initialisation parameters for the servlet, specified using <code>param-name</code> and <code>param-value</code> sub-elements,</p>
<p>just as in <code>web.xml</code>. This element and its child elements may be repeated.</p></td>
</tr>
<tr class="odd">
<td><p>resource</p></td>
<td>A resource for this plugin module. This element may be repeated. A 'resource' is a non-Java file that a plugin may need in order to operate. Refer to <a href="https://developer.atlassian.com/display/DOCS/Adding+Resources+to+your+Project">Adding Resources to your Project</a> for details on defining a resource.</td>
</tr>
<tr class="even">
<td><p>url-pattern</p></td>
<td><p>The pattern of the URL to match. This element may be repeated.</p>
<p></p>
<p>The URL pattern format is used in Atlassian plugin types to map them to URLs. On the whole, the pattern rules are consistent with those defined in the Servlet 2.3 API. The following wildcards are supported:</p>
<ul>
<li>* matches zero or many characters, including directory slashes</li>
<li>? matches zero or one character</li>
</ul>
<h6 id="examples">Examples</h6>
<ul>
<li><code>/mydir/*</code> matches <code>/mydir/myfile.xml</code></li>
<li><code>/*/admin/*.??ml</code> matches <code>/mydir/otherdir/admin/myfile.html</code></li>
</ul></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module.</p>
<p>I.e. the human-readable name of the servlet.</p>
<p><strong>Default:</strong> the plugin key.</p></td>
</tr>
<tr class="even">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
</tbody>
</table>

**\*url-pattern element is required.**

## Example

Here is an example `atlassian-plugin.xml` file containing a single servlet:

``` xml
<atlassian-plugin name="Hello World Servlet" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic Servlet module test - says "Hello World!</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <servlet name="Hello World Servlet" key="helloWorld" class="com.example.myplugins.helloworld.HelloWorldServlet">
        <description>Says Hello World, Australia or your name.</description>
        <url-pattern>/helloworld</url-pattern>
        <init-param>
            <param-name>defaultName</param-name>
            <param-value>Australia</param-value>
        </init-param>
    </servlet>
</atlassian-plugin>
```

## Accessing your Servlet

Your servlet will be accessible within the Atlassian web application via each `url-pattern` you specify, beneath the `/plugins/servlet` parent path.

For example, if you specify a `url-pattern` of `/helloworld` as above, and your Atlassian application was deployed at <a href="http://yourserver/jira" class="uri external-link">http://yourserver/jira</a> -- then your servlet would be accessed at <a href="http://yourserver/jira/plugins/servlet/helloworld" class="uri external-link">http://yourserver/jira/plugins/servlet/helloworld</a> .

## Notes

Some information to be aware of when developing or configuring a Servlet plugin module:

-   Your servlet's `init()` method will not be called on web application startup, as for a normal servlet. Instead, this method will be called the first time your servlet is accessed after each time it is enabled. This means that if you disable a plugin containing a servlet, or a single servlet module, and re-enable it again, the servlet is re-instantiated and its `init()` method will be called again.
-   Because all servlet modules are deployed beneath a common `/plugins/servlet` root, be careful when choosing each `url-pattern` under which your servlet is deployed. It is recommended to use a value that will always be unique to the world!

















































































































































































































































































































