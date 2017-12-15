---
aliases:
- /server/framework/atlassian-sdk/atlas-update-13633056.html
- /server/framework/atlassian-sdk/atlas-update-13633056.md
category: devguide
confluence_id: 13633056
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=13633056
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=13633056
date: '2017-12-08'
guides: guides
legacy_title: atlas-update
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-update
---
# atlas-update

This page describes the shell script `atlas-update`, part of the Atlassian Plugin SDK.

## Basic Usage

 `atlas-update [options]` - Updates the Atlassian Plugin SDK.

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
atlas-update -?
atlas-update -help
```

### Examples

Run the following command to determine if an update your SDK:

``` bash
atlas-update
```
