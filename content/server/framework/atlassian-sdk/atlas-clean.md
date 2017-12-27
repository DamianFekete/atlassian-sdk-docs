---
aliases:
- /server/framework/atlassian-sdk/atlas-clean-2818352.html
- /server/framework/atlassian-sdk/atlas-clean-2818352.md
category: devguide
confluence_id: 2818352
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818352
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818352
date: '2017-12-08'
guides: guides
legacy_title: atlas-clean
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-clean
---
# atlas-clean

This page describes the shell script `atlas-clean`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

## Basic Usage

`atlas-clean [options]` - Removes files from the project directory, that were generated during the build. (Runs `mvn clean`.) Passes all parameters straight through to Maven.

## Parameters

This shell script is a Maven wrapper script. All parameters are passed straight through to Maven.

## Getting Help

The shell script will display some help text if you enter one of the following as the first argument:

-   -?
-   -h
-   help
-   -help
-   --help

For example:

``` bash
atlas-clean -?
atlas-clean -help
```

## Examples

Let's assume that you want to use a specific version of your plugin's host application. You can specify the version of the host application to use as a parameter of your `atlas-run` command. If you have already used a different version of the same application, you will need to clear the previous version of the host application from your build output directory.

For example, let's assume that you want to use version 3.1 of your host application (e.g. Confluence):

1.  Run `atlas-clean`.
2.  Run `atlas-run -v 3.1`

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)  
[Getting Started](/server/framework/atlassian-sdk/index)
