---
title: Content for Resource Definition 852006
aliases:
    - /server/framework/atlassian-sdk/-content-for-resource-definition-852006.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852006
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852006
confluence_id: 852006
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Resource Definition

## Purpose of a Resource

A 'resource' is a non-Java file that a plugin may need in order to operate. Examples of possible resources might be:

-   A Velocity file used to generate HTML for a macro or layout plugin module in Confluence.
-   A CSS file required by a theme layout plugin module.
-   An image referenced from within a layout plugin module.
-   A macro help file.
-   A localisation property file.

Resource definitions can be either a part of the plugin, or part of a particular plugin module.

## Example of a Resource Definition

Here is a sample resource definition:

``` xml
<!-- A resource has a type, a name and a location. The resource definition maps -->
<!-- some arbitrary resource name to where that resource would be located in    -->
<!-- the server's classpath -->
<resource type="velocity" name="template" location="com/example/plugin/template.vm"/>

<!-- For the localisation property file below, it must be named exampleplugin.properties -->
<!-- located under the resources folder -->
<resource type="i18n" name="i18n" location="exampleplugin" />

<!-- Resources may contain arbitrary key/value pairs -->
<resource type="download" name="style.css" location="com/example/plugin/style.css">
   <property key="content-type" value="text/css"/>
</resource>
```

## Contents of the Resource Definition

A resource has a name, a type and a location. The resource definition maps an arbitrary resource name to the location of that resource in the server's classpath.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Element &amp; Attribute</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>&lt;resource&gt;</p></td>
<td><p>This block defines the resource. For example: <code>&lt;resource type=&quot;velocity&quot; name=&quot;template&quot; location=&quot;com/example/plugin/template.vm&quot;/&gt;</code></p></td>
</tr>
<tr class="even">
<td><p>&lt;resource&gt;</p>
<p>name</p></td>
<td><p>The name of the resource defines how the plugin module can locate a particular resource. Must be specified if 'namePattern' is not. If your location parameter points to a directory rather than a single resource, you should specify the name with a trailing '/'. For example: <code>&lt;resource type=&quot;download&quot; name=&quot;myimages/&quot; location=&quot;com/example/plugin/myimages&quot;/&gt;</code><br />
<br />
Note that for css/javascript resources, they must have the appropriate file extension in the name i.e. <code>.css, .js</code></p></td>
</tr>
<tr class="odd">
<td><p>&lt;resource&gt;</p>
<p>namePattern</p></td>
<td><p>The pattern to use when loading a directory resource.</p></td>
</tr>
<tr class="even">
<td><p>&lt;resource&gt;</p>
<p>type</p></td>
<td><p>The type of a resource tells the module how that resource can be used. The values allowed are different for each application.<br />
A module can look for resources of a certain type or name. For example, a <code>layout</code> plugin requires that its help file is a file of type <code>velocity</code> and name <code>help</code>.<br />
Refer to the examples of resource types below.</p></td>
</tr>
<tr class="odd">
<td><p>&lt;resource&gt;</p>
<p>location</p></td>
<td><p>The location of a resource tells the plugin where the resource can be found in the jar file. (Resources are loaded by Java's classpath resource loader.)</p>
<ul>
<li>The full path to the file (without a leading slash) is required.</li>
<li>Must end in a '/' when using the 'namePattern' attribute to load multiple resources in a directory.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>&lt;property&gt;</p>
<p>key/value</p></td>
<td><p>Resources may contain arbitrary key/value pairs. For example: <code>&lt;property key=&quot;content-type&quot; value=&quot;text/css&quot;/&gt;</code></p></td>
</tr>
<tr class="odd">
<td><p>&lt;param&gt;</p>
<p>name/value</p></td>
<td><p>Resources may contain arbitrary name/value pairs. For example: <code>&lt;param name=&quot;content-type&quot; value=&quot;image/gif&quot;/&gt;</code>. Refer to the list of values for the param element below</p></td>
</tr>
</tbody>
</table>

## Example of Resource Type: Downloadable Plugin Resources

The simplest kind of resource, supported with all plugin module types, is of type `download`, which makes a resource available for download from the application at a particular URL.

``` xml
<resource type="download" name="aimon.gif" location="templates/extra/impresence/aimon.gif">
   <param name="content-type" value="image/gif"/>
</resource>
```

## Example of Resource Type: Stylesheet referring to Images

Stylesheets for your plugin may often refer to images also in your plugin. In which case you would have to make both the stylesheet and image(s) downloadable.

``` xml
<resource type="download" name="my-images/" location="com/example/plugin/myimages"/>
<resource type="download" name="my-style.css" location="com/example/plugin/my-style.css"/>
```

Note: If you have multiple stylesheets and javascript resources defined, you should put the resource defintions in a [Web Resource Module.](/server/framework/atlassian-sdk/web-resource-plugin-module)

To refer to your plugin images in a stylesheet, use a relative path based on the resource name defined for the image (which is 'my-images' in this case).

**my-style.css**

``` css
 .my-class {
   background-image: url(my-images/mypicture.gif);
}
```

To reference images already available in an application, you will need to go up three parent directories like so:

``` css
.my-class {
   background-image: url(../../../images/icons/confluence-logo.gif);
}
```

## Values for Param Element

These are the common name/value pairs supported by the `<param>` element.

**Name &** **Value:** content-type \| image/gif

**Description:** Specify a MIME content type. 

------------------------------------------------------------------------

**Name & Value:** media \| print

**Description: ** 

Declare the media type for CSS resources. This is supported by [Web Resource plugin modules](/server/framework/atlassian-sdk/web-resource-plugin-module).  
For example, requesting this resource will insert a `<link>` in the HTML header, with a media value of 'print': 

``` xml
<web-resource key="mechanical-parts" name="Mechanical Parts"
    i18n-name-key="com.example.confluence.plugin.special.mechanical.parts.name">
    <resource type="download" name="sprockets.css" location="styles/sprockets.css">
        <param name="media" value="print"/>
    </resource>
</web-resource>
```

 

**Name & Value: **ieonly \| true 

**Description: ** 

Specify that the resource should be wrapped in an <a href="http://www.quirksmode.org/css/condcom.html" class="external-link">Internet Explorer conditional comment</a>. This is supported by [Web Resource plugin modules](/server/framework/atlassian-sdk/web-resource-plugin-module).  
For example, the web resource declaration below says that the resource should be wrapped in an Internet Explorer conditional comment, which means it will only be used by Internet Explorer. This is useful for IE-specific styling to work around browser bugs. 

``` xml
<web-resource key="mechanical-parts" name="Mechanical Parts"
    i18n-name-key="com.example.confluence.plugin.special.mechanical.parts.name">
    <resource type="download" name="sprockets-ie.css" location="styles/sprockets.css">
        <param name="ieonly" value="true"/>
    </resource>
</web-resource>
```

The HTML output when this resource is included will be something like this: 

``` xml
<!--[if IE]>
<link type="text/css" rel="stylesheet" media="all"
    href="/s/1418/13/1.0/_/download/resources/plugin.example:mechanical-parts/sprocket-ie.css" />
<![endif]-->
```

The `ieonly` parameter also works for JavaScript resources. 

------------------------------------------------------------------------

**Name & Value: **conditionalComment \| lt IE 9 

**Description:**  

Specify that the resource should be wrapped in an <a href="http://www.quirksmode.org/css/condcom.html" class="external-link">Internet Explorer conditional comment</a>, and should be used when targeting specific versions of Internet Explorer. This is supported by [Web Resource plugin modules](/server/framework/atlassian-sdk/web-resource-plugin-module).  
For example, the web resource declaration below says that the resource should be wrapped in an Internet Explorer conditional comment, which means it will only be used by versions of Internet Explorer less than 9. This is useful for IE version-specific styling to work around browser bugs. 

``` xml
<web-resource key="mechanical-parts" name="Mechanical Parts"
    i18n-name-key="com.example.confluence.plugin.special.mechanical.parts.name">
    <resource type="download" name="sprockets-lt-ie9.css" location="styles/sprockets-lt-ie9.css">
        <param name="conditionalComment" value="lt IE 9"/>
    </resource>
</web-resource>
```

The HTML output when this resource is included will be something like this: 

``` xml
<!--[if lt IE 9]>
<link type="text/css" rel="stylesheet" media="all"
    href="/s/1418/13/1.0/_/download/resources/plugin.example:mechanical-parts/sprocket-lt-ie9.css" />
<![endif]-->
```

The `conditionalComment` parameter also works for JavaScript resources. 

------------------------------------------------------------------------

**Name &** **Value (Example):** title \| (Your title) 

**Description:** The value given here will form the title attribute of the CSS `<link>` tag.

 





















































































































































































































































