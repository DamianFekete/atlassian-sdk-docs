---
title: "atlas-create-stash-plugin"
platform: server
product: atlassian-sdk
category: devguide
subcategory: index
date: "2018-07-25"
---
# atlas-create-stash-plugin

{{% warning %}}
Stash has been rebranded. For versions 4.0 and later it is known as Bitbucket Server. If you wish to create a plugin for a version 4.0 or later, please see [atlas-create-bitbucket-plugin](/server/framework/atlas-create-bitbucket-plugin) for the correct command. 
Stash commands will be deprecated with the next major version release for AMPS. 
{{% /warning %}}

This page describes the shell script `atlas-create-stash-plugin`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk). 

{{% note %}}
There is a specific version of this shell script for each Atlassian application. The shell script described on this page is for **Stash**.
{{% /note %}}

## Basic Usage

`atlas-create-stash-plugin [options]` - Creates an example of a Stash plugin, which you can adapt to suit your own plugin's needs. (Runs `mvn stash:create`.) Interpreted parameters: `artifact-id, group-id, version, package, non-interactive` and `maven-plugin-version`.

## Parameters

This shell script supports some interpreted parameters, specified below. All other parameters are passed straight through to Maven.

Explaining the table columns:

-   'Full Parameter' and 'Shortened' - Some parameters allow you to choose a full or a shortened version of the parameter, others just support the full version.
-   'Accepts a Value?' - 'Yes' means that you should specify a value in addition to the parameter, e.g. for the 'version' parameter you should specify the version number. 'No' means that the parameter does not accept a value.

Interpreted parameters:

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 80%" />
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
<td><p>Name of the project. This is an identifier for your plugin. It corresponds to the Maven artifactId. If you do not enter this value, the script will prompt you for it. In this case, the script will fail if you do not provide the <code>artifact-id</code> and <code>group-id</code>.</p>
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
<td><p>If this parameter is present, interactive mode is turned off, so that the script will not prompt the user for input.</p></td>
</tr>
<tr class="even">
<td><p>--maven-plugin-version</p></td>
<td><p>Sets the Maven AMPS plugin version to use (overrides the default)</p>
<p><strong>Shortend: -u [value]</strong></p></td>
</tr>
</tbody>
</table>

***--non-interactive* doesn't accept a value.**

## Getting Help

The shell script will display some help text if you enter one of the following as the first argument:

-   -?
-   -h
-   help
-   -help
-   --help

For example:

``` bash
atlas-create-stash-plugin -?
atlas-create-stash-plugin -help
```

## Examples

Let's assume you want to create a new Stash plugin skeleton. Simply open a command window, go to the directory where you want to create the plugin and type:

``` bash
atlas-create-stash-plugin
```

Let's assume you want to create a new Stash plugin by supplying all the necessary information to the script and allowing the package name to be the same as the group ID. Let's assume you do not want the script to prompt you for information. Type:

``` bash
atlas-create-stash-plugin --artifact-id myfooplugin --group-id com.mycompany.plugins --version 1.0 --non-interactive
```

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)
