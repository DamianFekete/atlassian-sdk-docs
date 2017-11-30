---
aliases:
- /server/framework/atlassian-sdk/configuring-the-plugin-descriptor-852008.html
- /server/framework/atlassian-sdk/configuring-the-plugin-descriptor-852008.md
category: devguide
confluence_id: 852008
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852008
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852008
legacy_url: https://developer.atlassian.com/docs/getting-started/configuring-the-plugin-descriptor
new_url: /server/framework/atlassian-sdk/configuring-the-plugin-descriptor
platform: server
product: atlassian-sdk
subcategory: intro
title: Configuring the plugin descriptor
---
# Configuring the plugin descriptor

This page describes the plugin descriptor, the XML file that describes the plugin to the Atlassian application. **   
**

 

## About the Plugin Descriptor

Every plugin must have a plugin descriptor file. The file, named `atlassian-plugin.xml`, describes the plugin to the Atlassian application framework.

The Atlassian Plugin SDK generates the plugin descriptor for you. When you add a module to your project with the `atlas-create-product-plugin-module` script, the SDK accordingly updates the descriptor file based on the new module.

While the SDK generates and maintains the plugin descriptor file for you, for most projects, you will need to modify the descriptor file manually at some point. For one, depending on the nature of your plugin, the descriptor may contain strings used in the UI representation of your plugin that you may want to modify. In any case, it's a good idea to understand what's in the plugin descriptor and how the SDK generates it.

The plugin descriptor file resides in the following directory in your project home:

`<project_home>/src/main/resources`

When you compile the plugin, the SDK copies the file to the root directory in the plugin archive. 

## Example Plugin Descriptor

The following is the plugin descriptor file that the SDK generates for a JIRA plugin.

``` javascript
<atlassian-plugin key="${project.groupId}.${project.artifactId}" name="${project.name}" plugins-version="2">
    <plugin-info>
        <description>${project.description}</description>
        <version>${project.version}</version>
        <vendor name="${project.organization.name}" url="${project.organization.url}" />
    </plugin-info>
</atlassian-plugin>
```

The descriptor doesn't tell us much, yet. Most of the element and attribute values [contain variables](#contain-variables). And the plugin project doesn't have modules yet, so there isn't much to the descriptor. But you can still start up JIRA and see the plugin in the administration console. It appears as a user-installed add-on in the Manage Add-ons page. 

Once we add a module to the plugin, such as a custom field to the JIRA plugin project, the plugin descriptor starts to take shape.

``` javascript
<?xml version="1.0" encoding="UTF-8"?>
<atlassian-plugin key="${project.groupId}.${project.artifactId}" name="${project.name}" plugins-version="2">
  <plugin-info>
    <description>${project.description}</description>
    <version>${project.version}</version>
    <vendor name="${project.organization.name}" url="${project.organization.url}"/>
  </plugin-info>
  <resource type="i18n" name="i18n" location="com.atlassian.samples.tutorial.myJiraPlugin"/>
  <customfield-type name="My Custom Field" i18n-name-key="my-custom-field.name" key="my-custom-field" 
                                     class="com.atlassian.samples.tutorial.jira.customfields.MyCustomField">
    <description key="my-custom-field.description">The My Custom Field Plugin</description>
    <resource name="view" type="velocity" location="/templates/customfields/my-custom-field/view.vm"/>
    <resource name="edit" type="velocity" location="/templates/customfields/my-custom-field/edit.vm"/>
  </customfield-type>
</atlassian-plugin>
```

While the details are handled by the SDK, it's worth looking at some of the features of the descriptor:

-   The `customfield-type` element is a plugin module element. The elements you can use vary depending on the target application for the plugin. For instance, the `customfield-type` element applies to JIRA plugins. For information on common plugin modules, see [Plugin Module Types](https://developer.atlassian.com/x/qAAN).
-   Each plugin has a **plugin key** which must be unique for plugins in the application.It is made up of the group ID and artifact ID. Since the plugin key must be unique, we suggest using the Java convention of reversing your domain name for the group ID to ensure that your key is unique. The plugin key must be in lower case in the descriptor.
-   The **complete module key** is made up of the concatenated plugin key and module key. So a module with key `fred` in a plugin of `com.example.modules` will have a complete key of `com.example.modules:fred`.
-   All plugin modules have a **class** attribute, which indicates which Java class should be instantiated when loading the module. When you create the resource with the SDK, it generates the starter class file for you.

## Adding Resource Declarations** **

Resources are non-Java files used by the plugin. For example, a resource may be:

-   A velocity file used to generate HTML for a macro or layout plugin module
-   A CSS file required by a theme layout plugin module
-   An image referenced from within a layout plugin module
-   A macro help file
-   A localisation property file

The SDK adds the resource definitions to your plugin descriptor. The declarations take the following form:

``` javascript
<resource type="velocity" name="template" location="com/example/plugin/template.vm"/>
<resource type="i18n" name="i18n" location="resources/exampleplugin" />
<resource type="download" name="style.css" location="com/example/plugin/style.css">
   <property key="content-type" value="text/css"/>
</resource>
```

As shown by the examples:

-   The `type` and `name` of the resource tells the module how the resource can be used. A module can look for resources of a certain type or name; for example, the `layout` plugin required that its help file is a file of type `velocity` and name `help`.
-   The **location** of a resource tells the plugin where the resource can be found in the JAR file (resources are loaded by Java's classpath resource-loader). The full path to the file (without a leading slash) is required.
-   The simplest kind of resource, supported with all plugin module types, is of type `download`, which makes a resource available for download from the application at a particular URL. See [Downloadable Plugin Resources](https://developer.atlassian.com/display/CONFDEV/Adding+Plugin+and+Module+Resources).

## Adding Configuration Pages

Plugins can specify internal links within the application to configure themselves. This is useful where your plugin requires any configuration or user specific settings to work. For example, the <a href="https://marketplace.atlassian.com/plugins/com.atlassian.confluence.ext.gmaps" class="external-link">Google Maps plugin</a> requires the administrator to configure a Google API Key from Google (which needs to be configured on each server).

-   Configuration links will *most often* point to XWork plugin modules within the plugin itself.
-   Configuration links can be provided for a whole plugin or for any module within a plugin.
-   Configuration links are relative to the application.

For the entire plugin, place a single `param` element with the name `configure.url` within the `plugin-info` element at the top of the plugin descriptor:

``` javascript
<plugin-info>
    <description>A macro which displays Google maps within a Confluence page.</description>
    <vendor name="Atlassian" url="http://www.atlassian.com/"/>
    <version>0.1</version>
    <param name="configure.url">/admin/plugins/gmaps/configurePlugin.action</param>
</plugin-info>
```

You can specify a configuration page for an individual module by placing the same `param` element with the name `configure.url` within the `descriptor` element for that module:

``` javascript
<macro name="gmap" class="com.atlassian.confluence.ext.gmaps.GmapsMacro" key="gmap">
    <description>The individual map macro.</description>
    <param name="configure.url">/admin/plugins/gmaps/configureMacro.action</param>
</macro>
```

## Keeping the POM and plugin descriptor in sync

The POM and plugin descriptor files both define certain common values for the plugin project, such as its project name and the organisation name of the plugin creator.

Instead of duplicating the values in both files, the Atlassian SDK uses the <a href="http://maven.apache.org/shared/maven-filtering/" class="external-link">Maven filtering</a> utility. The utility keeps common values synchronized, so you don't have to add or modify the properties in two places. You only need to change the value in the POM file to have it propagated to the plugin descriptor at compilation time.

![](/server/framework/atlassian-sdk/images/xmlfilemappings.png)

The plugin descriptor file already contains variables for common values, such as for the project name and description. But you can add more variables or change the default, if needed, by adding them to the plugin descriptor file. To add a variable to a value in the POM, wrap the element path for the POM value in ${...} delimiters, in the following form:

` ${element.subelement}`

##### RELATED TOPICS

-   [Marking Packages as Optional Imports](/server/framework/atlassian-sdk/marking-packages-as-optional-imports-852102.html)
-   [atlassian-plugin.xml Element Reference](/server/framework/atlassian-sdk/atlassian-plugin-xml-element-reference)


















































































