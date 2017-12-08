---
aliases:
- /server/framework/atlassian-sdk/atlas-install-plugin-2818722.html
- /server/framework/atlassian-sdk/atlas-install-plugin-2818722.md
category: devguide
confluence_id: 2818722
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818722
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818722
date: '2017-12-08'
guides: guides
legacy_title: atlas-install-plugin
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-install-plugin
---
# atlas-install-plugin

This page describes the shell script `atlas-install-plugin`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

 

## Basic Usage

 `atlas-install-plugin [options]` - Installs the plugin into a running application. (Runs `mvn amps:install`.) Interpreted parameters: `http-port, context-path, server, username, password, plugin-key`.

## Parameters

This shell script supports some interpreted parameters, specified below. All other parameters are passed straight through to Maven.

Explaining the table columns:

-   'Full Parameter' and 'Shortened' - Some parameters allow you to choose a full or a shortened version of the parameter, others just support the full version.
-   'Accepts a Value?' - 'Yes' means that you should specify a value in addition to the parameter, e.g. for the 'version' parameter you should specify the version number. 'No' means that the parameter does not accept a value.

Interpreted Parameters:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Full Parameter</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>--http-port</p></td>
<td><p>HTTP port for the servlet container. The defaults are as described in the <a href="/server/framework/atlassian-sdk/working-with-the-sdk-2818723.html#ports">SDK overview</a>. You may need to change this if you already have a process listed for the default port, such as when you want to bring up two instances of Confluence.</p>
<p><strong>Shortened: -p</strong></p></td>
</tr>
<tr class="even">
<td><p>--context-path</p></td>
<td><p>The application context path. You will need to include the leading forward slash. For example, if your application is running at <a href="http://localhost:1990/confluence" class="uri external-link">http://localhost:1990/confluence</a> then you should enter <code>/confluence</code>.</p>
<p>To run your application in the root web application context (eg. <a href="http://localhost:1990" class="uri external-link">http://localhost:1990</a>), then you should enter ROOT.</p></td>
</tr>
<tr class="odd">
<td><p>--server</p></td>
<td><p>Host name of the application server. The default is <code>localhost</code>.</p></td>
</tr>
<tr class="even">
<td><p>--username</p></td>
<td><p>Username for the administrator account on the plugin's host application. Default is <code>admin</code>.</p></td>
</tr>
<tr class="odd">
<td><p>--password</p></td>
<td><p>Password for the above administrator account on the plugin's host application. Default is <code>admin</code>.</p></td>
</tr>
<tr class="even">
<td><p>--plugin-key</p></td>
<td><p>Unique key identifying the plugin. This is the full key specified in your <code>atlassian-plugin.xml</code>, including the group and artifact IDs. For example, <code>&quot;com.atlassian.confluence.plugins.example&quot;</code>.</p></td>
</tr>
</tbody>
</table>

**All above accepts a value.**

## Getting Help

The shell script will display some help text if you enter one of the following as the first argument:

-   -?
-   -h
-   help
-   -help
-   --help

For example:

``` bash
atlas-install-plugin -?
atlas-install-plugin -help
```

## Examples

Go to the plugin's project directory (where you created the plugin) and run the following command to install your plugin `com.atlassian.confluence.plugins.example` into the host application, where the administration username is 'myadmin' with password 'secret'.

``` bash
atlas-install-plugin --username myadmin --password secret --plugin-key com.atlassian.confluence.plugins.example
```


























































































































