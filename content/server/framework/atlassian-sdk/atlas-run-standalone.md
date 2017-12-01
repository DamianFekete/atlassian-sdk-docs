---
aliases:
- /server/framework/atlassian-sdk/atlas-run-standalone-2818534.html
- /server/framework/atlassian-sdk/atlas-run-standalone-2818534.md
category: devguide
confluence_id: 2818534
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818534
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818534
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference/atlas-run-standalone
new_url: /server/framework/atlassian-sdk/atlas-run-standalone
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-run-standalone
---
# atlas-run-standalone

This page describes the shell script `atlas-run-standalone`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk). 

 

## Basic Usage

 `atlas-run-standalone [options]` - Runs an Atlassian application standalone, without a plugin project (that is, not requiring `atlas-create-<product>-plugin`). Interpreted parameters: `version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins, lib-plugins, bundled-plugins, product`.

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
<th><p>Full Parameter</p>
<p> </p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>--version</p>
<p> </p></td>
<td><p>Version of the application to run. Default is <code>RELEASE</code>. Examples:</p>
<ul>
<li><code>3.1</code></li>
<li><code>3.1-m7</code></li>
</ul>
{{% note %}}
<div class="confluence-information-macro-information confluence-information-macro">
<div class="confluence-information-macro-body">
<p>If you want to change versions, you need to clean the target directory by deleting it or running atlas-clean</p>
</div>
</div>
{{% /note %}}
<p><strong>Shortened: -v</strong></p>
<p> </p></td>
</tr>
<tr class="even">
<td><p>--container</p>
<p> </p></td>
<td><p>Container to run in. Default is <code>tomcat8x</code>. Other available values are <code>tomcat5x</code>, <code>resin3x</code> and <code>jboss42x</code>.</p>
<p><strong>Shortened: -c</strong></p></td>
</tr>
<tr class="odd">
<td><p>--http-port</p>
<p> </p></td>
<td><p>HTTP port for the servlet container. The defaults are as described in the <a href="/server/framework/atlassian-sdk/working-with-the-sdk-2818723.html#ports">SDK overview</a>. You may need to change this if you already have a process listed for the default port, such as when you want to bring up two instances of Confluence.</p>
<p><strong>Shortened: -p</strong></p></td>
</tr>
<tr class="even">
<td><p>--context-path</p>
<p> </p></td>
<td><p>The application context path. You will need to include the leading forward slash. For example, if your application is running at <a href="http://localhost:1990/confluence" class="uri external-link">http://localhost:1990/confluence</a> then you should enter <code>/confluence</code>.</p>
<p>To run your application in the root web application context (eg. <a href="http://localhost:1990" class="uri external-link">http://localhost:1990</a>), then you should enter <code>ROOT</code>.</p></td>
</tr>
<tr class="odd">
<td><p>--server</p>
<p> </p></td>
<td><p>Host name of the application server. The default is <code>localhost</code>.</p></td>
</tr>
<tr class="even">
<td><p>--jvmargs</p>
<p> </p></td>
<td><p>Additional JVM arguments if required.</p></td>
</tr>
<tr class="odd">
<td><p>--log4j</p>
<p> </p></td>
<td><p>Log4j properties file.</p></td>
</tr>
<tr class="even">
<td><p>--test-version</p>
<p> </p></td>
<td><p>Version to use for test resources. DEPRECATED: use data-version instead.</p></td>
</tr>
<tr class="odd">
<td>--data-version</td>
<td>Version to use for data resources (default is RELEASE)</td>
</tr>
<tr class="even">
<td><p>--sal-version</p>
<p> </p></td>
<td><p>Version of SAL (<a href="https://developer.atlassian.com/display/SAL">Shared Access Layer</a>) to use.</p></td>
</tr>
<tr class="odd">
<td><p>--rest-version</p>
<p> </p></td>
<td><p>Version of the <a href="/server/framework/atlassian-sdk/rest-plugin-module">Atlassian REST module</a> to use.</p></td>
</tr>
<tr class="even">
<td><p>--plugins</p></td>
<td><p>A list of plugin artifacts, separated by commas, in the form <code>GROUP_ID:ARTIFACT_ID:VERSION</code>. Version is optional. Default is <code>LATEST</code>. These plugins will be installed into the application.</p></td>
</tr>
<tr class="odd">
<td><p>--lib-plugins</p></td>
<td><p>A list of lib artifacts, separated by commas, in the form <code>GROUP_ID:ARTIFACT_ID:VERSION</code>. Version is optional. Default is <code>LATEST</code>. Use this to add additional JARs into your <code>/lib</code> folder.</p></td>
</tr>
<tr class="even">
<td><p>--bundled-plugins</p></td>
<td><p>A list of bundled plugin artifacts, separated by commas, in the form <code>GROUP_ID:ARTIFACT_ID:VERSION</code>. Version is optional. Default is <code>LATEST</code>. These plugins will be loaded as bundled plugins in the application.</p></td>
</tr>
<tr class="odd">
<td><p>--product</p></td>
<td><p>The application to launch.</p></td>
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
atlas-run-standalone -?
atlas-run-standalone -help
```

## Examples

###### Running an Application

Say you want to quickly spin up an instance of JIRA, without having previously created a JIRA plugin project using `atlas-create-jira-plugin`. At the command line, type:

``` bash
atlas-run-standalone --product jira
```

This will create a directory called `amps-standalone` in your current working directory, which will contain a JIRA home directory, database and server logs.

###### Specifying a Version of the Application

Say you want to start up Confluence version 3.2.2 specifically, rather than the latest version. At the command line, type:

``` bash
atlas-run-standalone --product confluence --version 3.2.2
```

## Default Ports for Each Application

The table below shows the applications currently supported by the Atlassian Plugin SDK, the default port, and the product key for each host application.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Atlassian Application</p></th>
<th><p>Default Port</p></th>
<th><p>Product Key</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/bamboo" class="external-link">Bamboo</a></p></td>
<td><p>6990</p></td>
<td><p>bamboo</p></td>
</tr>
<tr class="even">
<td><a href="https://www.atlassian.com/software/bitbucket/server" class="external-link">Bitbucket</a></td>
<td>7990</td>
<td>bitbucket</td>
</tr>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/confluence" class="external-link">Confluence</a></p></td>
<td><p>1990</p></td>
<td><p>confluence</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.atlassian.com/software/crowd" class="external-link">Crowd</a></p></td>
<td><p>4990</p></td>
<td><p>crowd</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/crucible" class="external-link">Crucible</a></p></td>
<td><p>3990</p></td>
<td><p>fecru</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.atlassian.com/software/fisheye" class="external-link">FishEye</a></p></td>
<td><p>3990</p></td>
<td><p>fecru</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/jira" class="external-link">JIRA</a></p></td>
<td><p>2990</p></td>
<td><p>jira</p></td>
</tr>
<tr class="even">
<td><p><a href="https://developer.atlassian.com/display/DOCS/About+the+Atlassian+RefApp">RefApp</a></p></td>
<td><p>5990</p></td>
<td><p>refapp</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/stash" class="external-link">Stash</a></p></td>
<td><p>7990</p></td>
<td><p>stash</p></td>
</tr>
</tbody>
</table>

***Caveat for <a href="http://www.atlassian.com/software/jira" class="external-link">JIRA</a>:** Plugins developed for versions of JIRA before 4.0 are supported, but using the SDK with versions of JIRA earlier than 4.0 is not. For developing plugins for JIRA 3.13 and earlier, take a look at the [JIRA Documentation Archives](https://developer.atlassian.com/display/ARCHIVES/JIRA+Documentation+Archives).*

## Limitations

Currently if you want to run multiple products, or multiple versions of each product, you must either use different working directories to contain the `amps-standalone` data for each product, or you must manually remove the `target` directory under `amps-standalone`. See issue <a href="https://studio.atlassian.com/browse/AMPS-403" class="external-link">AMPS-403</a>.

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)


















































































































