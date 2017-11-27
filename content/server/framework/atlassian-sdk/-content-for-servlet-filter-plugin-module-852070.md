---
title: Content for Servlet Filter Plugin Module 852070
aliases:
    - /server/framework/atlassian-sdk/-content-for-servlet-filter-plugin-module-852070.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852070
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852070
confluence_id: 852070
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Servlet Filter Plugin Module

## Purpose of this Module Type

Servlet Filter plugin modules allow you to deploy Java Servlet filters as a part of your plugin, specifying the location and ordering of your filter. This allows you to build filters that can tackle tasks like profiling and monitoring as well as content generation.

## Configuration

The root element for the Servlet Filter plugin module is `servlet-filter`. It allows the following attributes and child elements for configuration:

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
<td><p>The class which implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>. The servlet filter Java class must implement <code>javax.servlet.Filter</code>.</p></td>
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
I.e. the identifier of the servlet filter.</td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>location</p></td>
<td><p> </p></td>
<td><p>The position of the filter in the application's filter chain. If two plugins provide filters at the same position, the 'weight' attribute (see below) is evaluated.</p>
<ul>
<li><strong>after-encoding</strong> - Near the very top of the filter chain in the application, but after any filters which ensure the integrity of the request.</li>
<li><strong>before-login</strong> - Before the filter that logs in the user with any authentication information included in the request.</li>
<li><strong>before-decoration</strong> - Before the filter which does decoration of the response, typically with Sitemesh.</li>
<li><strong>before-dispatch</strong> - At the end of the filter chain, before any servlet or filter which handles the request by default.</li>
</ul></td>
<td><p>before-dispatch</p></td>
</tr>
<tr class="even">
<td><p>name</p></td>
<td><p> </p></td>
<td><p>The human-readable name of the plugin module. I.e. the human-readable name of the filter.</p></td>
<td><p>The plugin key</p></td>
</tr>
<tr class="odd">
<td><p>system</p></td>
<td><p> </p></td>
<td>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</td>
<td><p>false</p></td>
</tr>
<tr class="even">
<td><p>weight</p></td>
<td><p> </p></td>
<td><p>The weight of the filter, used to decide which order to place the filter in the chain for filters which have specified the same 'location' attribute (see above). The higher weight, the lower the filter's position.</p></td>
<td><p>100</p></td>
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
<td><p>The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body. I.e. the description of the filter.</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>init-param</p></td>
<td><p> </p></td>
<td><p>Initialisation parameters for the filter, specified using <code>param-name</code> and <code>param-value</code> sub-elements, just as in <code>web.xml</code>. This element and its child elements may be repeated.</p></td>
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>resource</p></td>
<td><p> </p></td>
<td>A resource for this plugin module. This element may be repeated. A 'resource' is a non-Java file that a plugin may need in order to operate. Refer to <a href="https://developer.atlassian.com/display/DOCS/Adding+Resources+to+your+Project">Adding Resources to your Project</a> for details on defining a resource.</td>
<td><p>N/A</p></td>
</tr>
<tr class="even">
<td><p>url-pattern</p></td>
<td><p>Yes</p></td>
<td><p>The pattern of the URL to match. This element may be repeated.</p>
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
<td><p>N/A</p></td>
</tr>
<tr class="odd">
<td><p>dispatcher</p></td>
<td><p> </p></td>
<td><p>Determines when the filter is triggered. You can include multiple <code>dispatcher</code> elements.<br />
If this element is present, its content must be one of the following, corresponding to the filter dispatcher options defined in the Java Servlet 2.4 specification:</p>
<ul>
<li><code>REQUEST</code>: the filter applies to requests that came directly from the client</li>
<li><code>INCLUDE</code>: the filter applies to server-side includes done via <code>RequestDispatcher.include()</code></li>
<li><code>FORWARD</code>: the filter applies to requests that are forwarded via <code>RequestDispatcher.forward()</code></li>
<li><code>ERROR</code>: the filter applies to requests that are handled by an error page<br />
Note: This element is only available in Plugin Framework 2.5 and later.<br />
If this element is not present, the default is <code>REQUEST</code>. (This is also the behaviour for Plugin Framework releases earlier than 2.5.)</li>
</ul></td>
<td><p>Filter will be triggered only for requests from the client</p></td>
</tr>
</tbody>
</table>

## Example

Here is an example `atlassian-plugin.xml` file containing a single servlet filter:

``` javascript
<atlassian-plugin name="Hello World Filter" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic Servlet filter module test - says "Hello World!</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <servlet-filter name="Hello World Servlet" key="helloWorld" class="com.example.myplugins.helloworld.HelloWorldFilter" location="before-dispatch" weight="200">
        <description>Says Hello World, Australia or your name.</description>
        <url-pattern>/helloworld</url-pattern>
        <init-param>
            <param-name>defaultName</param-name>
            <param-value>Australia</param-value>
        </init-param>
        <dispatcher>REQUEST</dispatcher>
        <dispatcher>FORWARD</dispatcher>
    </servlet-filter>
</atlassian-plugin>
```

## Accessing your Servlet Filter

Your servlet will be accessible within the Atlassian web application via each `url-pattern` you specify, but unlike the [Servlet Plugin Module](/server/framework/atlassian-sdk/servlet-plugin-module), the `url-pattern` is relative to the root of the web application.

For example, if you specify a `url-pattern` of `/helloworld` as above, and your Atlassian application was deployed at <a href="http://yourserver/jira" class="uri external-link">http://yourserver/jira</a> -- then your servlet filter would be accessed at <a href="http://yourserver/jira/helloworld" class="uri external-link">http://yourserver/jira/helloworld</a> .

## Notes

Some information to be aware of when developing or configuring a Servlet Filter plugin module:

-   Your servlet filter's `init()` method will not be called on web application startup, as for a normal filter. Instead, this method will be called the first time your filter is accessed after each time it is enabled. This means that if you disable a plugin containing a filter or a single servlet filter module, and re-enable it again, the filter will be re-created and its `init()` method will be called again.
-   Because servlet filters are deployed beneath root, be careful when choosing each `url-pattern` under which your filter is deployed. If you plan to handle the request in the filter, it is recommended to use a value that will always be unique to the world!
-   Some application servers, like WebSphere 6.1, won't call servlet filters if there is no underlying servlet to match the URL. On these systems, you will only be able to create a filter to handle normal application URLs.
















































































































































































































































































































