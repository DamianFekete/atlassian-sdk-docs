---
aliases:
- /server/framework/atlassian-sdk/atlas-help-2818350.html
- /server/framework/atlassian-sdk/atlas-help-2818350.md
category: devguide
confluence_id: 2818350
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818350
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818350
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference/atlas-help
new_url: /server/framework/atlassian-sdk/atlas-help
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-help
---
# atlas-help

This page describes the shell script `atlas-help`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

 

## Basic Usage

 `atlas-help [--verbose]` - Displays help text for the shell scripts incorporated into the Atlassian Plugin SDK. Interpreted parameters: `verbose`.

## Parameters

**--verbose** - lists all the shell scripts and the full help text for each command. Accepts a Value: no.

## Examples and More about Getting Help

{{% tip %}}

Help is at hand

Make sure you are not in the Maven command line interface (CLI) when you enter the help commands described below. If you are in the CLI, your command line will start with `maven2>`, and you will need to exit from the CLI first. Enter `quit`, `exit` or a friendly `bye`.

{{% /tip %}}

###### Getting an Overview of All the Scripts

Enter the following shell script to see an overview of all the scripts with a brief outline of their functionality:

``` bash
atlas-help
```

Enter the following to see all possible help content:

``` bash
atlas-help --verbose
```

###### Getting Help Text per Script

Each shell script provides help text if the first argument of the script is one of the following:

-   `-?`
-   `-h`
-   `help`
-   `-help`
-   `--help`

Examples:

``` bash
atlas-clean help
atlas-cli -?
```

###### Reading the Reference Guide

See the detailed <a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Atlassian+Plugin+SDK+Documentation&amp;linkCreation=true&amp;fromPageId=2818463" class="createlink">guide to all scripts</a>.

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)  
<a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Developing+your+Plugin+using+the+Atlassian+Plugin+SDK&amp;linkCreation=true&amp;fromPageId=2818350" class="createlink">Developing your Plugin using the Atlassian Plugin SDK</a>




























































































































