---
aliases:
- /server/framework/atlassian-sdk/atlas-create-crowd-plugin-2818340.html
- /server/framework/atlassian-sdk/atlas-create-crowd-plugin-2818340.md
category: devguide
confluence_id: 2818340
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818340
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818340
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: Atlas Create Crowd Plugin 2818340
---
# atlas-create-crowd-plugin

This page describes the shell script `atlas-create-crowd-plugin`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

NOTE: There is a specific version of this shell script for each Atlassian application. The shell script described on this page is for **Crowd**.

## Basic Usage

 `atlas-create-crowd-plugin [options]` - Creates an example of a Crowd plugin, which you can adapt to suit your own plugin's needs. (Runs `mvn crowd:create`.) Interpreted parameters: `artifact-id, group-id, version, package, non-interactive`.

## Parameters

This shell script supports some interpreted parameters, specified below. All other parameters are passed straight through to Maven.

Explaining the table columns:

-   'Full Parameter' and 'Shortened' - Some parameters allow you to choose a full or a shortened version of the parameter, others just support the full version.
-   'Accepts a Value?' - 'Yes' means that you should specify a value in addition to the parameter, e.g. for the 'version' parameter you should specify the version number. 'No' means that the parameter does not accept a value.

Interpreted parameters:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Full Parameter</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>--artifact-id</p></td>
<td><p>Name of the project. This is an identifier for your plugin. It corresponds to the Maven artifactId. If you do not enter this value, the script will prompt you for it.</p>
<p><strong>Shortened: -a</strong></p></td>
</tr>
<tr class="even">
<td><p>--group-id</p></td>
<td><p>Identifier for the logical group of artifacts associated with the project. Will be used as the default value for <code>package</code>. Corresponds to the Maven groupId. If you do not enter this value, the script will prompt you for it.</p>
<p><strong>Shortened: -g</strong></p></td>
</tr>
<tr class="odd">
<td><p>--version</p></td>
<td><p>Version of your plugin. Default is <code>1.0-SNAPSHOT</code>. If you do not enter this value, the script will prompt you for it.</p>
<p><strong>Shortened: -v</strong></p></td>
</tr>
<tr class="even">
<td><p>--package</p></td>
<td><p>Name of the Java package that will contain the plugin source code. Default is the value given for <code>group-id</code>.</p>
<p><strong>Shortened: -p</strong></p></td>
</tr>
<tr class="odd">
<td><p>--non-interactive</p></td>
<td><p>If this parameter is present, interactive mode is turned off, so that the script will not prompt the user for input. In this case, the script will fail if you do not provide the <code>artifact-id</code> and <code>group-id</code>.</p></td>
</tr>
</tbody>
</table>

***--non-interactive* doesn't accept a value.**

## Getting Help

The shell script will display some help text if you enter one of the following as the first argument:

-   -?
-   -h
-   help
-   -help
-   --help

For example:

``` bash
atlas-create-crowd-plugin -?
atlas-create-crowd-plugin -help
```

## Examples

Let's assume you want to create a new Crowd plugin skeleton. Simply open a command window, go to the directory where you want to create the plugin and type:

``` bash
atlas-create-crowd-plugin
```

Let's assume you want to create a new Crowd plugin by supplying all the necessary information to the script and allowing the package name to be the same as the group ID. Let's assume you do not want the script to prompt you for information. Type:

``` bash
atlas-create-crowd-plugin --artifact-id myfooplugin --group-id com.mycompany.plugins --version 1.0 --non-interactive
```

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)  
<a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Developing+your+Plugin+using+the+Atlassian+Plugin+SDK&amp;linkCreation=true&amp;fromPageId=2818340" class="createlink">Developing your Plugin using the Atlassian Plugin SDK</a>






































































































































