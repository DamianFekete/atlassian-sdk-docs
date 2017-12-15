---
aliases:
- /server/framework/atlassian-sdk/-content-for-plugin-descriptor-852011.html
- /server/framework/atlassian-sdk/-content-for-plugin-descriptor-852011.md
category: devguide
confluence_id: 852011
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852011
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852011
date: '2017-12-08'
legacy_title: _Content for Plugin Descriptor
platform: server
product: atlassian-sdk
subcategory: other
title: _Content for Plugin Descriptor
---
# \_Content for Plugin Descriptor

Every plugin requires an `atlassian-plugin.xml` file. This is a single file also known as the *plugin descriptor*. The plugin descriptor is an XML file that describes a plugin and the modules contained within it for the host application. In a plugin project, the file is resides in the `resources` directory. In a plugin submission, the descriptor is located at the root of the plugin's jar file.

The following is a basic descriptor file:

``` xml
<!-- Every plugin must have a key, which identifies the plugin uniquely to the system -->
<!-- and a name, which is used to display the plugin in menus. -->
<atlassian-plugin key="com.atlassian.confluence.plugins.example" name="The Customizer" plugins-version="2">

  <!-- The plugin info block allows you to provide more information about your plugin -->
  <plugin-info>
    <description>
      A sample plugin for demonstrating the file format.
    </description>
    <!-- This version is displayed in the application's Plugin Manager. -->
    <version>1.0</version>
    <!-- The versions of the application this plugin is compatible with -->
    <application-version min="1.3" max="1.3"/>
    <vendor name="Atlassian Software Systems Pty Ltd" url="http://www.atlassian.com/"/>
    <!-- The location of any plugin configuration (optional) -->
    <param name="configure.url">/admin/plugins/example/configurePlugin.action</param>
    <!-- Specifically declare bundle instructions (optional) -->    
    <bundle-instructions>
      <Export-Package>my.external.pkg</Export-Package>
      <Import-Package>com.mylibrary,*;resolution:=optional</Import-Package>
    </bundle-instructions>
  </plugin-info>

  <!-- Here is where you define your modules. The code you use        -->
  <!-- to define a module depends on the module itself. This is just  -->
  <!-- a sample, which will not load if installed into Confluence     -->

  <!-- Modules must have a key that is unique within the plugin, a name -->
  <!-- and an implementing class. -->
  <examplemodule key="module1" name="Example Module" class="com.atlassian.confluence.plugins.example.ExampleModule">
    <!-- All modules can optionally have a description -->
    <description>An example module</description>
  </examplemodule>
</atlassian-plugin>
```

The following sections describe the basic elements in the descriptor XML file.

## `atlassian-plugin` element

The root element for your plugin descriptor. For example, the plugin descriptor file should have this structure:

``` xml
<atlassian-plugin key="com.atlassian.confluence.plugins.example" name="The Customizer" plugins-version="2">
    <!-- ... -->
</atlassian-plugin>
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Attribute</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>key</code></p></td>
<td><p>A String identifying the plugin module. This attribute is required and must be unique within the plugin. You should use the reverse domain name notation to ensure your key is unique. In other contexts, you may need to uniquely identify a module. You should use the complete module key.<br />
<br />
By default, the SDK generation commands sets the key for you by referencing and concatenating the <code>groupId</code> and <code>artifactId</code> from the <code>pom.xml</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>name</code></p></td>
<td><p>This is a human-readable name, used for display in menus within the application. By default, the SDK generation commands sets the key for you by referencing the add-on <code>name</code> from the <code>pom.xml</code>. You should not use the words 'plugin' or 'add-on' in this value.</p></td>
</tr>
<tr class="odd">
<td><p><code>state</code></p></td>
<td><p>This is <code>enabled</code> by default. To disable the entire plugin, specify <code>disabled</code>.</p></td>
</tr>
<tr class="even">
<td><p><code>plugins-version</code></p></td>
<td><p>To create an OSGi plugin, use <code>plugins-version=&quot;2&quot;</code>.<br />
NOTE: The attribute <code>pluginsVersion</code> was <strong>deprecated</strong> in version 2.1 of the plugin framework.</p></td>
</tr>
<tr class="odd">
<td><p><code>i18n-name-key</code></p></td>
<td><p>The localization key for the human-readable name of the plugin module.</p></td>
</tr>
<tr class="even">
<td><p><code>class</code></p></td>
<td><p>The class that implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin.</p></td>
</tr>
<tr class="odd">
<td><p><code>system</code></p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p></td>
</tr>
</tbody>
</table>

## `plugin-info` Element

Contains plugin information displayed by the application for administrators, plugin parameters, and OSGi bundle instructions. Its parent element is `<atlassian-plugin>`, and it supports several nested elements.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Nested element</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>&lt;description&gt;</code></p></td>
<td><p>A human-readable description of your plugin.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;version&gt;</code></p></td>
<td><p>The version of your plugin. This number is displayed in the application's plugin manager.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;java-version</code></p></td>
<td><p>The Java version required for this plugin module. This is an optional value. It is not used consistently among the host applications.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;application-version&gt;</code></p></td>
<td><p>Supply the versions of the application that will support your plugin. Deprecated.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;vendor&gt;</code></p></td>
<td><p>Supply information about the developer of the plugin.</p></td>
</tr>
<tr class="even">
<td><p><code>&lt;param&gt;</code></p></td>
<td><p>Supply parameter values if required by your plugin.</p></td>
</tr>
<tr class="odd">
<td><p><code>&lt;bundle-instructions&gt;</code></p></td>
<td><p>Declare plugin dependencies and shorten your export package lists by specifying OSGi bundle instructions directly in the plugin XML (OSGi plugins only).</p></td>
</tr>
</tbody>
</table>

These nested elements are described in more detail below.

### `description` element

Describes your plugin. Its parent element is `<plugin-info>`.

``` xml
<atlassian-plugin ...>
    <plugin-info>
        <!-- ... -->
        <description>New macros for integration with Acme Corp. web services</description>
    </plugin-info>
</atlassian-plugin>
```

### `version` element

The current version of your plugin. Its parent element is `<plugin-info>`. The UPM sometimes compares the plugin version value within an application to determine the newer version, particularly when performing automated upgrades. Versions are compared by splitting the version number into components and comparing them numerically first and alphabetically second.

Following are some sample version numbers in ascending order: 0.99, 1.0, 1.0.1-alpha, 1.0.1-beta, 1.0.1-beta2, 1.0.1, 1.0.1.0, 1.1, 1.2, 1.10, 2.0.

``` xml
<atlassian-plugin ...>
    <plugin-info>
        <!-- ... -->
        <version>1.2</version>
    </plugin-info>
</atlassian-plugin>
```

### `application-version` element

{{% note %}}

Deprecated since Atlassian Plugin Framework 2.2

 

{{% /note %}}

Describe which versions of the host application are compatible with this plugin. Enforcement of this property varies between applications: some applications strictly enforce compatibility, while others ignore the value.

Its parent element is `<plugin-info>`.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Attribute name</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>min</code></p></td>
<td><p>Lowest application version that your plugin is compatible with.</p></td>
</tr>
<tr class="even">
<td><p><code>max</code></p></td>
<td><p>Highest application version that your plugin is compatible with.</p></td>
</tr>
</tbody>
</table>

``` xml
<atlassian-plugin ...>
    <plugin-info>
        <!-- ... -->
        <application-version min="2.0" max="2.7" />
    </plugin-info>
</atlassian-plugin>
```

### `vendor` element

The plugin vendor. Provides a link in the plugin administration screens. Its parent element is `<plugin-info>`.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Attribute name</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>name</code></p></td>
<td><p>Supply your name or the name of the company you work for.</p></td>
</tr>
<tr class="even">
<td><p><code>url</code></p></td>
<td><p>Supply a web site address.</p></td>
</tr>
</tbody>
</table>

``` xml
<atlassian-plugin ...>
    <plugin-info>
        <!-- ... -->
        <vendor name="Acme Systems Ltd" url="http://acme.example.com/" />
    </plugin-info>
</atlassian-plugin>
```

### `param` element

Arbitrary parameters for a plugin. Its parent element is `<plugin-info>`. These can be nested in many other elements. Attribute `name` gives the parameter name. The element's body is its value.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Attribute</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>name</code></p></td>
<td><p>The name of the parameter.</p></td>
</tr>
<tr class="even">
<td><p>(body)</p></td>
<td><p>The value of the parameter.</p></td>
</tr>
</tbody>
</table>

A common example of a `param` element the URL for your plugin's configuration screen. Below is an example.

``` xml
<atlassian-plugin ...>
    <plugin-info>
        <!-- ... -->
        <param name="configure.url">/admin/plugins/example/configurePlugin.action</param>
    </plugin-info>
</atlassian-plugin>
```

### `bundle-instructions` element

This element allows you to declare plugin dependencies and shorten your export package lists by specifying OSGi bundle instructions directly in the plugin XML. The element's parent element is `<plugin-info>`.

``` xml
<atlassian-plugin ...>
    <plugin-info>
        <!-- ... -->
        <bundle-instructions>
          <Export-Package>my.external.pkg</Export-Package>
          <Import-Package>com.mylibrary,*;resolution:=optional</Import-Package>
        </bundle-instructions>
    </plugin-info>
</atlassian-plugin>
```

As seen in the above example, the `bundle-instructions` element allows child elements, including:

-   `<Export-Package>`
-   `<Import-Package>`  
    Alternatively, you can declare these instruction sets inside your `pom.xml` file.

{{% note %}}

Speeding up Plugin Loading

[How to Speed Up Plugin Startup](/server/framework/atlassian-sdk/how-to-speed-up-plugin-startup) contains information on using bundle instructions for speeding plugin start up.

{{% /note %}}

The Atlassian Plugin Framework uses the <a href="http://www.aqute.biz/Code/Bnd" class="external-link">bnd</a> tool to generate OSGi bundles. This tool is available as the <a href="http://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html" class="external-link">Bundle Plugin for Maven</a>. For details of the bnd directives, please refer to the <a href="http://www.aqute.biz/Code/Bnd#directives" class="external-link">bnd documentation</a>.

## Plugin module elements

In the rest of the descriptor XML file, contains any modules that make up your plugin. You can add these modules through the `atlas-`\* commands or manually. The following illustrates the addition of a `web-item` module:

``` xml
<web-item name="Radio Paradise" i18n-name-key="radio-paradise.name" key="radio-paradise" section="client-sites-link/my-section" weight="1000">
    <description key="radio-paradise.description">The Radio Paradise Plugin</description>
    <label key="radio-paradise.label"></label>
    <link linkId="radio-paradise-link">http://www.radioparadise.com</link>
  </web-item>
```

For more information about the modules a plugin can contain, refer to the list of module types for your plugin's host application.
