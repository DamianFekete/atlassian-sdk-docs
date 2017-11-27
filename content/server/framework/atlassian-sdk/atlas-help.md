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

<table>
<colgroup>
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
<col style="width: 25%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Full Parameter</p></th>
<th><p>Shortened</p></th>
<th><p>Accepts a Value?</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>--verbose</p></td>
<td><p> </p></td>
<td><p>No</p></td>
<td><p>Lists all the shell scripts and the full help text for each command.</p></td>
</tr>
</tbody>
</table>

## Examples and More about Getting Help

{{% tip %}}

Help is at hand

Make sure you are not in the Maven command line interface (CLI) when you enter the help commands described below. If you are in the CLI, your command line will start with `maven2>`, and you will need to exit from the CLI first. Enter `quit`, `exit` or a friendly `bye`.

{{% /tip %}}

###### Getting an Overview of All the Scripts

Enter the following shell script to see an overview of all the scripts with a brief outline of their functionality:

``` javascript
atlas-help
```

Enter the following to see all possible help content:

``` javascript
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

``` javascript
atlas-clean help
atlas-cli -?
```

###### Reading the Reference Guide

See the detailed <a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Atlassian+Plugin+SDK+Documentation&amp;linkCreation=true&amp;fromPageId=2818463" class="createlink">guide to all scripts</a>.

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)  
<a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Developing+your+Plugin+using+the+Atlassian+Plugin+SDK&amp;linkCreation=true&amp;fromPageId=2818350" class="createlink">Developing your Plugin using the Atlassian Plugin SDK</a>































































































































































