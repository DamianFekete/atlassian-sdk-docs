---
aliases:
- /server/framework/atlassian-sdk/atlas-debug-2818346.html
- /server/framework/atlassian-sdk/atlas-debug-2818346.md
category: devguide
confluence_id: 2818346
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818346
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818346
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: Atlas Debug 2818346
---
# atlas-debug

This page describes the shell script `atlas-debug`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

 

## Basic Usage

 `atlas-debug [options]` - Runs the application in debug mode with your plugin installed. (Runs `mvn amps:debug`.) Interpreted parameters: `version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins, lib-plugins, bundled-plugins, product, jvm-debug-port, jvm-debug-suspend`.

## Parameters

This shell script supports some interpreted parameters, specified below. All other parameters are passed straight through to Maven.

Explaining the table columns:

-   'Full Parameter' and 'Shortened' - Some parameters allow you to choose a full or a shortened version of the parameter, others just support the full version.
-   'Accepts a Value?' - 'Yes' means that you should specify a value in addition to the parameter, e.g. for the 'version' parameter you should specify the version number. 'No' means that the parameter does not accept a value.

Interpreted parameters:

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
<td><p>--version</p></td>
<td><p>Version of the application to run. Default is <code>RELEASE</code>, i.e. the latest publicly-available milestone release. Examples:</p>
<ul>
<li><code>3.1</code></li>
<li><code>3.1-m7</code></li>
</ul>
<p><strong>Shortened: -v</strong></p></td>
</tr>
<tr class="even">
<td><p>--container</p></td>
<td><p>Container to run in. Default is <code>tomcat6x</code>. Other available values are <code>tomcat5x</code>, <code>resin3x</code> and <code>jboss42x</code>.</p>
<p><strong>Shortened: -c</strong></p></td>
</tr>
<tr class="odd">
<td><p>--http-port</p></td>
<td><p>HTTP port for the servlet container. The defaults are as described in the <a href="/server/framework/atlassian-sdk/working-with-the-sdk-2818723.html#ports">SDK overview</a>. You may need to change this if you already have a process listed for the default port, such as when you want to bring up two instances of Confluence.</p>
<p><strong>Shortened: -p</strong></p></td>
</tr>
<tr class="even">
<td><p>--context-path</p></td>
<td><p>The application context path. You will need to include the leading forward slash. For example, if your application is running at <a href="http://localhost:1990/confluence" class="uri external-link">http://localhost:1990/confluence</a> then you should enter <code>/confluence</code>.</p>
To run your application in the root web application context (eg. <a href="http://localhost:1990" class="uri external-link">http://localhost:1990</a>), then you should enter ROOT.</td>
</tr>
<tr class="odd">
<td><p>--server</p></td>
<td><p>Host name of the application server. The default is <code>localhost</code>.</p></td>
</tr>
<tr class="even">
<td><p>--jvmargs</p></td>
<td><p>Additional JVM arguments if required.</p></td>
</tr>
<tr class="odd">
<td><p>--log4j</p></td>
<td><p>Path and file name of the Log4j properties file.</p></td>
</tr>
<tr class="even">
<td><p>--test-version</p></td>
<td><p>Version to use for test resources. Default is <code>LATEST</code>.</p></td>
</tr>
<tr class="odd">
<td><p>--sal-version</p></td>
<td><p>Version of SAL (<a href="https://developer.atlassian.com/display/SAL">Shared Access Layer</a>) to use.</p></td>
</tr>
<tr class="even">
<td><p>--rest-version</p></td>
<td><p>Version of the <a href="/server/framework/atlassian-sdk/rest-plugin-module">Atlassian REST module</a> to use.</p></td>
</tr>
<tr class="odd">
<td><p>--plugins</p></td>
<td><p>A list of plugin artifacts, separated by commas, in the form <code>GROUP_ID:ARTIFACT_ID:VERSION</code>. Version is optional. Default is <code>LATEST</code>. These plugins will be installed into your local version of your plugin's host application.</p></td>
</tr>
<tr class="even">
<td><p>--lib-plugins</p></td>
<td><p>A list of lib artifacts, separated by commas, in the form <code>GROUP_ID:ARTIFACT_ID:VERSION</code>. Version is optional. Default is <code>LATEST</code>. Use this to add additional JARs into your <code>/lib</code> folder.</p></td>
</tr>
<tr class="odd">
<td><p>--bundled-plugins</p></td>
<td><p>A list of bundled plugin artifacts, separated by commas, in the form <code>GROUP_ID:ARTIFACT_ID:VERSION</code>. Version is optional. Default is <code>LATEST</code>. These plugins will be loaded as bundled plugins in your local version of your plugin's host application.</p></td>
</tr>
<tr class="even">
<td><p>--product</p></td>
<td><p>The application to launch with the plugin. You might use this if your plugin is written for one application (as specified in the POM) but you want to install the plugin into another application.</p></td>
</tr>
<tr class="odd">
<td><p>--jvm-debug-port</p></td>
<td><p>Port open to accept connections for remote debugging. Default is <code>5005</code>.</p></td>
</tr>
<tr class="even">
<td><p>--jvm-debug-suspend</p></td>
<td><p>If this parameter is present, the JVM will be suspended until the debugger connects.</p></td>
</tr>
</tbody>
</table>

***--jvm-debug-suspend* doesn't accept a value.**

## Getting Help

The shell script will display some help text if you enter one of the following as the first argument:

-   -?
-   -h
-   help
-   -help
-   --help

For example:

``` bash
atlas-debug -?
atlas-debug -help
```

## Examples

###### Running a Plugin in an Application

Say you want to install and run your plugin in your host Atlassian application, attaching your debugger. Go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-debug
```

Note that the above shell script will work for any host application, including Confluence, JIRA, etc. The script will determine the application, based on your plugin's specifications.

###### Specifying a Version of the Application

Say you want to run your plugin with Confluence 2.10.3, attaching your debugger. Go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-clean
atlas-debug --version 2.10.3
```

Say you want to run your plugin with JIRA 4.0 snapshot. Go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-clean
atlas-debug --version 4.0-SNAPSHOT
```

*Note:* Running `atlas-clean` will clear the previous version of the host application from your build output directory. You only need to do this if the previous application version was different from the one you need now.

###### Specifying an Application Server (Container)

Say you want to run your plugin with Confluence 2.10.3 and JBoss 4.2.x. Go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-debug --version 2.10.3 --container jboss42x
```

###### Specifying a Version of SAL

Say you want to run that plugin but with Confluence 2.10.3 and SAL 2.0.5:

``` bash
atlas-debug --version 2.10.3 --sal-version 2.0.5
```

###### Running your Plugin in Multiple Applications

Say you want to run that RefApp plugin in multiple applications simultaneously, with debugger attached. In three separate tabs in your terminal (command window):

-   Type the following to run the plugin in the RefApp:

    ``` bash
    atlas-debug
    ```

-   Type the following to run the plugin in Confluence:

    ``` bash
    atlas-debug --product confluence --version 3.0-m9
    ```

-   Type the following to run the plugin in JIRA:

    ``` bash
    atlas-debug --product jira --version 4.0-SNAPSHOT
    ```





























































































































