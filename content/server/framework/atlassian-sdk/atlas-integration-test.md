---
aliases:
- /server/framework/atlassian-sdk/atlas-integration-test-2818349.html
- /server/framework/atlassian-sdk/atlas-integration-test-2818349.md
category: devguide
confluence_id: 2818349
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818349
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818349
date: '2017-12-08'
guides: guides
legacy_title: atlas-integration-test
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-integration-test
---
# atlas-integration-test

This page describes the shell script `atlas-integration-test`, part of the <a href="/server/framework/atlassian-sdk/atlas-integration-test/" class="createlink">Atlassian Plugin SDK</a>.

## Basic Usage

 `atlas-integration-test [options]` - Runs the integration tests for the plugin. (Runs `mvn integration-test`.) Interpreted parameters: `version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins,lib-plugins, bundled-plugins, product, no-webapp, skip-tests`.

## Parameters

This shell script supports some interpreted parameters, specified below. All other parameters are passed straight through to Maven.

Explaining the table columns:

-   'Full Parameter' and 'Shortened' - Some parameters allow you to choose a full or a shortened version of the parameter, others just support the full version.
-   'Accepts a Value?' - 'Yes' means that you should specify a value in addition to the parameter, e.g. for the 'version' parameter you should specify the version number. 'No' means that the parameter does not accept a value.

Interpreted parameters:

<table>
<colgroup>
<col style="width: 20%" />
<col style="width: 80%" />
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
<td><p>Version of the application to run. Default is <code>RELEASE</code>. Examples:</p>
<ul>
<li><code>3.1</code></li>
<li><code>3.1-m7</code></li>
</ul>
<p><code>Shortened: -v</code></p></td>
</tr>
<tr class="even">
<td><p>--container</p></td>
<td><p>Container to run in. Default is <code>tomcat6x</code>. Other available values are <code>tomcat5x</code>, <code>resin3x</code> and <code>jboss42x</code>.</p>
<p><strong>Shortened: -c</strong></p></td>
</tr>
<tr class="odd">
<td><p>--http-port</p></td>
<td><p>HTTP port for the servlet container. The defaults are as described in the <a href="/server/framework/atlassian-sdk/atlas-integration-test/" class="createlink">SDK overview</a>. You may need to change this if you already have a process listed for the default port, such as when you want to bring up two instances of Confluence.</p>
<p><strong>Shortened: -p</strong></p></td>
</tr>
<tr class="even">
<td><p>--context-path</p></td>
<td><p>The<br />
application context path. You will need to include the leading forward<br />
slash. For example, if your application is running at</p>
<a href="http://localhost:1990/confluence" class="uri external-link">http://localhost:1990/confluence</a>
<p>then you should enter <code>/confluence</code>.<br />
To run your application in the root web application context (eg.<a href="http://localhost:1990" class="uri external-link">http://localhost:1990</a>), then you should enter <code style="background-color: transparent;">ROOT</code>.</p></td>
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
<td><p>Log4j properties file.</p></td>
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
<td><p>Version of the <a href="https://developer.atlassian.com/display/REST/REST+Plugin+Module">Atlassian REST module</a> to use.</p></td>
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
<td><p>A list of bundled plugin artifacts, separated by commas, in the form <code>GROUP_ID:ARTIFACT_ID:VERSION</code>. Version is optional. Default is <code>LATEST</code>.These plugins will be loaded as bundled plugins in your local version of your plugin's host application.</p></td>
</tr>
<tr class="even">
<td><p>--product</p></td>
<td><p>The application to launch with the plugin. You might use this if your plugin is written for one application (as specified in the POM) but you want to install the plugin into another application.</p></td>
</tr>
<tr class="odd">
<td><p>--no-webapp</p></td>
<td><p>If this parameter is present, then the script will not start up the plugin's host application.</p></td>
</tr>
<tr class="even">
<td><p>--skip-tests</p></td>
<td><p>If this parameter is present, the script will not execute the unit or integration tests.</p></td>
</tr>
</tbody>
</table>

***--no-webapp* and *--skip-tests* don't accept a value.**

## Getting Help

The shell script will display some help text if you enter one of the following as the first argument:

-   -?
-   -h
-   help
-   -help
-   --help

For example:

``` bash
atlas-integration-test -?
atlas-integration-test -help
```

## Examples

You can run your integration tests against a different application. Say you have a RefApp plugin but want to run your integration tests against Confluence:

``` bash
atlas-integration-test --product confluence
```

##### RELATED TOPICS

<a href="/server/framework/atlassian-sdk/atlas-integration-test/" class="createlink">Atlassian Plugin SDK Documentation</a>  
[Plugin Testing Resources and Discussion](https://developer.atlassian.com/pages/viewpage.action?pageId=2818627)
