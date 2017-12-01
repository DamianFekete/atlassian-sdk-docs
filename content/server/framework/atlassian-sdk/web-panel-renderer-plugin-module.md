---
aliases:
- /server/framework/atlassian-sdk/web-panel-renderer-plugin-module-852106.html
- /server/framework/atlassian-sdk/web-panel-renderer-plugin-module-852106.md
category: reference
confluence_id: 852106
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852106
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852106
legacy_url: https://developer.atlassian.com/docs/getting-started/plugin-modules/web-panel-renderer-plugin-module
new_url: /server/framework/atlassian-sdk/web-panel-renderer-plugin-module
platform: server
product: atlassian-sdk
subcategory: modules
title: Web Panel Renderer plugin module
---
# Web Panel Renderer plugin module

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p><a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852001">Atlassian Plugin Framework 2.5</a> and later.</p></td>
</tr>
</tbody>
</table>

 

 

## Purpose of this Module Type

The Web Panel Renderer plugin module allows plugins to define custom renderer engines for [web panels](https://developer.atlassian.com/display/DOCS/Web+Panel+Plugin+Module). (Web panels are bits of HTML that will be inserted into a page.)

## Configuration

The root element for the Web Panel Renderer plugin module is `web-panel-renderer`. It allows the following attributes and child elements for configuration:

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
<td><p>The class which implements <a href="https://studio.atlassian.com/source/browse/PLUG/trunk/atlassian-plugins-webfragment/src/main/java/com/atlassian/plugin/web/renderer/WebPanelRenderer.java?r=56664" class="external-link">com.atlassian.plugin.web.renderer.WebPanelRenderer</a>.</p>
<p>This class is responsible for turning a web panel's content into proper HTML.</p>
<p>See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>.</p></td>
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
<p>In the example, <code>appProps</code> is the key for this particular module declaration, for <code>component-import</code>, in this case.</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module.</p>
<p>Used only in the plugin's administrative user interface.</p></td>
</tr>
<tr class="even">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
</tbody>
</table>

**\*class and key attributes are required.**

## Writing a Custom Renderer

To create your own renderer you should create a class that implements <a href="https://studio.atlassian.com/source/browse/PLUG/trunk/atlassian-plugins-webfragment/src/main/java/com/atlassian/plugin/web/renderer/WebPanelRenderer.java?r=56664" class="external-link">com.atlassian.plugin.web.renderer.WebPanelRenderer</a>.

As an example we will create a plugin for the <a href="https://studio.atlassian.com/browse/REFAPP" class="external-link">Atlassian Reference Application</a> (version 2.5.0 or higher). We will create a web panel template renderer for <a href="http://freemarker.sourceforge.net" class="external-link">FreeMarker templates</a>, which is a format that is not supported by the Atlassian Plugin Framework out of the box. We will then also add a web panel that uses a FreeMarker template.

1.  Using the [Atlassian Plugin SDK](https://developer.atlassian.com/display/DOCS/Working+with+the+SDK), create a new plugin for the Reference Application and make sure the generated `pom.xml` file uses version 2.5.0 or higher:

    ``` bash
    $ atlas-create-refapp-plugin
    ```

2.  Add the FreeMarker library to the Maven dependencies:

    **pom.xml**

    ``` xml
    ...
            <dependency>
                <groupId>freemarker</groupId>
                <artifactId>freemarker</artifactId>
                <version>2.3.9</version>
            </dependency>
    ...
    ```

3.  Create your renderer class:

    ``` java
    package refapptest.freemarker;

    import com.atlassian.plugin.Plugin;
    import com.atlassian.plugin.web.renderer.RendererException;
    import com.atlassian.plugin.web.renderer.WebPanelRenderer;
    import freemarker.cache.ClassTemplateLoader;
    import freemarker.template.Configuration;
    import freemarker.template.DefaultObjectWrapper;
    import freemarker.template.Template;
    import freemarker.template.TemplateException;

    import java.io.IOException;
    import java.io.Writer;
    import java.util.Map;

    public class FreeMarkerWebPanelRenderer implements WebPanelRenderer
    {
        private Template loadTemplate(String filename) throws IOException
        {
            final Configuration conf = new Configuration();
            conf.setObjectWrapper(new DefaultObjectWrapper());
            conf.setTemplateLoader(new ClassTemplateLoader(this.getClass(), "/"));
            return conf.getTemplate(filename);
        }

        public String getResourceType()
        {
            return "freemarker";
        }

        public void render(String templateFile, Plugin plugin, Map<String, Object> stringObjectMap, Writer writer)
                throws RendererException, IOException
        {
            try
            {
                loadTemplate(templateFile).process(stringObjectMap, writer);
            }
            catch (TemplateException te)
            {
                throw new RendererException(String.format(
                        "Unable to render freemarker template %s: %s", templateFile, te.getMessage()), te);
            }
        }

        public String renderFragment(String templateFile, Plugin plugin, Map<String, Object> stringObjectMap)
                throws RendererException
        {
            throw new AssertionError("Not yet implemented.");
        }
    }
    ```

      
      
    Note how the `WebPanelRenderer` interface declares two render methods: one that takes the name of a template file and one that takes the whole template as a String. In this example we have only implemented the former method. The latter is left as an exercise for you. The consequence of this is that we will not be able to embed our FreeMarker content in `atlassian-plugin.xml`.

4.  Add the new renderer to `atlassian-plugin.xml`:

    **atlassian-plugin.xml**

    ``` xml
    ...
        <web-panel-renderer key="freemarkerWebPanelRenderer" class="refapptest.freemarker.FreeMarkerWebPanelRenderer"/>
    ...
    ```

5.  Add a web panel to the Reference Application's administration page that uses this new renderer:

    **atlassian-plugin.xml**

    ``` xml
    ...
        <web-panel key="aFreeMarkerPanel" location="atl.admin.body">
            <resource name="view" type="freemarker" location="templates/mytemplate.ftl"/>
        </web-panel>
    ...
    ```

6.  Add your FreeMarker template:

    **src/main/resources/templates/mytemplate.ftl**

    ``` xml
    <#assign color = "DarkRed">
    <div style="color: ${color};">
        <p>
            This is a FreeMarker Web Panel!
        </p>

        <#assign people = [{"name":"Joe", "age":25}, {"name":"Fred", "age":18}]>
        <ul>
        <#list people as person>
            <li>${person.name} is ${person.age}</li>
        </#list>
        </ul>
    </div>
    ```

7.  Start up the Reference Application using the command: `$ atlas-mvn refapp:run`)
8.  Go to: <a href="http://localhost:5990/refapp/admin" class="uri external-link">http://localhost:5990/refapp/admin</a>

## Known Limitations

You may have noticed how the configuration for our FreeMarker's template loader uses a `freemarker.cache.ClassTemplateLoader` instance which expects templates to be on the classpath. To do this, FreeMarker's `ClassTemplateLoader` constructor takes a `Class` instance and then calls `Class.getResource()` when it needs to load a template.

In our example we use `FreeMarkerWebPanelRenderer.class`, which means that our renderer is limited to rendering templates that live in its own plugin JAR file. This is sufficient for this tutorial which has the renderer, the web panel and the template all in the same plugin. However, it would not work when the renderer is shared with other plugins and needs to render a template that lives in another plugin JAR.

If you want to build a shared FreeMarker renderer this way, you would have to implement your own `freemarker.cache.TemplateLoader`. Instead of taking a `Class` instance, your template loader would take the `ClassLoader` that is returned by `plugin.getClassLoader()`.

To keep the example clear and simple, we have chosen to accept this limitation. However, note that it has been addressed properly in the full source code that is available below.

## Source Code

To access the full source code for this plugin, you can:

-   <a href="http://svn.atlassian.com/fisheye/browse/public/contrib/tutorials/web-panel-renderer/trunk" class="external-link">browse it online</a>.
-   <a href="https://svn.atlassian.com/svn/public/contrib/tutorials/web-panel-renderer/trunk" class="external-link">check it out from Subversion</a>.

  

##### RELATED TOPICS

[Web Panel Plugin Module](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Web+Panel+Plugin+Module)  
[Plugin Modules](/server/framework/atlassian-sdk/plugin-modules)






























