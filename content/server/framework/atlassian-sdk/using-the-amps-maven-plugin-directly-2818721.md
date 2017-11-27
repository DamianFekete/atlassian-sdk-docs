---
title: Using the Amps Maven Plugin Directly 2818721
aliases:
    - /server/framework/atlassian-sdk/using-the-amps-maven-plugin-directly-2818721.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818721
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818721
confluence_id: 2818721
platform:
product:
category:
subcategory:
---
# Documentation : Using the AMPS Maven Plugin Directly

The Atlassian Plugin SDK is built on top of the Atlassian Maven Plugin Suite (AMPS). AMPS extends the Maven 2 build environment specifically for developing Atlassian plugins. When you create a project with the Atlassian Plugin SDK, AMPS is automatically configured as the build environment for your project.

This page provides more information about AMPS. You won't normally need to use AMPS directly, since the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk) wraps AMPS commands with its own script-style commands. However, in some cases you may wish to invoke AMPS commands directly or specify configuration settings for AMPS, which you can do in the project POM.

For information on configuring AMPS settings see [AMPS Build Configuration Reference](/server/framework/atlassian-sdk/amps-build-configuration-reference).

## AMPS Architecture

AMPS provides a set of plugins for Maven 2. AMPS combines multiple plugins, conventions, and POM configuration.  
  
*Diagram: AMPS architecture:*

![](/server/framework/atlassian-sdk/images/ampsarchitecture.png)

The application-specific configuration is as follows:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Application</p></th>
<th><p>AMPS Plugin Type</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Confluence</p></td>
<td><p><code>maven-confluence-plugin</code></p></td>
</tr>
<tr class="even">
<td><p>JIRA</p></td>
<td><p><code>maven-jira-plugin</code></p></td>
</tr>
<tr class="odd">
<td><p>Bamboo</p></td>
<td><p><code>maven-bamboo-plugin</code></p></td>
</tr>
<tr class="even">
<td><p>FishEye/Crucible</p></td>
<td><p><code>maven-fecru-plugin</code></p></td>
</tr>
<tr class="odd">
<td><p>Crowd</p></td>
<td><p><code>maven-crowd-plugin</code></p></td>
</tr>
<tr class="even">
<td>Stash</td>
<td><code>maven-stash-plugin</code></td>
</tr>
</tbody>
</table>

## Basic Commands

The commands are of the form `mvn APPLICATION:CMD`, where:

-   `APPLICATION` is the name of the product plugin above;
-   `CMD` is one of the commands listed below.

Examples:

-   `mvn confluence:run`
-   `mvn confluence:create`
-   `mvn jira:run`
-   `mvn jira:create`

In the table below, replace `APPLICATION` with the name of Atlassian application you are developing your plugin for. Fisheye and Crucible use the same plugin, so `APPLICATION` should be replaced with `fecru` if you are developing for Fisheye or Crucible.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>APPLICATION:create</p></td>
<td><p>Create a plugin skeleton from a Maven archetype, specific to the Atlassian application you are developing for.<br />
Examples: <code>mvn confluence:create</code> or <code>mvn jira:create</code></p></td>
</tr>
<tr class="even">
<td><p>APPLICATION:run</p></td>
<td><p>Download the application binaries (if not already downloaded), install your plugin, start the application with the container (application server) of your choice and your deployed plugin.<br />
Examples: <code>mvn confluence:run</code> or <code>mvn jira:run</code></p></td>
</tr>
<tr class="odd">
<td><p>APPLICATION:debug</p></td>
<td><p>Start the application with the container of your choice and your deployed plugin, with remote debugging enabled.</p></td>
</tr>
<tr class="even">
<td><p>APPLICATION:integration-test</p></td>
<td><p>Start the application with the container of your choice, and run all <code>it/**</code> integration tests, then shut the application down.</p></td>
</tr>
<tr class="odd">
<td><p>APPLICATION:unit-test</p></td>
<td><p>Run the unit tests, excluding <code>it/**</code>.</p></td>
</tr>
<tr class="even">
<td><p>APPLICATION:cli</p></td>
<td><p>Runs Maven in its interactive command line mode</p></td>
</tr>
<tr class="odd">
<td><p>APPLICATION:create-home-zip</p></td>
<td><p>Creates a zip of the current application's data which can be used in future runs of the SDK.</p></td>
</tr>
<tr class="even">
<td><p>APPLICATION:copy-bundled-dependencies</p></td>
<td><p>Copy all runtime and compile-scoped dependencies into <code>META-INF/lib</code>.</p></td>
</tr>
<tr class="odd">
<td><p>APPLICATION:install</p></td>
<td><p>Install your plugin (via the PDK).</p></td>
</tr>
<tr class="even">
<td><p>APPLICATION:uninstall</p></td>
<td><p>Uninstall your plugin (via the PDK).</p></td>
</tr>
</tbody>
</table>

## Examples

This section describes how to run the following commands:

-   [Creating a New Confluence Plugin from Scratch](#creating-a-new-confluence-plugin-from-scratch)
-   [Running a Plugin in an Application](#running-a-plugin-in-an-application)
-   [Specifying a Version of the Application](#specifying-a-version-of-the-application)
-   [Specifying an Application Server (Container)](#specifying-an-application-server-(container))
-   [Running your Plugin in Debug Mode from your IDE](#running-your-plugin-in-debug-mode-from-your-ide)
-   [Writing Integration Tests](#writing-integration-tests)
-   [Running Integration Tests against a Different Application](#running-integration-tests-against-a-different-application)
-   [Running your Plugin in Multiple Applications](#running-your-plugin-in-multiple-applications)
-   [Using the Command Line Interface in Interactive Mode](#using-the-command-line-interface-in-interactive-mode)
-   [Specifying a Version of AMPS](#specifying-a-version-of-amps)

### Creating a New Confluence Plugin from Scratch

Say you want to create a new Confluence plugin skeleton. Simply go to the directory where you want to create the plugin and type:

    mvn confluence:create

### Running a Plugin in an Application

Say you wanted to run an arbitrary plugin in Confluence. Simply go to the plugin's project directory and type:

    mvn confluence:run

### Specifying a Version of the Application

Say you wanted to run your plugin with Confluence 3.4:

    mvn confluence:run -Dproduct.version=3.4

Say you want to run your plugin with JIRA 4.2:

    mvn jira:run -Dproduct.version=4.2

### Specifying an Application Server (Container)

Say you wanted to run that plugin but with Confluence 3.4 and Tomcat 7:

    mvn confluence:run -Dproduct.version=3.4 -Dcontainer=tomcat7x

### Running your Plugin in Debug Mode from your IDE

Say you wanted to run that plugin in debug mode from your IDE. Set up a configuration in IDEA that executes from the project directory:

    mvn confluence:run -Dcontainer=jetty6x

### Writing Integration Tests

Say you wanted to write a new plugin for Confluence, with integration tests, but wanted minimal POM XML and you do not want to have to extend any other POM:

``` javascript
<packaging>confluence-plugin</packaging>
...
<plugin>
  <groupId>com.atlassian.maven.plugins</groupId>
  <artifactId>maven-confluence-plugin</artifactId>
  <extensions>true</extensions>
</plugin>
```

### Running Integration Tests against a Different Application

Say you had a Refapp plugin but wanted to run your integration tests against Confluence:

    mvn package confluence:integration-test

### Running your Plugin in Multiple Applications

Say you want to run the plugin in multiple applications simultaneously. In three separate tabs in your terminal (command window), type:

    mvn refapp:run

    mvn confluence:run -Dproduct.version=3.4

    mvn jira:run -Dproduct.version=4.2

You can now test your plugin on three applications side by side in your browser. This also means you can upgrade your plugin simultaneously:

    mvn package confluence:install refapp:install

### Using the Command Line Interface in Interactive Mode

The CLI command, a feature of the bundled <a href="http://wiki.github.com/mrdon/maven-cli-plugin" class="external-link">Maven CLI plugin</a>, allows you to work with Maven through an interactive command line.

In this mode, Maven remains in a running state, so that you can enter commands interactively. This saves time for JVM startups between running commands.

To put Maven into CLI mode, run this command from the project home directory:

    mvn confluence:cli

After a few moments, the CLI prompt appears:

    ...
    [INFO] [confluence:cli]
    [INFO] [cli:execute]
    [INFO] Opening port 4330 for socket cli access
    [INFO] Waiting for commands...
    maven2> 

From there, you can enter Maven commands as usual. For a list of available commands, enter `help` at the prompt.

### Specifying a Version of AMPS

The short form of the `mvn APPLICATION:run` or `mvn APPLICATION:create` command will use the latest version of the AMPS plugins. If you want to get a specific version of an AMPS command, use the longer form of the command. For example:  
`mvn com.atlassian.maven.plugins:maven-confluence-plugin:3.2.4:create`

##### RELATED TOPICS

[AMPS Build Configuration Reference](/server/framework/atlassian-sdk/amps-build-configuration-reference)

 

















































































































































































































































































































