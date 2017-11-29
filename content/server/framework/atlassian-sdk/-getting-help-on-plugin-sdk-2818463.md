---
title: Getting Help On Plugin Sdk 2818463
aliases:
    - /server/framework/atlassian-sdk/-getting-help-on-plugin-sdk-2818463.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818463
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818463
confluence_id: 2818463
platform:
product:
category:
subcategory:
---
# Documentation : \_Getting Help on Plugin SDK

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

























