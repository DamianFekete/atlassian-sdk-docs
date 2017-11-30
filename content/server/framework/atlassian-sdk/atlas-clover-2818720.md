---
aliases:
- /server/framework/atlassian-sdk/atlas-clover-2818720.html
- /server/framework/atlassian-sdk/atlas-clover-2818720.md
category: devguide
confluence_id: 2818720
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818720
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818720
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference/atlas-clover
new_url: /server/framework/atlassian-sdk/atlas-clover
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-clover
---
# atlas-clover

This page describes the shell script `atlas-clover`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

 

## Basic Usage

`atlas-clover [options]` - Runs unit and integration tests, generating a code coverage report with <a href="http://atlassian.com/clover" class="external-link">Clover</a>. Passes all parameters straight through to Maven. Report is available in `target/site/clover/index.html`.

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
atlas-clover -?
atlas-clover -help
```

## Examples

``` javascript
atlas-clover
```

will run all your tests with Clover enabled and generate a source level, <a href="http://clover.atlassian.com/browse/guice/" class="external-link">HTML code coverage report</a> in `target/site/clover/index.html`.

A coverage summary will also be printed to stdout at the end of the build and will be pretty if you have [MAVEN\_COLOR=true](/server/framework/atlassian-sdk/colour-coding-your-maven-output-2818644.html):  
![](/server/framework/atlassian-sdk/images/screen-capture-5.png)

##### RELATED TOPICS

<a href="http://docs.atlassian.com/maven-clover2-plugin/2.6.0/" class="external-link">maven-clover2-plugin Site Docs</a>  
<a href="http://confluence.atlassian.com/x/K4CDBQ" class="external-link">Maven Clover User Guide</a>  
[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)  
[Getting Started](/server/framework/atlassian-sdk/index)





















































































































