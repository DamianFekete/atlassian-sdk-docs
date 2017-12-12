---
aliases:
- /server/framework/atlassian-sdk/working-with-maven-5669840.html
- /server/framework/atlassian-sdk/working-with-maven-5669840.md
category: devguide
confluence_id: 5669840
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669840
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669840
date: '2017-12-08'
guides: guides
legacy_title: Working with Maven
platform: server
product: atlassian-sdk
subcategory: learning
title: Working with Maven
---
# Working with Maven

While the SDK conceals many of the complexities of Maven, it is helpful to understand how it is used, particularly when you are troubleshooting or using advance Maven features. This page discusses concepts behind Maven and how it is used with the SDK.

## What is Maven?

Calling Maven a 'build tool' would be an understatement. But if you have no experience with Maven yet, start thinking of it as a tool for simplifying your life by building your plugin. Quoting the Maven home page:

> Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

Maven is particularly useful because it can automatically manage massive dependency trees, especially transitive dependencies where Plugin X depends on Application Y, which depends on Shared Library Z. Using Maven, you should be able to quickly and easily retrieve all the dependencies that your plugin will need, and create a working development environment in just a few steps.

## Maven and the Atlassian Plugins SDK 

Maven is bundled with the Atlassian Plugin SDK, so you do not need to install it manually. Even if you already have Maven on your system, you should use the one bundled with the SDK, since the SDK requires a specific version of Maven. The version bundled with the SDK is already configured for the SDK, so you do not need to specify repositories. The Atlassian Plugin SDK includes a correctly-configured Maven `settings.xml` file.

The Atlassian SDK wraps Maven commands with its own interactive, script-based commands. The SDK commands offer command-line help and auto-completion, easing development tasks. 

## Running Maven Commands

If you already know Maven, you may want to invoke Maven commands directly.  When running Maven commands against your project, make sure that you use the version of Maven bundled with the Atlassian Plugin SDK. This is important if you have a local version of Maven installed, as well as the Atlassian Plugin SDK.

The simplest way is to use the [`atlas-mvn`](https://developer.atlassian.com/display/DOCS/atlas-mvn) wrapper command instead of `mvn`. You can invoke any Maven command by preceding it in the '`atlas-`' prefix.

For example:

 

``` bash
atlas-mvn clean
```

The command performs the same function as the Maven command `mvn clean`, removing build artifacts from the current project.

If you have multiple versions of Maven on your system, you should use the SDK command wrapper to ensure that the correct Maven version is executed. Alternatively, you can put the bundled Maven on your path. (Run atlas-version to discover the location of the SDK's Maven instance binary file.)

For information on the standard SDK command format, see [Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

## Verifying Your Maven Settings

The Maven settings file, `settings.xml`, controls some of the general behavior of Maven. For instance, the file identifies the repositories used to resolve plugin dependencies. It also specifies development environment properties. For example, the `settings.xml` file is where you configure your proxy settings if you need to connect to the Internet through a web proxy.

## settings.xml Location

The file is located in the following directory:

`<atlassian-plugin-sdk-home>/apache-maven/conf`

When installed with the Atlassian SDK, the `settings.xml` is pre-configured with the Atlassian repositories needed to build plugin projects. If you want to include additional repositories in the default profile, you can add them to the file.

## Adding the Atlassian Plugin Repository

We recommend that you use the Maven instance installed with the SDK, which is already configured to rely on the required repositories. However, if for some reason you are attempting to use a `settings.xml` file that was not installed with the Atlassian SDK, you will likely encounter problems resolving dependencies required by the SDK commands. To prevent these problems, add the `pluginGroups` and `profile` elements to your local `settings.xml` file:

``` xml
<pluginRepository>
    <id>atlassian-plugin-sdk</id>
    <url>file://${env.ATLAS_HOME}/repository</url>
     <releases>
        <enabled>true</enabled>
        <checksumPolicy>warn</checksumPolicy>
      </releases>
      <snapshots>
         <enabled>false</enabled>
      </snapshots>
 </pluginRepository>
```

## Colour-Coding your Maven Output

If you are using the Atlassian Plugin SDK in  a UNIX, Linux, or OSX environment you can ensure that your Maven output comes in true colour. Just add an environment variable with the name `MAVEN_COLOR` and value `true`.

``` bash
export MAVEN_COLOR=true
```

Your Maven output will look something like this:  
![](/server/framework/atlassian-sdk/images/mavencolourisedoutput.png)

## Using the AMPS Maven Plugin Directly

The Atlassian Plugin SDK is built on top of the Atlassian Maven Plugin Suite (AMPS). AMPS extends the Maven 2 build environment specifically for developing Atlassian plugins. When you create a project with the Atlassian Plugin SDK, AMPS is automatically configured as the build environment for your project.

This page provides more information about AMPS. You won't normally need to use AMPS directly, since the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk) wraps AMPS commands with its own script-style commands. However, in some cases you may wish to invoke AMPS commands directly or specify configuration settings for AMPS, which you can do in the project POM.

For information on configuring AMPS settings see [AMPS Build Configuration Reference](/server/framework/atlassian-sdk/amps-build-configuration-reference).

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

The commands are of the form `mvn APPLICATION:CMD`, where:

-   `APPLICATION` is the name of the product plugin above;
-   `CMD` is one of the commands listed below.

Examples:

-   `mvn confluence:run`
-   `mvn confluence:create`
-   `mvn jira:run`
-   `mvn jira:create`

In the table below, replace `APPLICATION` with the name of Atlassian application you are developing your plugin for. Fisheye and Crucible use the same plugin, so `APPLICATION` should be replaced with `fecru` if you are developing for Fisheye or Crucible.

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

### Creating a New Confluence Plugin from Scratch

Say you want to create a new Confluence plugin skeleton. Simply go to the directory where you want to create the plugin and type:

``` bash
mvn confluence:create
```

### Running a Plugin in an Application

Say you wanted to run an arbitrary plugin in Confluence. Simply go to the plugin's project directory and type:

``` bash
mvn confluence:run
```

### Specifying a Version of the Application

Say you wanted to run your plugin with Confluence 3.4:

``` bash
mvn confluence:run -Dproduct.version=3.4
```

Say you want to run your plugin with JIRA 4.2:

``` bash
mvn jira:run -Dproduct.version=4.2
```

### Specifying an Application Server (Container)

Say you wanted to run that plugin but with Confluence 3.4 and Tomcat 7:

``` bash
mvn confluence:run -Dproduct.version=3.4 -Dcontainer=tomcat7x
```

### Running your Plugin in Debug Mode from your IDE

Say you wanted to run that plugin in debug mode from your IDE. Set up a configuration in IDEA that executes from the project directory:

``` bash
mvn confluence:run -Dcontainer=jetty6x
```

### Writing Integration Tests

Say you wanted to write a new plugin for Confluence, with integration tests, but wanted minimal POM XML and you do not want to have to extend any other POM:

``` xml
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

``` bash
mvn package confluence:integration-test
```

### Running your Plugin in Multiple Applications

Say you want to run the plugin in multiple applications simultaneously. In three separate tabs in your terminal (command window), type:

``` bash
mvn refapp:run
```

``` bash
mvn confluence:run -Dproduct.version=3.4
```

``` bash
mvn jira:run -Dproduct.version=4.2
```

You can now test your plugin on three applications side by side in your browser. This also means you can upgrade your plugin simultaneously:

``` bash
mvn package confluence:install refapp:install
```

### Using the Command Line Interface in Interactive Mode

The CLI command, a feature of the bundled <a href="http://wiki.github.com/mrdon/maven-cli-plugin" class="external-link">Maven CLI plugin</a>, allows you to work with Maven through an interactive command line.

In this mode, Maven remains in a running state, so that you can enter commands interactively. This saves time for JVM startups between running commands.

To put Maven into CLI mode, run this command from the project home directory:

``` bash
mvn confluence:cli
```

After a few moments, the CLI prompt appears:

``` bash
...
[INFO] [confluence:cli]
[INFO] [cli:execute]
[INFO] Opening port 4330 for socket cli access
[INFO] Waiting for commands...
maven2> 
```

From there, you can enter Maven commands as usual. For a list of available commands, enter `help` at the prompt.

### Specifying a Version of AMPS

The short form of the `mvn APPLICATION:run` or `mvn APPLICATION:create` command will use the latest version of the AMPS plugins. If you want to get a specific version of an AMPS command, use the longer form of the command. For example:   
`mvn com.atlassian.maven.plugins:maven-confluence-plugin:3.2.4:create`

##### RELATED TOPICS

[AMPS Build Configuration Reference](/server/framework/atlassian-sdk/amps-build-configuration-reference)

## Atlassian Maven Repositories

Atlassian provides various Maven repositories for Plugin Developers.We recommend using the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk) to make sure you've got the correct settings to use our servers.

The Plugin SDK handles almost all of this Maven tweaking for you. The SDK includes an embedded Maven installation and correct `settings.xml` that will be kept up to date as necessary. We believe it makes the plugin development process much easier. For more information, see [here](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

## Atlassian Maven Proxy 

The Atlassian Maven proxy sits in front of all of our other Maven repositories, as well as third-party repositories like iBiblio and Codehaus. This should provide all artifacts needed to build our products and plugins. In the basic case, this is the only repository you need to know about.

-   <a href="https://packages.atlassian.com/maven/repository/public" class="uri external-link">https://packages.atlassian.com/maven/repository/public</a>

``` xml
<repository>
      <id>atlassian-public</id>
      <url>https://packages.atlassian.com/maven/repository/public</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
        <checksumPolicy>warn</checksumPolicy>
      </snapshots>
       <releases>
         <enabled>true</enabled>
         <checksumPolicy>warn</checksumPolicy>
      </releases>
</repository>
```

### Atlassian 3rdParty Repository

The third-party directory contains jars that we are allowed to re-distribute or re-host but we do not own.

-   <a href="https://packages.atlassian.com/maven/3rdparty" class="uri external-link">https://packages.atlassian.com/maven/3rdparty</a>

It is contained in <a href="https://packages.atlassian.com/maven/repository/public" class="uri external-link">https://packages.atlassian.com/maven/repository/public</a>.

### Atlassian Public Repository

The Atlassian public repository contains all artifacts owned by Atlassian necessary to build a plugin for our products. It contains binaries, source and javadoc of our opensource components, and binaries and javadoc for our closed-source components.

-   <a href="https://packages.atlassian.com/maven/public" class="uri external-link">https://packages.atlassian.com/maven/public</a>
-   <a href="https://packages.atlassian.com/maven/public-snapshot" class="uri external-link">https://packages.atlassian.com/maven/public-snapshot</a>

It is contained in <a href="https://packages.atlassian.com/maven/repository/public" class="uri external-link">https://packages.atlassian.com/maven/repository/public</a>

{{% warning %}}

We are in the process of deprecating all <a href="https://maven.atlassian.com/" class="external-link">maven.atlassian.com</a> urls. If you are using any of those, please change them to a url mentioned above as soon as practical. We will update the developer community more widely when we expect to decommision the old <a href="http://maven.atlassian.com" class="external-link">maven.atlassian.com</a> urls permanently.

{{% /warning %}}

## Developing Plugins with Maven 3

Maven is included in the Atlassian SDK, so you do not normally need to install it yourself. However, the version that the SDK bundles is Maven 2.1.0. This may be an obstacle for some who prefer or need to use Maven 3.

In previous versions of the SDK (and as previously described on this page), you needed to add repository proxies and modify your Maven settings file to use the SDK with Maven 3. 

Now you can simply follow the steps on [Changing the Default Maven Version](/server/framework/atlassian-sdk/changing-the-default-maven-version) to use Maven 3 with the SDK.































































































































































































































































































































































