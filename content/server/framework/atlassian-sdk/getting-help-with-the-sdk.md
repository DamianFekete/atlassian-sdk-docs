---
aliases:
- /server/framework/atlassian-sdk/getting-help-with-the-sdk-2818317.html
- /server/framework/atlassian-sdk/getting-help-with-the-sdk-2818317.md
category: devguide
confluence_id: 2818317
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818317
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818317
date: '2017-12-08'
guides: guides
legacy_title: Getting Help with the SDK
platform: server
product: atlassian-sdk
subcategory: learning
title: Getting help with the SDK
---
# Getting help with the SDK

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

See the detailed <a href="/server/framework/atlassian-sdk/getting-help-with-the-sdk" class="createlink">guide to all scripts</a>.
