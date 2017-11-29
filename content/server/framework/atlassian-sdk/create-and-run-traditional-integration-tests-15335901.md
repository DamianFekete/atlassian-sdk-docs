---
title: Create and Run Traditional Integration Tests 15335901
aliases:
    - /server/framework/atlassian-sdk/create-and-run-traditional-integration-tests-15335901.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=15335901
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=15335901
confluence_id: 15335901
platform:
product:
category:
subcategory:
---
# Create and run traditional integration tests

This page explains the tools and processes you use in the Atlassian Plugin SDK, to create and run traditional integration tests for your plugin. The material on this page assumes you have already worked through or otherwise understand the information in [Create and Run Unit Tests](/server/framework/atlassian-sdk/create-and-run-unit-tests-15335878.html). 

## Overview of Integration Testing

Integration testing validates the interactions between an Atlassian host application (JIRA, Confluence, Stash, etc.) and your plugin. Traditional integration tests typically used Mockito to replicate or mock-up functions in the host. Now, Atlassian offers the Wired Test Framework for integration and unit testing.

The Wired Test Framework allows you to test your plugin in the actual host application environment rather than against mocked functions. Thus, for example, if your plugin creates an issue in JIRA by invoking the JIRA API, the Wired Test Framework lets you invoke your plugin and then test whether an issue was actually created in JIRA.  

If you have existing integration or functional tests, you can convert these to the new framework.  You also have the choice of continuing to use your traditional integration tests. And, of course, you can use both the traditional and wired integration test in the same plugin.

There are several ways to execute integration tests and review the results--from the command line or from the test console in the host application's UI. The command line approach as described here compiles the project, starts up the application and executes all the tests. When writing and tweaking the test code itself, this may not be the most efficient manner of working.

As an alternative, if you are using the Wired Test Framework, you can use the test console in the application. The test console lets you modify test code and rerun the individual test you are working on and see the results of the test without having to recompile the plugin and restart the application. This is usually the most efficient manner of working when you are developing and tweaking test code. (The test console is described [in the next page in this tutorial](/server/framework/atlassian-sdk/run-wired-tests-with-the-plugin-test-console-15335909.html)).  

### The atlas-integration-test Command

You use the `atlas-integration-test` command to run integration tests explicitly.  The command does the following:

-   executes your unit tests (unit tests are part of the `<test>` scope)
-   starts the host application configure in your `pom.xml` file's `<build>` section (for this tutorial JIRA)
-   loads the application with some default data 
-   executes your integration tests 

Just as with unit tests, the integration tests use Maven's Surefire plugin. Unlike unit tests, the `atlas-integration-test` command starts a host application environment.

### Test Configuration

By default, the system runs all the tests defined in your project's `it` package with the host application.  You can configure additional information in the `<build>` block of your `pom.xml` file through the `<configuration>` element. You can specify one or more &lt;products&gt; to test against.  You can also use the `<testGroups>` element to group integration tests.  The following example illustrates both elements:

``` xml
<build>
        <plugins>
            <plugin>
                <groupId>com.atlassian.maven.plugins</groupId>
                <artifactId>maven-jira-plugin</artifactId>
                <version>${amps.version}</version>
                <extensions>true</extensions>
                <configuration>
                    <products>
                        <product>
                            <id>jira</id>
                            <instanceId>jiraExpected</instanceId>
                            <productVersion>${jira.version}</productVersion>
                            <productDataVersion>${jira.version}</productDataVersion>
                        </product>
                    </products>
                    <testGroups>
                        <testGroup>
                            <id>jira-integration</id>
                            <productIds>
                                <productId>jira</productId>
                            </productIds>
                            <includes>
                                <include>it/**/*Test.java</include>
                            </includes>
                        </testGroup>
                    </testGroups>
                </configuration>
            </plugin>
... 
```

You can specify one or more `<product>` children in  `<products>` element. A &lt;product&gt; has the following fields:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>id</code></td>
<td><p>Can be one of:</p>
<ul>
<li><code>jira</code></li>
<li><code>confluence</code></li>
<li><code>bamboo</code></li>
<li><code>fecru</code></li>
<li><code>crowd</code></li>
<li><code>refapp</code></li>
<li><code>stash</code></li>
</ul></td>
</tr>
<tr class="even">
<td><code>instanceId</code></td>
<td>Unique identifier for this product definition.</td>
</tr>
<tr class="odd">
<td><pre><code>productVersion</code></pre></td>
<td>Version of the product to use.</td>
</tr>
<tr class="even">
<td><pre><code>productDataVersion</code></pre></td>
<td>Version of test data to use.</td>
</tr>
</tbody>
</table>

You can specify one or more `<testGroup>` children in  `<testGroups>` element.  A `<testGroup>` has the following fields:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Definition</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><code>id</code></td>
<td>Unique identifier for the test group.</td>
</tr>
<tr class="even">
<td><code>productIds</code></td>
<td><p>Contains one or more <code>&lt;productId&gt;</code> values:</p>
<ul>
<li><code>jira</code></li>
<li><code>confluence</code></li>
<li><code>bamboo</code></li>
<li><code>fecru</code></li>
<li><code>crowd</code></li>
<li><code>refapp</code></li>
<li><code>stash</code></li>
</ul>
<p>Alternatively, you can refer to a defined <code>&lt;instanceId&gt;</code> value from a <code>&lt;product&gt;</code> element.</p></td>
</tr>
<tr class="odd">
<td><code>includes</code></td>
<td>Contains one or more <code>&lt;include&gt;</code> values.</td>
</tr>
</tbody>
</table>

Through this configuration you can specify which tests to include in your integration tests and which products to run them against.   You can even configure the build to run multiple versions of the host application or more than one host application.  For example, you can run Confluence and JIRA together with your plugin tests. Or, you could run JIRA 5.0 and JIRA 4.0.  

``` xml
<configuration>
    <products>
        <product>
            <id>confluence</id>
            <instanceId>confluence-3.3.1</instanceId>
            <productVersion>3.3.1</productVersion>
            <productDataVersion>3.0</productDataVersion>
        </product>
        <product>
            <id>confluence</id>
            <instanceId>confluence-3.4.0</instanceId>
            <productVersion>3.4.0</productVersion>
            <productDataVersion>3.0</productDataVersion>
        </product>
        <product>
            <id>jira</id>
            <instanceId>jiraExpected</instanceId>
            <productVersion>${jira.version}</productVersion>
            <productDataVersion>${jira.version}</productDataVersion>
        </product>
    </products>
    <testGroups>
        <testGroup>
            <id>allConfluence</id>
            <productIds>
                <productId>confluence-3.3.1</productId>
                <productId>confluence-3.4.0</productId>
            </productIds>
            <includes>
                <include>it/**/confluence/*Test.java</include>
            </includes>
        </testGroup>
        <testGroup>
            <id>jira</id>
            <productIds>
                <productId>confluence-3.3.1</productId>
                <productId>confluence-3.4.0</productId>
            </productIds>
            <includes>
                <include>it/**/confluence/*Test.java</include>
            </includes>
        </testGroup>
        <testGroup>
            <id>jira-integration</id>
            <productIds>
                <productId>jira</productId>
            </productIds>
            <includes>
                <include>it/**/jira/*Test.java</include>
            </includes>
            </testGroup>
    </testGroups>
</configuration>
```

### Accessing Test Instances

During each test execution, the build system sets the following system properties for each product definition:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><strong>Property</strong></td>
<td><strong>Description</strong></td>
</tr>
<tr class="even">
<td><p><code>baseurl.instanceId</code></p></td>
<td><p>The base url of the application, e.g.</p>
<a href="http://localhost:8990/jira" class="uri external-link">http://localhost:8990/jira</a>
<p> </p></td>
</tr>
<tr class="odd">
<td><p><code>http.instanceId.port</code></p></td>
<td><p>The HTTP port that the application is listening on, e.g. <code>8990</code></p></td>
</tr>
<tr class="even">
<td><p><code>context.instanceId.path</code></p></td>
<td><p>The context path of the application, e.g. <code>/jira</code></p></td>
</tr>
</tbody>
</table>

Use these values to co-ordinate communication between your integration tests and running application instances.

## Step 1.  Run the Skeleton Integration Tests 

When you created the plugin, the system generated an integration test class for you, the `MyComponentWiredTest.java` file.  You can find this file in your project's `PLUGIN_HOME/src/test/java/it /com/atlassian/plugins/tutorials/jira/testTutorial` folder.  As the file's name implies, the generated test files assume you plan to use the Wired Test Framework rather than traditional integration tests.  This is really the recommended approach during the development phase.

However, you may have situations where you want to run your integration tests using traditional tools, from the command line.  One such situation would be if you are building your plugin with Bamboo.  In that case, you can still use the traditional Atlassian `atlas-integration-test` command-line interface.   The command executes only the `test` scope as defined in your `pom.xml` file (which also includes any unit tests you may have). Try the command now to run the generated test files:

1.  Go to a command line.
2.  Make sure you are in at the top level `PLUGIN_HOME` directory for you plugin.
3.  Enter the `atlas-integration-test` command:

    ``` bash
    atlas-integration-test
    ```

    Notice in command's output, the system runs the unit tests, starts the host application, and then runs your integration tests.  The command output should succeed with test output similar to the following:

    ``` bash
    -------------------------------------------------------
     T E S T S
    -------------------------------------------------------
    Running it.com.example.plugins.tutorial.jira.testTutorial.MyComponentWiredTest
    SLF4J: Failed to load class "org.slf4j.impl.StaticLoggerBinder".
    SLF4J: Defaulting to no-operation (NOP) logger implementation
    SLF4J: See http://www.slf4j.org/codes.html#StaticLoggerBinder for further details.
    [INFO] [talledLocalContainer] Nov 15, 2012 11:32:50 AM com.sun.jersey.server.impl.application.WebApplicationImpl _initiate
    [INFO] [talledLocalContainer] INFO: Initiating Jersey application, version 'Jersey: 1.8-atlassian-6 03/12/2012 02:59 PM'
    [INFO] [talledLocalContainer] Nov 15, 2012 11:32:51 AM com.sun.jersey.api.wadl.config.WadlGeneratorLoader loadWadlGenerator
    [INFO] [talledLocalContainer] INFO: Loading wadlGenerator com.sun.jersey.server.wadl.generators.WadlGeneratorApplicationDoc
    [INFO] [talledLocalContainer] Nov 15, 2012 11:32:51 AM com.sun.jersey.api.wadl.config.WadlGeneratorLoader loadWadlGenerator
    [INFO] [talledLocalContainer] INFO: Loading wadlGenerator com.sun.jersey.server.wadl.generators.WadlGeneratorGrammarsSupport
    [INFO] [talledLocalContainer] Nov 15, 2012 11:32:51 AM com.sun.jersey.api.wadl.config.WadlGeneratorLoader loadWadlGenerator
    [INFO] [talledLocalContainer] INFO: Loading wadlGenerator com.atlassian.plugins.rest.doclet.generators.resourcedoc.AtlassianWadlGeneratorResourceDocSupport
    Tests run: 1, Failures: 0, Errors: 0, Skipped: 0, Time elapsed: 3.185 sec
    Results :
    Tests run: 1, Failures: 0, Errors: 0, Skipped: 0
    ```

    When you next run your plugin with `atlas-run`, the command also runs both your unit and integration tests.  If the build were to fail on unit or integration tests, the application does not start.

## Step 2.  Create a Traditional Integration Test 

You may have existing traditional integration tests you want to maintain for some time.  You can still do so. The difference between traditional tests and wired tests is the use of the `AtlassianPluginsTestRunner`.  If your tests omit the `@RunWith(AtlassianPluginsTestRunner.class)` annotation, they are treated as traditional integration tests. Try adding a traditional integration test. If you haven't already done so, start Eclipse and open the testTutorial project you created.

1.  Go to the `PLUGIN_HOME/src/test/java/it/com/atlassian/plugins/tutorials/jira/testTutorial` folder.
2.  Create a  `MyComponentTrdTest.java` file.
3.  Edit the file and add the following code:

    ``` java
    import static org.junit.Assert.assertEquals;
    import org.junit.Test;
     
    public class MyComponentTrdTest
    {
        @Test
        public void testSomeFailure()
        {
            System.out.println("I RAN But failed...");
            assertEquals("something failed","blah","boo");
        }
    }
    ```

4.  Save and close the file. 

## Step 3.  Configure Test Groups

When your tests run, Surefire creates a `PLUGIN_HOME/target/testgroupname` directory to hold temporary files during the test generation and reports. At this point, you haven't defined any test groups.  So, Surefire created a `PLUGIN_HOME/target/group-__no_test_group__` directory.  Test groups are useful if you are running a lot of integration tests.   You can create test groups that represents categories in your tests. Try this now.

While still in Eclipse and do the following to define a `<testGroup>` for your integration tests.

1.  Open your `PLUGIN_HOME/pom.xml` file.
2.  Locate the `<build>` section.  
    This section lists each plugin you are building.   You are using a built-in Atlassian Maven plugin to run your plugin build.  Locate the plugin with the `<groupId>` of `com.atlassian.maven.plugins` you should see the following:

    ``` xml
    <plugin>
        <groupId>com.atlassian.maven.plugins</groupId>
        <artifactId>maven-jira-plugin</artifactId>
        <version>${amps.version}</version>
        <extensions>true</extensions>
        <configuration>
            <productVersion>${jira.version}</productVersion>
            <productDataVersion>${jira.version}</productDataVersion>
        </configuration>
    </plugin>
    ```

3.  Define a `<testGroups>` section with two `<testGroup>` elements inside the configuration:

    ``` xml
    <plugin>
        <groupId>com.atlassian.maven.plugins</groupId>
        <artifactId>maven-jira-plugin</artifactId>
        <version>${amps.version}</version>
        <extensions>true</extensions>
        <configuration>
            <productVersion>${jira.version}</productVersion>
            <productDataVersion>${jira.version}</productDataVersion>
            <testGroups>
                <testGroup>
                    <id>wired-integration</id>
                    <productIds>
                        <productId>jira</productId>
                    </productIds>
                    <includes>
                        <include>it/**/*WiredTest.java</include>
                    </includes>
                </testGroup>
                <testGroup>
                    <id>traditional-integration</id>
                    <productIds>
                        <productId>jira</productId>
                    </productIds>
                    <includes>
                        <include>it/**/*TrdTest.java</include>
                    </includes>
                </testGroup>
            </testGroups>
        </configuration>
    </plugin> 
    ```

    You defined a test group consisting of all the test files ending with `WiredTest` and another for traditional tests `TrdTest`. If you have multiple `<testGroups>` defined, you can run a subset of those groups by using the `-DtestGroups=groupname` flag on the command line.  

4.  Save and close the file.
5.  Re-run `atlas-integration-tests` but only for the traditional tests.``

    ``` bash
    atlas-integration-test -DtestGroups=traditional-integration
    ```

    Surefire creates the `PLUGIN_HOME/target/group-traditional-integration` directory

6.  Change directory to `PLUGIN_HOME/target/group-traditional-integration/tomcat6x/surefire-reports `directory.
7.  List the directory contents.  
    You should see something simliar to the following:

    ``` bash
    TEST-it.com.example.plugins.tutorial.jira.testTutorial.MyComponentTrdTest.xml       
    it.com.example.plugins.tutorial.jira.testTutorial.MyComponentTrdTest.txt
    ```

    Take some time and browse the contents of each file.

8.  Try the command again without the `-D` flag.  
    Surefire creates a directory for each group.

## Next Steps

In this page and the previous, you learned how to build, configure, and run tests.  All the testing is run from the command line, this can make the development process time consuming and awkward. In the next section, you learn how [to use wired test together with the test console](/server/framework/atlassian-sdk/run-wired-tests-with-the-plugin-test-console-15335909.html) to test your code and speed up development.

 

























