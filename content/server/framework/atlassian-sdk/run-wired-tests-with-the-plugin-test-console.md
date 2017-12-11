---
aliases:
- /server/framework/atlassian-sdk/run-wired-tests-with-the-plugin-test-console-15335909.html
- /server/framework/atlassian-sdk/run-wired-tests-with-the-plugin-test-console-15335909.md
category: devguide
confluence_id: 15335909
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=15335909
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=15335909
date: '2017-12-11'
guides: tutorials
legacy_title: Run Wired Tests with the Plugin Test Console
platform: server
product: atlassian-sdk
subcategory: learning
title: Run Wired Tests with the Plugin Test Console
---
# Run Wired Tests with the Plugin Test Console

In previous pages in this tutorial, you learned how to use JUnit to construct unit tests, how to configure and run your traditional integration tests, and how to use the `atlas-` commands to run tests. On this page, you learn how to speed up and simplify plugin development using the Atlassian Wired Test Framework and the Plugin Test Console.

## Overview of the Atlassian Wired Test Framework

While the` atlas-unit-test` and `atlas-integration-test `commands allow you to run tests from the command line, neither allowed for a fast development process. The Atlassian Wired Test Framework lets you test your plugin in the context of the host Atlassian product. (In contrast, the traditional plugin testing framework required the use of a host-mocking framework, such as Mockito.)

An additional advantage of the framework is that it facilitates faster test development. Instead of recompiling your plugin and restarting the host application every time you make a change to a test, you can use the test console to re-run the test, without having to recompile and restart the host.  

Running as a plugin in product has several advantages:

-   Test code is deployed as a plugin bundle in the same OSGI-fied Tomcat container as the host application.
-   Your code can use all the JUnit functionality and any additional functionality you would be able to do in non-test plugin.
-   Dependencies in your test code are "wired" by Spring inside the container.
-   Test code runs in the product container and reports back to the locally running JUnit.
-   Tests results display in the Plugin Test Console in addition to Surefire reports. 

Finally, since your tests are running in the product, you can test your plugins in a more realistic context.

### JUnit Enhancements for Wired Tests

The Atlassian Wired Test Framework includes some enhancements that causes difference in how you use JUnit annotation inside of Atlassian Wired Tests. The following table lists these differences.

 

-   **Standard JUnit Test**: Requires a single zero-argument, public constructor.
-   **Atlassian Wired Test**: Can use constructor for dependency injection.  
      
-   **Standard JUnit Test**: Tests are stateless and every method is run on its own instance of the test class.
-   **Atlassian Wired Test**: Tests are stateful. All methods run on the same test class instance. You must be careful to clean up any data at the end of your methods!  
      
-   **Standard JUnit Test**: `@BeforeClass` and `@AfterClass` must annotate a `public static void` method.
-   **Atlassian Wired Test**: `@BeforeClass` and `@AfterClass `must ***not*** annotate a static method. These methods ***should*** annotate a `public void` method.

 

The `@Before` and `@After` annotations remain the same both in standard and wired tests; they annotate `public void` methods.

## Step 1.  Check for the Wired Dependencies

If you have followed along through this tutorial, you should already have the correct dependencies in your `pom.xml`.  If you are upgrading a `pom.xml` file you used from a pre-existing project, you may need to add dependencies to it.  Regardless, it is good to check your dependencies. 

1.  Navigate to the top of your project's `PLUGIN_HOME`.
2.  Open the `pom.xml` file.
3.  Make sure you have the following wired test dependencies:

    ``` xml
    <dependencies>
    ....

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

    Specifying the `jsr311-api` and `gson` dependencies overrides the transitive versions Maven would have fetched.

4.  Make sure that your JUnit dependency is set to 4.10 or higher:

    ``` xml
    <dependency>
      <groupId>junit</groupId>
      <artifactId>junit</artifactId>
      <version>4.10</version>
      <scope>test</scope>
    </dependency>
    ```

5.  Make your project `<properties>` include the following values:

    ``` xml
    <amps.version>4.1</amps.version>
    <plugin.testrunner.version>1.1</plugin.testrunner.version>
    ```

6.  Save any changes you made and close the file.

## Step 2. Examine the atlassian-plugin.xml File for Your Tests

Remember, your wired tests get bundled together as a plugin.  Like any other Atlassian plugin, your test suite needs a plugin descriptor file (`atlassian-plugin.xml`).  The descriptor lists any components or modules needed by your integration tests.  At runtime, Spring examines this plugin file and wires in the modules needed by your tests.

The Plugins Test Console always runs and displays results from wired tests. It can also run and display the results of unit tests and traditional integration tests. It can do this only if your descriptor file also includes any resources need by these tests as well.  For example, unit tests typically have dependencies on the base plugin.  So, your descriptor should make sure to include any base plugin dependencies.

If you are following along with this tutorial, the `atlassian-plugin.xml` descriptor file was created for you in the  `P``LUGIN_HOME/src/test/resources` directory. To convert, a pre-4.1 SDK existing project over to using the Wired Test Framework, you'll need to add this file yourself.   Take a moment to familiarize yourself with the test descriptor file and how it differs from your standard descriptor.

1.  Navigate to your project's `PLUGIN_HOME/src/test/resources` directory.
2.  `Open the atlassian-plugin.xml` file.  
    It should look similar to the following:

    ``` xml
    <atlassian-plugin key="${project.groupId}.${project.artifactId}-tests" name="${project.name}" plugins-version="2">
       <plugin-info>
            <description>${project.description}</description>
            <version>${project.version}</version>
            <vendor name="${project.organization.name}" url="${project.organization.url}" />
        </plugin-info>
      <!-- from our base plugin -->
      <component-import key="myComponent" interface="com.example.plugins.tutorial.jira.testTutorial.MyPluginComponent"/>
      <!-- from the product container -->
       <component-import key="applicationProperties" interface="com.atlassian.sal.api.ApplicationProperties" />

    </atlassian-plugin>
    ```

3.  Note that your test project `key` is different from your project's `key`.  
    The test `key` has a  `-tests` identifier at the end of the plugin key as follows:

    ``` xml
    <atlassian-plugin key="${project.groupId}.${project.artifactId}-tests" name="${project.name}" plugins-version="2">
     ...
    ```

    This identifier distinguishes your test bundle from your project bundle in the OSGI container. 

4.  Locate the `component-import` from the base plugin.  
    You'll recall that your `MyComponentWiredTest.java` file tests a method on your base plugin. This import tells Spring that your test bundle needs an interface from another bundle, the plugin. 
5.  Locate the `component-import` from the product  container.  
    Your wired test relies on the Shared Access Layer (SAL).  This is a component common to all Atlassian applications. So, here you are just telling Spring to wire in SAL as well. 
6.  Close the file.

You may want specific modules in your test plugin that you don't have in your main plugin. If that is the case, you would add them to this descriptor rather than your main descriptor.  Any dependencies you need to declare to support the component-imports would go into your `pom.xml` file.

## Step 3.   Launch the Application and the Plugin Test Console

Now, you are ready to run the host application and view your tests in the Plugin Test Console.

1.  Open a command or terminal window.
2.  Change directory to the `PLUGIN_HOME` directory.
3.  Start the application with the `atlas-debug` command.

    ``` bash
    atlas-debug
    ```

    When the command succeeds, it displays the URL for the host application:

    ``` bash
    ...
    [INFO] jira started successfully in 106s at http://localhost:2990/jira
    [INFO] Type Ctrl-D to shutdown gracefully
    [INFO] Type Ctrl-C to exit
    ```

4.  Copy and paste the URL into your browser's address field.
5.  The browser displays the host application, in the case of this tutorial, JIRA. 
6.  Enter `admin` for both the **User** and the **Password**.
7.  Display the Developer Toolbar by clicking on the arrow in the lower left corner of your browser.
8.  Click **Toolbox &gt; Plugin Test Console**.  
    The test console appears. The console lists the type of tests it found in your project.
9.  Press **Rerun all 3 test classes** to run your tests and display their results:  
    <img src="/server/framework/atlassian-sdk/images/test-run.png" width="700" />   
      

## Step 4. Make a Change to Your Running Test Suite

Like any other Atlassian plugin, you can use the FastDev feature with your test plugin.  Try this now:

1.  Leave the **Plugin Test Console** running in your browser.
2.  Edit the `MyComponentWiredTest` class.
3.  Add the `@Ignore` annotation to the `testMyName()` method.
4.  Add the Ignore import to the test file:

    ``` bash
    import org.junit.Ignore;
    ```

5.  Save the test file.
6.  Return to the **Plugin Test Console**.
7.  Press the play button next to the test you changed.  
    The system recognizes that you changed the underlying tests. It launches FastDev to rebuild your test plugin:  
    <img src="/server/framework/atlassian-sdk/images/testfastdev.png" width="700" />  
    When the build completes, the system returns you to the Plugin Test Console.  
8.  Now try changing a unit test or a traditional integration tests.  
    Just as with wired tests, the system recognizes the changes and launches FastDev.

## Next Steps

This page taught you how to code using the Atlassian Wired Test Framework.  Tests that use this framework are plugins that use Spring dependency injection to run inside an Atlassian host application.  When you use the framework, you have access to the Plugin Test Console.  This console allows you to run test and view their results right in the application.  When your underlying test code changes, the system recognizes the change and launches FastDev to rebuild your tests.

At this point, all you really need is some test data. In the next section, you learn [how to seed your host application with test data](/server/framework/atlassian-sdk/create-test-data-and-a-test-fixture).
































































































































































