---
aliases:
- /server/framework/atlassian-sdk/atlas-package-2818351.html
- /server/framework/atlassian-sdk/atlas-package-2818351.md
category: devguide
confluence_id: 2818351
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818351
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818351
date: '2017-12-08'
guides: guides
legacy_title: atlas-package
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-package
---
# atlas-package

This page describes the shell script `atlas-package`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

 

## Basic Usage

 `atlas-package[options]` - Packages the plugin artifacts and produces the JAR. (Runs `mvn package`.) Passes all parameters straight through to Maven.

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
atlas-package -?
atlas-package -help
```

Run the following command to see all options provided by `mvn package`:

``` bash
atlas-mvn package --help
```

## Examples

Run the following command to produce your JAR:

``` bash
atlas-package
```

Run the following command to produce your JAR without failing the build, even if there are errors

``` bash
atlas-package --fail-never
```










































































































































































































































