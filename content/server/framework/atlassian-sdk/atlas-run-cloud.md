---
aliases:
- /server/framework/atlassian-sdk/atlas-run-cloud-37882647.html
- /server/framework/atlassian-sdk/atlas-run-cloud-37882647.md
category: devguide
confluence_id: 37882647
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=37882647
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=37882647
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference/atlas-run-cloud
new_url: /server/framework/atlassian-sdk/atlas-run-cloud
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-run-cloud
---
# atlas-run-cloud

{{% warning %}}

The atlas-run-cloud command is no longer the supported method for developing a cloud add-on as per the blog <a href="https://developer.atlassian.com/blog/2016/04/cloud-ecosystem-dev-env/" class="external-link" title="Follow link">Atlassian introduces new cloud development environment</a>.

{{% /warning %}}

This page describes the shell script `atlas-run-cloud`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk) (6.2.2 and later).

This command is used to start a local Cloud instance of an Atlassian application. It currently only works for JIRA Software. If you want to start a local instance of another application, or you want to start a local Server instance of JIRA Software, see [atlas-run-standalone](/server/framework/atlassian-sdk/atlas-run-standalone) instead.

 

## Basic Usage

 `atlas-run-cloud [options]` - Runs an Atlassian application with Connect and the Cloud dependencies installed. Interpreted parameters: `application, maven-plugin-version`.

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
<td><p>--application</p></td>
<td><p>Application to run. Application will be run with current Cloud configuration. Valid values:</p>
<ul>
<li><code>jira-software</code></li>
</ul></td>
</tr>
<tr class="even">
<td>--maven-plugin-version</td>
<td><p>Maven AMPS plugin version to use. The default value depends on the version of the Atlassian plugin SDK. View the help text for <code>atlas-run-cloud</code> (see below) for details.</p>
<p><strong>Shortened: -u</strong></p></td>
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
atlas-run-cloud -?
atlas-run-cloud -help
```

## Examples

Say you want to quickly spin up an instance of JIRA Software with Connect and all of the Cloud dependencies installed. At the command line, type:

``` bash
atlas-run-cloud --application jira-software
```

This will do the following:

1.  Download the latest pom defining the current Cloud production environment with JIRA Software, Atlassian Connect and other Cloud dependencies
2.  Create a directory called `target` in your current working directory, which will contain a JIRA home directory, database and server logs.
3.  Start up a JIRA Software instance. The output message from this command will tell you the URL where JIRA Software was started.

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)



















































































































