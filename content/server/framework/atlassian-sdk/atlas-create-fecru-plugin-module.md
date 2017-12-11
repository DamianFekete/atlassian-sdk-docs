---
aliases:
- /server/framework/atlassian-sdk/atlas-create-fecru-plugin-module-8945893.html
- /server/framework/atlassian-sdk/atlas-create-fecru-plugin-module-8945893.md
category: devguide
confluence_id: 8945893
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8945893
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8945893
date: '2017-12-11'
guides: guides
legacy_title: atlas-create-fecru-plugin-module
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-create-fecru-plugin-module
---
# atlas-create-fecru-plugin-module

This page describes the shell script `atlas-create-fecru-plugin-module`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).  

NOTE: There is a specific version of this shell script for each Atlassian application. The shell script described on this page is for **FishEye and Crucible**.

## Basic Usage

`atlas-create-fecru-plugin-module [options]` - Prompts you for plugin module type and related details, then creates an example of a FishEye/Crucible plugin module that you can adapt to suit your own plugin's needs. (Runs `mvn fecru:create-plugin-module`.) Passes all parameters straight through to Maven.

The script will automatically add the changes to your `atlassian-plugin.xml` and generate the appropriate Java code.

## Parameters

This shell script is a Maven wrapper script. All parameters are passed straight through to Maven.

## Supported plugin module types

The plugin module generation scripts are still under development. Currently, only the JIRA script has the full set of modules. All other products contain the applicable common modules, such as REST, web item and servlet. See the list of [common modules in the Atlassian Plugin Framework](/server/framework/atlassian-sdk/plugin-modules).

## Getting Help

The shell script will display some help text if you enter one of the following as the first argument:

-   -?
-   -h
-   help
-   -help
-   --help

For example:

``` bash
atlas-create-fecru-plugin-module -?
atlas-create-fecru-plugin-module -help
```

## Examples

Let's assume you want to add a new plugin module to your existing FishEye/Crucible plugin.

1.  Create your plugin (`atlas-create-fecru-plugin`) and install it into the application (`atlas-run`) as usual.
2.  Go to the root directory for your plugin (where the `pom.xml` is located).
3.  Run this command:

    ``` bash
    atlas-create-fecru-plugin-module
    ```

4.  Follow the prompts to specify the type of plugin module that you want, and further information required to create the basic module.
5.  The script will added the required module to your `atlassian-plugin.xml` file.
6.  Where relevant, the script will add the Java classes to your plugin's .java file too.

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)





























































































































































































































































































