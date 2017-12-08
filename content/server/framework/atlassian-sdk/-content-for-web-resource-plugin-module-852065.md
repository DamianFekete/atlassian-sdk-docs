---
title: Content for Web Resource Plugin Module 852065
aliases:
    - /server/framework/atlassian-sdk/-content-for-web-resource-plugin-module-852065.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852065
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852065
confluence_id: 852065
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Web Resource Plugin Module

## Purpose of this Module Type

Web Resource plugin modules allow plugins to define downloadable resources. If your plugin requires the application to serve additional static Javascript or CSS files, you will need to use downloadable web resources to make them available. Web resources are added at the top of the page in the header with the cache-related headers set to never expire. In addition, you can specify web resources like CSS and JavaScript to be included in specific contexts within the application.

## Configuration

The root element for the Web Resource plugin module is `web-resource`. It allows the following attributes and child elements for configuration:

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
<td>The class which implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>.</td>
</tr>
<tr class="even">
<td><p>state</p>
<p>(<strong>default:</strong> enabled)</p></td>
<td>Indicate whether the plugin module should be disabled by default (value='disabled') or enabled by default (value='enabled').</td>
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
That is, the identifier of the web resource.</td>
</tr>
<tr class="odd">
<td><p>name</p>
<p>(<strong>default:</strong> the plugin key)</p></td>
<td><p>The human-readable name of the plugin module. That is, the human-readable name of the web resource.</p></td>
</tr>
<tr class="even">
<td><p>location</p></td>
<td><p>The <a href="https://developer.atlassian.com/display/JIRADEV/Web+Fragments#WebFragments-Locations">location</a> into which this web item should be placed.</p></td>
</tr>
<tr class="odd">
<td><p>system</p>
<p>(<strong>default:</strong> false)</p></td>
<td>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</td>
</tr>
</tbody>
</table>

**\*key attribute is required**

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
<td>The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body. That is, the description of the resource.</td>
</tr>
<tr class="even">
<td><p>resource</p>
<p> </p></td>
<td>Indicate whether the plugin module should be disabled by default (value='disabled') or enabled by default (value='enabled').</td>
</tr>
<tr class="odd">
<td><p>dependency</p></td>
<td>Dependencies for the web resource module. A web resource can depend on other web resource(s) to be available. Dependencies are defined in the format 'pluginKey:webResourceKey' e.g. <code>&lt;dependency&gt;com.atlassian.auiplugin:ajs&lt;/dependency&gt;</code><br />
Note: This element is only available in <a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852077">Plugin Framework 2.2</a> and later.</td>
</tr>
<tr class="even">
<td><p>context</p></td>
<td>Use this element to include web resources like CSS and JavaScript on all screens of a specific type in the application. See below.<br />
Note: This element is only available in <a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852001">Plugin Framework 2.5</a> and later.</td>
</tr>
<tr class="odd">
<td><p>transformation</p></td>
<td><p>Use this element to make a particular transformer available to the web resource in the plugin. Example:</p>
<p> </p>
<pre><code>&lt;transformation extension=&quot;txt&quot;&gt;
  &lt;transformer key=&quot;template&quot; /&gt;
&lt;/transformation&gt;</code></pre>
<p> </p>
<p>For a complete description, please refer to the page on <a href="/server/framework/atlassian-sdk/web-resource-transformer-plugin-module">Web Resource Transformer Plugin Modules</a>.<br />
Note: This element is only available in <a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852001">Plugin Framework 2.5</a> and later.</p></td>
</tr>
<tr class="even">
<td><p>condition</p></td>
<td><p>Use this element to define when this web resource should display or not.  See <a href="/server/framework/atlassian-sdk/web-item-plugin-module-852014.html#conditionand-conditions-elements">Web Item Conditions</a> for more information.<br />
Note: This element is only available in Plugin Framework 2.7 or later.</p></td>
</tr>
</tbody>
</table>

**\*resource element is required**

## Example

Here is an example `atlassian-plugin.xml` file containing a single web resource:

``` xml
<atlassian-plugin name="Hello World Resource" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic web resource module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <web-resource key="scriptaculous" name="Scriptaculous" >
        <resource type="download" name="scriptaculous.js" location="includes/js/effects/scriptaculous.js" />
        <resource type="download" name="effects.js" location="includes/js/effects/effects.js" />
    </web-resource>
</atlassian-plugin>
```

## Referring to Web Resources

In your plugin, you need to refer to a `PageBuilderService` and call the `requireResource()` method. A reference to a `PageBuilderService` can be injected into your constructor:

``` java
public MyServlet extends HttpServlet
{
    private PageBuilderService pageBuilderService;

    public MyServlet(PageBuilderService pageBuilderService)
    {
        this.pageBuilderService = pageBuilderService;
    }

    protected final void doGet(HttpServletRequest httpServletRequest, HttpServletResponse httpServletResponse) throws IOException
    {
        //should be the full module key for the <webreference> module.
        pageBuilderService.assembler().resources().requireWebResource("example.plugin.helloworld:scriptaculous");
        // more code
    }
}
```

 

## Web Resource Contexts

In [version 2.5](https://developer.atlassian.com/pages/viewpage.action?pageId=852001) and later of the Plugin Framework, you can automatically include web resources like CSS and JavaScript on all screens of a specific type in the application. These are called 'web resource contexts'. The currently available contexts are:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Context</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>atl.general</p></td>
<td><p>Everywhere except administration screens.</p>
{{% note %}}
<div class="confluence-information-macro-note confluence-information-macro">
<div class="confluence-information-macro-body">
<p>An issue prevents this context from working in the JIRA login page in JIRA 5.x and later. See <a href="https://jira.atlassian.com/browse/JRA-27960" class="uri external-link">https://jira.atlassian.com/browse/JRA-27960</a> for more information and a work-around.</p>
</div>
</div>
{{% /note %}}</td>
</tr>
<tr class="even">
<td><p>atl.admin</p></td>
<td><p>Administration screens. Use with care because poorly formed CSS or JavaScript can prevent access to administering the application.</p></td>
</tr>
<tr class="odd">
<td><p>atl.userprofile</p></td>
<td><p>User profile screens.</p></td>
</tr>
<tr class="even">
<td><p>atl.popup</p></td>
<td><p>Browser pop-up windows. This will open a new window for things like OAuth authorisation, and similar purposes.</p></td>
</tr>
</tbody>
</table>

The above contexts are applicable to all Atlassian applications. In addition to these application-independent contexts, each Atlassian application can also supply its own application-specific contexts.  

**Example:** To configure your web resource to be included in every page (both administration and non-administration pages), add `<context>` child elements to your `<web-resource>` element in your `atlassian-plugin.xml`:

``` xml
<web-resource name="Resources" key="resources">
       <resource name="foo.js" type="download" location="resources/foo.js"/>
       <context>atl.general</context>
</web-resource>
```

Using web resource contexts allows you to provide plugins that dynamically create HTML using JavaScript on any page in the application. For example, the Confluence <a href="http://labs.atlassian.com/wiki/display/ACN" class="external-link">Content Navigation Plugin</a> includes a snippet of JavaScript on every page in the application, which listens for a particular keyboard shortcut to open a little search box on top the Confluence UI.

##### Introducing new contexts

If your plugin adds a number of screens to the application, you may find it useful to introduce a new web resource context for your plugin that your plugin web resources (or any other plugin web resource) can hook into, to be automatically included on these screens.

To introduce a new context in your plugin Velocity templates, you can call the `requireResourcesForContext()` method on the `WebResourceManager` object from your Velocity templates:

``` javascript
$webResourceManager.requireResourcesForContext("com.acme.plugin.fancy-context")
```

This will include any resource in the page that specifies a context like this in its definition: `<context>com.acme.plugin.fancy-context</context>`.

We recommend that you namespace your new contexts in this way so as not to clash with any future contexts in the applications themselves or in other plugins.

## Batched Mode

The default mode for serving web resources in Plugin Framework 2.2 is batched mode. Batched mode refers to the serving of multiple plugin resources (of the same type) in one request. For example, the two scriptaculous web resources defined above would be served in one request, containing both scriptaculous.js and effects.js. Hence, batching reduces the number of HTTP requests that web browsers need to make to load a web page.

URLs for batched resources are in the following format:

``` bash
SERVER_ROOT/s/BUILD_NUM/PLUGIN_VERSION/SYSTEM_COUNTER/_/download/batch/js/PLUGIN_KEY:MODULE_KEY/BATCHNAME.js
SERVER_ROOT/s/BUILD_NUM/PLUGIN_VERSION/SYSTEM_COUNTER/_/download/batch/css/PLUGIN_KEY:MODULE_KEY/BATCHNAME.css
```

For the above scriptaculous example, the following code will be inserted in the header of the page:

``` xml
<script type="text/javascript"
  src="http://jira.example.com/s/170/1.0/1/_/download/batch/js/jira.extra.impresence:scriptaculous/jira.extra.impresence:scriptaculous.js"></script>
```

{{% note %}}

Batched resource URLs do not include any URL path prefixes that were specified in the individual `<resource>` names. This can cause problems if a resource refers to another resource by a relative URL.

For instance, if your web resource contains a stylesheet with the name `"css/styles.css"`, and that stylesheet uses an image from the same web resource whose name is `"images/foo.png"`, you could use the relative URL `../images/foo.png` if batch mode is off; but with batch mode on, the stylesheet will no longer have `css/` in its URL, so the relative URL will be wrong. (The absolute URL of the image remains the same, since images are not affected by batching.)

The plugin framework attempts to help by rewriting URLs in stylesheets to be relative to the server root, but there is a <a href="https://studio.atlassian.com/browse/PLUG-854" class="external-link">known issue</a> that prevents this from working correctly. Therefore, if you do not know whether batch mode will be on or off, avoid using a subpath prefix in the `name` attribute of any resource that contains relative URL references. In the above example, the stylesheet's name would be simply `"styles.css"` and the relative image URL would be `images/foo.png`. The `location` attribute, since it refers to the location of the actual file before any batching or URL rewriting takes place, does not need to change.

{{% /note %}}

  
  

## Transforming Web Resources

!!! Transformers are only available in [Plugin Framework 2.5](https://developer.atlassian.com/pages/viewpage.action?pageId=852001) and later.

The plugin framework provides web resource transformers that you can use to manipulate static web resources before they are batched and delivered to the browser.

To use a web resource transformer, you need the following elements in your `atlassian-plugin.xml` file:

-   **The transformer module:** A `<web-resource-transformer>` element, defining the transformer plugin module. This module can be in the same plugin as the web resource, or in a different plugin.
-   **Transformation elements in the web resource module:** A `<transformation>` element and its child `<transformer>` element inside the `<web-resource>` block, making a particular transformer available to the web resource in the plugin.

For a complete description and example, please refer to the page on Web Resource Transformer plugin modules.

## Notes

-   Since the resources are returned with headers that tell the browser to cache the content indefinitely, during development, you may need to hold down the "shift" key while reloading the page to force the browser to re-request the files.

Use this element to make a particular transformer available to the web resource in the plugin. Example:

  


















































































































































































































































































































