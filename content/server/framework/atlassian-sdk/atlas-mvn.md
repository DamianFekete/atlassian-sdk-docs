---
aliases:
- /server/framework/atlassian-sdk/atlas-mvn-2818341.html
- /server/framework/atlassian-sdk/atlas-mvn-2818341.md
category: devguide
confluence_id: 2818341
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818341
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818341
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference/atlas-mvn
new_url: /server/framework/atlassian-sdk/atlas-mvn
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-mvn
---
# atlas-mvn

This page describes the shell script `atlas-mvn`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

{{% tip %}}

Do not use your local Maven

When running Maven commands against your project, make sure that you use the version of Maven bundled with the Atlassian Plugin SDK. This is important if you have a local version of Maven installed, as well as the Atlassian Plugin SDK. The simplest way is to use the [atlas-mvn](https://developer.atlassian.com/display/DOCS/atlas-mvn) wrapper command instead of `mvn`. Another way is to [put the bundled Maven on your path](https://developer.atlassian.com/display/DOCS/Verifying+Your+Maven+Settings).

{{% /tip %}}

 

## Basic Usage

 `atlas-mvn [options]` - Allows you to execute any Maven command using the version of Maven bundled with your Atlassian Plugin SDK. (Runs `mvn`.) Passes all parameters straight through to Maven.

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
atlas-mvn -?
atlas-mvn -help
```

## Examples

Run the following command to compile the Java JUnit test classes:

``` bash
atlas-mvn test-compile 
```

Run the following command to get help on the Maven `test-compile` goal:

``` bash
atlas-mvn test-compile --help
```

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)
























































































































