---
aliases:
- /server/framework/atlassian-sdk/generate-and-examine-skeleton-tests-15335867.html
- /server/framework/atlassian-sdk/generate-and-examine-skeleton-tests-15335867.md
category: devguide
confluence_id: 15335867
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=15335867
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=15335867
date: '2017-12-08'
guides: tutorials
legacy_title: Generate and Examine Skeleton Tests
platform: server
product: atlassian-sdk
subcategory: learning
title: Generate and Examine skeleton tests
---
# Generate and Examine skeleton tests

When you generate a new plugin with an `atlas-create-application-plugin` command, the generated plugin skeleton includes skeleton tests.  This page walks you through the process of generating the plugin skeleton and its tests.  It also introduces you to the project components the tests rely on.  

## Backgrounder:  Supported Plugin Test Types

You can and should test plugins using the same types of tests as you would for other software. In general, the different types of tests fall into these categories:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Type</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>unit</td>
<td>Test on a distinct unique of work within the plugin such as a single method or function.</td>
</tr>
<tr class="even">
<td>integration</td>
<td><p>Tests the interactions between the plugin and the plugin's target environment. In the case of an Atlassian plugin, the target environment is the host application. Integration tests can also include or rely on other external, services.</p>
<p>Atlassian supports traditional integration tests and wired integration tests. Wired integration tests are bundled as a plugin and run directly in the host application. You'll learn more about creating wired integration tests later in this tutorial.</p></td>
</tr>
<tr class="odd">
<td>functional</td>
<td>Tests the functionality of the application's features and functions.</td>
</tr>
<tr class="even">
<td>stress</td>
<td>Tests how the application performs under a large number of requests within a given period.</td>
</tr>
<tr class="odd">
<td>acceptance</td>
<td>Tests how well the application meets a customer's needs.</td>
</tr>
</tbody>
</table>

Unit and integration tests test your plugin's internal structures or functions.  Atlassian provides you with a plugin test skeleton and a tools for unit and integration testing.  Often, you can combine functional tests with your integration tests.  In some cases, Atlassian host applications supply functional test libraries that you can leverage in developing your own tests.

The stress and acceptance tests require you to write specifications or build systems specific to your plugin and its requirements.   Atlassian does not provide tools, processes, or infrastructures for these test types but we do encourage you to do them on your own.

## Step 1. Create a Plugin Skeleton

In this step, you create a simple plugin skeleton and import it into the Eclipse IDE.  You can create a skeleton for any of the Atlassian host applications.  This tutorial uses JIRA.

{{% note %}}

Do I have to Use Eclipse?

If you aren't interested in using Eclipse and prefer another IDE, you are perfectly free to use another. However, the tutorial assumes you are using Eclipse.

{{% /note %}}

Do the following to generate the plugin skeleton and its tests resources:

1.  Open a terminal and navigate to your Eclipse workspace directory.
2.  Enter the following command to create a JIRA plugin skeleton:

    ``` bash
    atlas-create-jira-plugin
    ```

    When prompted, enter the following information to identify your plugin:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Create a plugin for?</p></td>
    <td><p>Enter a JIRA version</p></td>
    </tr>
    <tr class="even">
    <td><p>group-id</p></td>
    <td><p><code>com.example.plugins.tutorial.jira</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>artifact-id</p></td>
    <td><p><code>testTutorial</code></p></td>
    </tr>
    <tr class="even">
    <td><p>version</p></td>
    <td><p><code>1.0-SNAPSHOT</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>package</p></td>
    <td><p><code>com.example.plugins.tutorial.jira.testTutorial</code></p></td>
    </tr>
    </tbody>
    </table>

3.  Confirm your entries when prompted.
4.  Change to the `testTutorial` directory created by the previous step.
5.  Run the command:

    ``` bash
    atlas-mvn eclipse:eclipse
    ```

    You should repeat this command after you add a dependency to your `pom.xml` file. It ensures that Eclipse populates your project dependencies correctly. 

6.  Start Eclipse.
7.  Select **File-&gt;Import**.   
    Eclipse launches the **Import** wizard.
8.  Filter for **Existing Projects into Workspace** (or expand the **General** folder tree).
9.  Press **Next** and enter the root directory of your workspace.   
    Your Atlassian plugin folder should appear under **Projects**.
10. Select your plugin and click **Finish**.   
    Eclipse imports your project.

## Step 2. Review the Generated Test Structure

The `atlas-create-jira-plugin` command creates test directories and skeleton test files.   Most `atlas-create-application-plugin` commands create the following directories:

 

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Directory</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr class="even">
<td><code>PLUGIN_HOME/src/test/java/it</code></td>
<td>Place integration tests here. You must package all your integration tests in a package that begins with the <code>it</code> prefix.</td>
</tr>
<tr class="odd">
<td><code>PLUGIN_HOME/src/test/java/ut</code></td>
<td>Place unit test here. You must package all your unit tests in a package that begins with the <code>ut</code> prefix.</td>
</tr>
<tr class="even">
<td><p><code>PLUGIN_HOME/src/test/resources</code></p></td>
<td>Place resource test files here.</td>
</tr>
</tbody>
</table>

Not all  `atlas-create-application-plugin` commands generate these directories. If you use a command that does not generate these directories, create them yourself.

Along with the test directory structure, most `atlas-create-application-plugin` commands generate skeleton test files.  For this tutorial, the generation step created these additional files:  

-   `PLUGIN_HOME/src/test/java/it/com/example/plugins/tutorial/jira/testTutorial/MyComponentWiredTest.java`
-   `PLUGIN_HOME/src/test/java/ut/com/example/plugins/tutorial/jira/testTutorial/MyComponentUnitTest.java`
-   `PLUGIN_HOME/src/test/resources/atlassian_plugin.xml`

The wired integration tests rely on the descriptor file (`atlassian_plugin.xml`). You'll learn more about this later in the tutorial. 

Take some time and open the generated test files.  The Java files contain simple classes that you can expand on as you work.  If you use the `atlas-create-application-plugin-module` commands to add plugin modules, you may find the commands generate additional files in these folders.  

## Step 3. Review the pom.xml Test Dependencies

Typically, your `pom.xml` file contains three elements related to test dependencies.

### The JUnit Dependency

In the previous step, you may have noticed that all of your plugin test files import a `org.junit.Test` class. JUnit is a widely-used testing framework supported for testing Atlassian plugins. When you generate a plugin, the  `pom.xml` file includes a dependency on JUnit 4.10:

``` xml
<dependency>
       <groupId>junit</groupId>
       <artifactId>junit</artifactId>
       <version>4.10</version>
       <scope>test</scope>
</dependency>
```

The scope of this dependency limits the availability of JUnit only to the project test compilation and execution phases.  If you are packaging a plugin, you need not remove your tests files as the test dependencies do not load at runtime in a production system.

### Testrunner Dependencies

Look for the wired test runner dependencies further down the page.  These look like the following:

``` xml
 <!-- WIRED TEST RUNNER DEPENDENCIES -->
  <dependency>
     <groupId>com.atlassian.plugins</groupId>
     <artifactId>atlassian-plugins-osgi-testrunner</artifactId>
     <version>${plugin.testrunner.version}</version>
     <scope>test</scope>
  </dependency>
  <dependency>
     <groupId>javax.ws.rs</groupId>
     <artifactId>jsr311-api</artifactId>
     <version>1.1.1</version>
     <scope>provided</scope>
  </dependency>
  <dependency>
     <groupId>com.google.code.gson</groupId>
     <artifactId>gson</artifactId>
     <version>2.2.2-atlassian-1</version>
  </dependency>
 </dependencies>
```

Your integration tests can make use of these dependencies to write in-product, wired integration tests.

### Product-specific Dependencies

Depending on which host application you are using, Jira, Confluence, etc., your `pom.xml` file may contain dependencies in addition to JUnit.  The dependencies can be on third-party test frameworks, like Mockito, or to Atlassian test suites. The JIRA generated `pom.xml` includes two additional dependencies:

``` xml
<dependency>
      <groupId>com.atlassian.jira</groupId>
      <artifactId>jira-tests</artifactId>
      <version>${jira.version}</version>
      <scope>test</scope>
</dependency>
<dependency>
      <groupId>com.atlassian.jira</groupId>
      <artifactId>jira-func-tests</artifactId>
      <version>${jira.version}</version>
      <scope>test</scope>
</dependency> 
```

The `jira-tests` artifact contains the JIRA Unit tests.  The `jira-func-tests`, like the name sounds, contains the JIRA functional tests.  When you write your tests, you can access these artifacts from your own unit, integration, and functional tests.  The application-specific sections of this site contain information on these resources. The last page of this tutorial explains where those are.

## Next Step

So far, you've learned about the generated structure created for you when you run an `atlas-create-application-plugin` command.  This structure includes test directories, files, and dependencies. This is code that Atlassian generates for all plugin developers automatically.  In the next section, you [write a simple unit test, execute the test in your plugin, and review the results](/server/framework/atlassian-sdk/create-and-run-unit-tests) of the test.










































































































































































































