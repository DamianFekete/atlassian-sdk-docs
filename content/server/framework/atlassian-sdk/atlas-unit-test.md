---
aliases:
- /server/framework/atlassian-sdk/atlas-unit-test-2818360.html
- /server/framework/atlassian-sdk/atlas-unit-test-2818360.md
category: devguide
confluence_id: 2818360
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818360
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818360
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: Atlas Unit Test 2818360
---
# atlas-unit-test

This page describes the shell script `atlas-unit-test`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

## Basic Usage

 `atlas-unit-test [options]` - Runs the unit tests for your plugin. (Runs `mvn test`.) Passes all parameters straight through to Maven.

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
atlas-unit-test -?
atlas-unit-test -help
```

Run the following command to see all options provided by `mvn test`:

``` bash
atlas-mvn test --help
```

## Examples

Run the following command to run your unit tests:

``` bash
atlas-unit-test
```

Run the following command to run your unit tests without failing the build, even if there are errors:

``` bash
atlas-unit-test --fail-never
```

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)  
[Plugin Testing Resources and Discussion](https://developer.atlassian.com/pages/viewpage.action?pageId=2818627)

















































































































