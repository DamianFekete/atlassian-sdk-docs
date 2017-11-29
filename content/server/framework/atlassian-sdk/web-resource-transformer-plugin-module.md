---
aliases:
- /server/framework/atlassian-sdk/web-resource-transformer-plugin-module-852002.html
- /server/framework/atlassian-sdk/web-resource-transformer-plugin-module-852002.md
category: reference
confluence_id: 852002
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852002
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852002
legacy_url: https://developer.atlassian.com/docs/getting-started/plugin-modules/web-resource-transformer-plugin-module
new_url: /server/framework/atlassian-sdk/web-resource-transformer-plugin-module
platform: server
product: atlassian-sdk
subcategory: modules
title: Web Resource Transformer plugin module
---
# Web Resource Transformer plugin module

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

Web Resource Transformer plugin modules allow you to manipulate static web resources before they are batched and delivered to the browser. This means that you can get past the restrictions of straight JavaScript and CSS, including restrictions like no includes, no external resource support, no CSS variables, only one JS context, and so on.

## Configuration

To use a web resource transformer, you need the following elements in your `atlassian-plugin.xml` file:

-   **The transformer module:** A `<web-resource-transformer>` element, defining the transformer plugin module. This module can be in the same plugin as the web resource, or in a different plugin.
-   **Transformation elements in the web resource module:** A `<transformation>` element and its child `<transformer>` element inside the `<web-resource>` block, making a particular transformer available to the web resource in the plugin.

Below is a description of the attributes and child elements for each of the above elements.

#### Attributes of `web-resource-transformer`

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
<td>The class which implements <a href="http://docs.atlassian.com/atlassian-plugins-webresource/2.6.4/atlassian-plugins-webresource/apidocs/com/atlassian/plugin/webresource/transformer/WebResourceTransformer.html" class="external-link">com.atlassian.plugin.webresource.transformer.WebResourceTransformer</a>. This class is responsible for doing the resource transformation before it is served to the client. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>.</td>
</tr>
<tr class="even">
<td><p>state</p></td>
<td><p>Indicate whether the plugin module should be disabled by default (value='disabled') or enabled by default (value='enabled').</p>
<p><strong>Default:</strong> enabled</p></td>
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
<p>The value of this attribute must match the <code>key</code> attribute of the <code>transformer</code> element in the <code>web-resource</code>.</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module.</p></td>
</tr>
<tr class="even">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false</p></td>
</tr>
</tbody>
</table>

**\*class and key attributes are required**

#### Child Elements of `web-resource-transformer`

|             |                                                                                                                                                             |
|-------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Name        | description                                                                                                                                                 |
| Description | The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body. |

####  Attributes of `transformation`

|             |                                   |
|:------------|:----------------------------------|
| Name\*      | extension                         |
| Description | Defines a transformation process. |

**\*extension attribute is required**

#### Child Elements of `transformation`

|             |                                   |
|:------------|:----------------------------------|
| Name\*      | transformer                       |
| Description | Defines a transformation process. |

**\*transformer element is required**

#### Attributes of `transformer`

|             |                                                                                                       |
|:------------|:------------------------------------------------------------------------------------------------------|
| Name\*      | key                                                                                                   |
| Description | The value of this attribute must match the `key` attribute of the `web-resource-transformer` element. |

**\*key attribute is required**

 

|             |                                                                                                             |
|:------------|:------------------------------------------------------------------------------------------------------------|
| Name        | *(others)*                                                                                                  |
| Description | You can add your own attributes as required, to pass information to your implementation of the transformer. |

####  Child Elements of `transformer`

|             |                                                                                                                 |
|:------------|:----------------------------------------------------------------------------------------------------------------|
| Name        | *(others)*                                                                                                      |
| Description | You can add your own child elements as required, to pass information to your implementation of the transformer. |

##  Example

Here is an example `atlassian-plugin.xml` file containing a web resource and a transformer that turns a static template file into a JavaScript variable. You could use this transformer for common components that need to use client-side templates.

``` xml
<atlassian-plugin name="Hello World Resource" key="example.plugin.helloworld" plugins-version="2">
<plugin-info>
  <description>A web resource module with a transformer</description>
  <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
  <version>1.0</version>
</plugin-info>
<web-resource key="testTemplate">
  <transformation extension="txt">
    <transformer key="template" />
  </transformation>
  <resource type="download" name="testTemplate.js" location="testTemplate.txt" />
  <resource type="download" name="testTemplate.css" />
</web-resource>
<web-resource-transformer key="template" class="com.atlassian.labs.template.TemplateTransformer" />
</atlassian-plugin>
```

The template `testTemplate.txt` file looks like this:

``` text
Hello world "bob"
and 'friends'
```

The JavaScript resulting from the transformation is:

``` javascript
var testTemplate = "Hello world \"bob\"\nand \'friends\'";
```

## Notes

Some information to be aware of when developing or configuring a Web Resource Transformer plugin module:

-   The `<web-resource-transformer>` module can live in the same plugin as the `<web-resource>` module, or in a different module. The transformers are registered globally.
-   You can apply multiple transformers. Any subsequent transformer will process the result of the earlier transformation.
-   You can pass information to the transformer by adding arbitrary attributes and child elements to the `<transformer>` element in the resource.

##### RELATED TOPICS

[Web Resource Plugin Module](/server/framework/atlassian-sdk/web-resource-plugin-module)  
[Plugin Modules](/server/framework/atlassian-sdk/plugin-modules)













































































































































