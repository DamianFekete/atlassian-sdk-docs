---
title: Obsolete Atlassian Maven Pdk 2818711
aliases:
    - /server/framework/atlassian-sdk/obsolete-atlassian-maven-pdk-2818711.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818711
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818711
confluence_id: 2818711
platform:
product:
category:
subcategory:
---
# Documentation : Obsolete Atlassian Maven PDK

{{% warning %}}

These instructions are obsolete if you are using the <a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Developing+your+Plugin+using+the+Atlassian+Plugin+SDK&amp;linkCreation=true&amp;fromPageId=2818711" class="createlink">Atlassian Plugin SDK</a> (and you should be). Leaving here only as reference for those using very old products which do not support the SDK.

{{% /warning %}}

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Name</p></td>
<td><p>Atlassian Plugin Developer Kit for Maven2</p></td>
</tr>
<tr class="even">
<td><p>Vendor</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Author(s)</p></td>
<td><p>Dan Hardiker, Michael Mekaail, Tony Truong, David Peterson, Kevin Ross</p></td>
</tr>
<tr class="even">
<td><p>Homepage</p></td>
<td><p><a href="/server/framework/atlassian-sdk/obsolete-atlassian-maven-pdk-2818711.html">Obsolete Atlassian Maven PDK</a></p></td>
</tr>
<tr class="odd">
<td><p>Issue Tracking</p></td>
<td><p><a href="http://developer.atlassian.com/jira/browse/CPDK" class="uri external-link">http://developer.atlassian.com/jira/browse/CPDK</a></p></td>
</tr>
<tr class="even">
<td><p>Categories</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Version</p></td>
<td><p>2.1.6</p></td>
</tr>
<tr class="even">
<td><p>Availability</p></td>
<td><p>All</p></td>
</tr>
<tr class="odd">
<td><p>State</p></td>
<td><p>Stable</p></td>
</tr>
<tr class="even">
<td><p>License</p></td>
<td><p>Apache 2</p></td>
</tr>
<tr class="odd">
<td><p>Price</p></td>
<td><p>Free</p></td>
</tr>
<tr class="even">
<td><p>Java API Docs</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Download Source</p></td>
<td><p><a href="http://svn.atlassian.com/svn/public/contrib/maven-plugins/com.atlassian.maven.plugins/atlassian-pdk/tags/atlassian-pdk-2.1.6" class="external-link">Subversion</a></p></td>
</tr>
<tr class="even">
<td><p>Download JAR</p></td>
<td><p><a href="https://maven.atlassian.com/contrib/com/atlassian/maven/plugins/atlassian-pdk/2.1.6/atlassian-pdk-2.1.6.jar" class="external-link">atlassian-pdk-2.1.6.jar</a></p></td>
</tr>
</tbody>
</table>

## Description/Features

This is a Maven 2 plugin which assists in building and deploying Atlassian plugins.

## Installation

To start, you must be using Maven 2.0.9 or later.

Maven automatically downloads plugins that are configured in your pom and installs them into its repository when you use them. If you use Atlassian's [plugin archetypes](/server/framework/atlassian-sdk/atlassian-plugin-archetypes-2818678.html) to create your plugin, you should not have to do anything else to install the Atlassian PDK.

{{% note %}}

Manual Installation

Sometimes automatic install doesn't work. If so, try this:

-   Download the latest version of the PDK, listed above.
-   Install it to your maven repository by running this command from the directory where the downloaded JAR resides:  
    `mvn install:install-file -DgroupId=com.atlassian.maven.plugins -DartifactId=atlassian-pdk -Dpackaging=jar -Dfile=atlassian-pdk-2.1.6.jar -Dversion=2.1.6`
-   Create an issue in the <a href="http://developer.atlassian.com/jira/browse/CPDK" class="external-link">Developer Network CPDK JIRA project</a> to let us know the details of the problem you encountered so we can fix it or improve these instructions.

{{% /note %}}

## Configuration

There are several properties which should be specified in your local `settings.xml` file which are used by this plugin. These are all noted in the [Example settings.xml](/server/framework/atlassian-sdk/example-settings.xml-2818713.html) file.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Property Name</p></th>
<th><p>Default</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>atlassian.pdk.server.url</strong></p></td>
<td><p><em>None</em></p></td>
<td><p>The URL for the base address of the Confluence server the plugin should be installed on e.g., <code>'http://localhost:8080'</code>.</p></td>
</tr>
<tr class="even">
<td><p><strong>atlassian.pdk.server.username</strong></p></td>
<td><p><em>None</em></p></td>
<td><p>The username to log in as when installing. This user must have administration privillages on the server.</p></td>
</tr>
<tr class="odd">
<td><p><strong>atlassian.pdk.server.password</strong></p></td>
<td><p><em>None</em></p></td>
<td><p>The password to log in with when installing.</p></td>
</tr>
</tbody>
</table>

{{% note %}}

Speeding Up Confluence Plugin Development

Looking for for faster turnaround times in Confluence plugin development? Try the guide to [Speeding Up Confluence Plugin Development Using Maven CLI](/server/framework/atlassian-sdk/speeding-up-confluence-plugin-development-using-maven-cli-2818680.html).

{{% /note %}}

## Usage

#### mvn package

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Command</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>mvn package</code></p></td>
<td><p>Creates a <strong>Jar</strong> in the target directory with any dependencies your plugin depends on.</p></td>
</tr>
</tbody>
</table>

### Variables

#### `extractDependencies`

**Type:** boolean  
**Default:** `false`

Atlassian plugins often needs other libraries as dependencies. In Confluence, you can include dependent JARs *inside* your plugin, and the default atlassian-plugin package is configured to do this. Any dependency that you specify in your POM will be included inside the META-INF/lib of your plugin jar.

However, JIRA plugins cannot yet do the same thing, so it is necessary to explode your dependent JARs, and include their classes and resources inside your plugin. By specifying `extractDependencies=true` the Atlassian PDK can do this for you.

**Note:** Any dependency that has a `<scope>compile</scope>` or `<scope>runtime</scope>` will be packaged in the final JAR. All other dependencies will be ignored. To exclude particular dependencies, use the `provided` scope, which indicates that the environment is expected to provide the library at runtime.

#### `installMethod`

**Type:** text  
**Options:** `upload` or `copy`**Default:** upload

Confluence allows plugins to be uploaded directly into a running instance of the server. JIRA, Bamboo and the other Atlassian products do not yet allow this. If building a plugin for those servers you will need to specify that the plugin should be installed via `copy`.

If you do, you also need to specify the `pluginsHome` option to tell the PDK where to copy to.

#### `pluginsHome`

**Type:** text  
**Default:** N/A

This defines the location that the plugin will be copied to. Typically, this is something like this:

``` javascript
<pluginsHome>${jira.webapp.path}/WEB-INF/lib</pluginsHome>
```

The `${jira.webapp.path`} value is set in your `settings.xml` file and points to the absolute path to your local JIRA server. Substitute 'bamboo', 'fisheye', etc for other application servers.

## Plugin Goals

The following goals manage the plugin's installation in a specified Confluence server.

-   `atlassian-pdk:disable`: Disables the current plugin in the server specified in `atlassian.pdk.server.url`.
-   `atlassian-pdk:enable`: Disables the current plugin in the server specified in `atlassian.pdk.server.url`.
-   `atlassian-pdk:install`: Packages the plugin, uninstalls any existing copies, and installs the new version to the server specified in `atlassian.pdk.server.url`.
-   `atlassian-pdk:uninstall`: Uninstalls the current plugin from the server specified in `atlassian.pdk.server.url`, if it exists.
-   `atlassian-pdk:rescan`: Asks the server specified in `atlassian.pdk.server.url` to rescan the plugins directory for new plugins. *(Note: this has basically no effect since Confluence 2.5, due to plugins being stored in the database from that version onwards)*

## Version History

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>2.1.6</p></td>
<td><p><a href="http://developer.atlassian.com/jira/sr/jira.issueviews:searchrequest-xml/temp/SearchRequest.xml?pid=10211&amp;fixfor=11770&amp;sorter/field=issuekey&amp;sorter/order=DESC&amp;tempMax=20" class="external-link">Release Notes</a></p></td>
</tr>
<tr class="even">
<td><p>2.1.5</p></td>
<td><p><a href="http://developer.atlassian.com/jira/sr/jira.issueviews:searchrequest-xml/temp/SearchRequest.xml?&amp;pid=10211&amp;fixfor=11688&amp;sorter/field=issuekey&amp;sorter/order=DESC&amp;tempMax=20" class="external-link">Release Notes</a></p></td>
</tr>
<tr class="odd">
<td><p>2.1.2</p></td>
<td><p><a href="http://developer.atlassian.com/jira/sr/jira.issueviews:searchrequest-xml/temp/SearchRequest.xml?&amp;pid=10211&amp;fixfor=11543&amp;sorter/field=issuekey&amp;sorter/order=DESC&amp;tempMax=20" class="external-link">Release Notes</a></p></td>
</tr>
</tbody>
</table>


















































































































































































































































































































