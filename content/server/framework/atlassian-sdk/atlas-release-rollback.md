---
aliases:
- /server/framework/atlassian-sdk/atlas-release-rollback-2818347.html
- /server/framework/atlassian-sdk/atlas-release-rollback-2818347.md
category: devguide
confluence_id: 2818347
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818347
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818347
date: '2017-12-08'
guides: guides
legacy_title: atlas-release-rollback
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-release-rollback
---
# atlas-release-rollback

This page describes the shell script `atlas-release-rollback`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

## Basic Usage

 `atlas-release-rollback [options]` - Rolls back a release of the current plugin. (Runs `mvn release:rollback`.) Passes all parameters straight through to Maven.

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
atlas-release-rollback -?
atlas-release-rollback -help
```

Run the following command to see all options provided by `mvn release`:

``` bash
atlas-mvn release --help
```

## Examples

Run the following command to roll back a previous release of your plugin:

``` bash
atlas-release-rollback
```

Run the following command to roll back a previous release of your plugin without failing the build, even if there are errors

``` bash
atlas-release-rollback --fail-never
```

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)  
<a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Developing+your+Plugin+using+the+Atlassian+Plugin+SDK&amp;linkCreation=true&amp;fromPageId=2818347" class="createlink">Developing your Plugin using the Atlassian Plugin SDK</a>





















































































































