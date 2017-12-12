---
aliases:
- /server/framework/atlassian-sdk/atlas-cli-2818336.html
- /server/framework/atlassian-sdk/atlas-cli-2818336.md
category: devguide
confluence_id: 2818336
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818336
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818336
date: '2017-12-08'
guides: guides
legacy_title: atlas-cli
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-cli
---
# atlas-cli

{{% warning %}}

FastDev and atlas-cli have been deprecated. Please use [Automatic Plugin Reinstallation with QuickReload](https://developer.atlassian.com/docs/developer-tools/automatic-plugin-reinstallation-with-quickreload) instead.

{{% /warning %}}

 

This page describes the shell script `atlas-cli`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

 

Along with the plugin install (`pi`) command, this command allows you to install a plugin into a running Atlassian application, without having to restart the application. At the CLI prompt, you enter `pi` to install a plugin whenever you change its code.

Note that this mechanism is now incorporated in the user interface of Atlassian application as one of the developer tools. For more information, see [Automatic Plugin Reinstallation with FastDev](/server/framework/atlassian-sdk/automatic-plugin-reinstallation-with-fastdev). If you want to avoid using FastDev but do want to use the command line mode as described here, add the following to the AMPS configuration in your project POM:

`<useFastdevCli>false</useFastdevCli>`

## Basic Usage

`atlas-cli [options]` - Starts up a command line interface to your plugin running in the host application. After you change the plugin code, enter `pi` at the CLI prompt to install the updated plugin in the Atlassian application. (Runs `mvn amps:cli`.) Interpreted parameters: `http-port, context-path, server, cli-port`.Available CLI commands:

-   `pi` -- Plugin install. Installs your updated plugin into the application.
-   `quit`, `exit` or `bye` -- Exits from the CLI.

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
<td><p>HTTP port for the servlet container, e.g. <code>1990</code>. The defaults are as described in the <a href="/server/framework/atlassian-sdk/working-with-the-sdk-2818723.html#ports">SDK overview</a>. You may need to change this if you already have a process listed for the default port, such as when you want to bring up two instances of Confluence.</p>
<p><strong>Shortened: -p</strong></p></td>
</tr>
<tr class="even">
<td><p>--context-path</p></td>
<td><p>The application context path. You will need to include the leading forward slash. For example, if your application is running at <a href="http://localhost:1990/confluence" class="uri external-link">http://localhost:1990/confluence</a> then you should enter <code>/confluence</code>.</p>
<p>To run your application in the root web application context (eg. <a href="http://localhost:1990" class="uri external-link">http://localhost:1990</a>), then you should enter <code>ROOT</code>.</p></td>
</tr>
<tr class="odd">
<td><p>--server</p></td>
<td><p>Host name of the application server. The default is <code>localhost</code>.</p></td>
</tr>
<tr class="even">
<td><p>--cli-port</p></td>
<td><p>The port the CLI will listen to for commands. The default is <code>4330</code>. You may need to change this if you already have a process listed for this port.</p></td>
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
atlas-cli -?
atlas-cli -help
```

## Examples

Once you have done the initial `atlas-create-APPLICATION-plugin` and `atlas-run`, you can keep the application running in one command window and use the CLI (command line interface) to dynamically re-install your plugin after each change.

{{% note %}}

1.  Make your changes in your IDE.
2.  Open a command window and go to the plugin's root folder (where the `pom.xml` is located).
3.  Run `atlas-cli` to start the CLI.
4.  Wait until you see a message, `Waiting for commands`.
5.  Run `pi` (plugin install) to compile, package and install the plugin.
6.  Go back to your browser. The updated plugin will have been installed into the application, and you can test your changes. (You may need to refresh the browser page first.)

{{% /note %}}

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)































































































































































































































































