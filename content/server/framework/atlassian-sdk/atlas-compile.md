---
aliases:
- /server/framework/atlassian-sdk/atlas-compile-2818348.html
- /server/framework/atlassian-sdk/atlas-compile-2818348.md
category: devguide
confluence_id: 2818348
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818348
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818348
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference/atlas-compile
new_url: /server/framework/atlassian-sdk/atlas-compile
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-compile
---
# atlas-compile

This page describes the shell script `atlas-compile`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

 

## Basic Usage

`atlas-compile [options]` - Compiles the sources of your project. (Runs `mvn compile`.) Passes all parameters straight through to Maven.

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
atlas-compile -?
atlas-compile -help
```

Run the following command to see all options provided by `mvn compile`:

``` javascript
atlas-mvn compile --help
```

Refer to the <a href="http://maven.apache.org/guides/getting-started/index.html#How_do_I_compile_my_application_sources" class="external-link">Maven documentation</a> for more information about the `mvn compile` command.

## Examples

Run the following command to compile your source code:

``` javascript
atlas-compile
```

Run the following command to compile your source code without failing the build, even if there are errors

``` javascript
atlas-compile --fail-never
```







































































































































































































