---
title: Atlas Release 2818354
aliases:
    - /server/framework/atlassian-sdk/atlas-release-2818354.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818354
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818354
confluence_id: 2818354
platform:
product:
category:
subcategory:
---
# atlas-release

This page describes the shell script `atlas-release`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk-2818723.html).

 

## Basic Usage

`atlas-release [options]` - Performs a release of the current plugin. (Runs `mvn release:prepare release:perform`.) Passes all parameters straight through to Maven.

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

``` javascript
atlas-release -?
atlas-release -help
```

Run the following command to see all options provided by `mvn release`:

``` javascript
atlas-mvn release --help
```

## Examples

Run the following command to release your plugin:

``` javascript
atlas-release
```

Run the following command to release your plugin without failing the build, even if there are errors

``` javascript
atlas-release --fail-never
```

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk-2818723.html)  
<a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Developing+your+Plugin+using+the+Atlassian+Plugin+SDK&amp;linkCreation=true&amp;fromPageId=2818354" class="createlink">Developing your Plugin using the Atlassian Plugin SDK</a>

























