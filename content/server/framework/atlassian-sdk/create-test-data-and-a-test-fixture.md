---
aliases:
- /server/framework/atlassian-sdk/create-test-data-and-a-test-fixture-15335913.html
- /server/framework/atlassian-sdk/create-test-data-and-a-test-fixture-15335913.md
category: devguide
confluence_id: 15335913
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=15335913
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=15335913
date: '2017-12-08'
guides: tutorials
legacy_title: Create Test Data and a Test Fixture
platform: server
product: atlassian-sdk
subcategory: learning
title: Create test data and a test fixture
---
# Create test data and a test fixture

Most tests, and in particular integration tests, rely on sample data for testing.  You need sample data in the host application and may also need sample data specific to your plugin. This page explains how to populate your test instance with data for testing.

## Initial Test Application Configuration

For testing purposes, Atlassian stores a configuration for each host application in Atlassian's Maven repository. This data is a zip archive of a fully configured application's home directory.  The `home` directory includes database properties, search indexes, caches, and more. If you are using the embedded HSQLDB database supplied for evaluation purposes, the database files are also stored in this directory.

The host configuration your plugin uses is specified in the `pom.xml` file through the `<productDataVersion>` value.  This value is set automatically for you when you generate a project.  When you first start the application and load your plugin, the `atlas`- commands download the specified `<productDataVersion>`, unzip it, and use it to seed the `PLUGIN_HOME/target/application/home` directory.  

The following table lists the repository location for each test configuration:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p><strong>Product</strong></p></th>
<th><p><strong>Artifact ID with Link to Maven Repo</strong></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>JIRA</p></td>
<td><p><a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/jira/plugins/jira-plugin-test-resources/" class="external-link">jira-plugin-test-resources</a></p></td>
</tr>
<tr class="even">
<td><p>Confluence</p></td>
<td><p><a href="https://maven.atlassian.com/public/com/atlassian/confluence/plugins/confluence-plugin-test-resources/" class="external-link">confluence-plugin-test-resources</a></p></td>
</tr>
<tr class="odd">
<td><p>Bamboo</p></td>
<td><p><a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/bamboo/plugins/bamboo-plugin-test-resources/" class="external-link">bamboo-plugin-test-resources</a></p></td>
</tr>
<tr class="even">
<td><p>Crowd</p></td>
<td><p><a href="https://maven.atlassian.com/public/com/atlassian/crowd/distribution/crowd-plugin-test-resources/" class="external-link">crowd-plugin-test-resources</a></p></td>
</tr>
<tr class="odd">
<td><p>FishEye/Crucible</p></td>
<td><p><a href="https://maven.atlassian.com/public/com/atlassian/fecru/amps-fecru/" class="external-link">amps-fecru</a></p></td>
</tr>
<tr class="even">
<td>Stash</td>
<td><a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/stash/stash-plugin-test-resources/" class="external-link">stash-plugin-test-resources</a>  </td>
</tr>
</tbody>
</table>

The product configuration data does not *have* to match the application version you are testing. In many cases, you can use an older `<productDataVersion>`. For example, you can specify a `<productDataVersion>` of 3.1 but write a plugin for Confluence 3.2.  When you start the Confluence 3.2 with an `atlas-` command, the system automatically updates the 3.1 data to 3.2.  

 To the initial host configuration, you may want to add a set of test data that you use in testing.  You might store some test data your in your project's `PLUGIN_HOME/src/test/resources` directory. Other tests, especially integration and functional tests, can require data to exist in the host application itself.  For example, a JIRA project and issues or pages and a space for Confluence.  

The combination of the host application and an initial data set would form the basis of a *test fixture*. You use a test fixture to ensure that your plugin is tested against a well known and fixed environment every time the test suite runs.  Then, problems that occur in a test run are either the result of problems in your code -- plugin or test code.  The rest of this article, explains how to create an initial set of test data.  

## Step 1. Know your Project Data Version

In this step, you check your `pom.xml` and verify the data version you want to use for your tests. If you are following along the tutorial exactly, go ahead and launch the Eclipse IDE.  Otherwise, use your favorite editor to do the following:

1.  Edit the `pom.xml` file.
2.  Locate the `<build>` section of the file.
3.  Locate the `<configuration>` for the `com.atlassian.maven.plugins`.
4.  Make sure you have a `<productDataVersion>` defined.  
    If you have followed along with this tutorial, you should seem something like the following:

    ``` xml
       <build>
          <plugins>
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
                         <includes>
                            <include>it/**/*WiredTest.java</include>
                         </includes>
                      </testGroup>
                      <testGroup>
                         <id>traditional-integration</id>
                         <includes>
                            <include>it/**/*TrdTest.java</include>
                         </includes>
                      </testGroup>
                   </testGroups>
                </configuration>
             </plugin>
             <plugin>
                <artifactId>maven-compiler-plugin</artifactId>
                <configuration>
                   <source>1.6</source>
                   <target>1.6</target>
                </configuration>
             </plugin>
          </plugins>
       </build>
    ```

5.  Check the `<productDataVersion>` against the `<productVersion>`.  
    The your product and data version don't have to be the same.  It is a good idea that they within one or two point releases of each other. 
6.  Close the file.  
      
     

## Step 2. Create the Test Data Archive

Now, you are ready to create some in-product test data for your tests.  If you have complex tests that need a lot of data, you may import a subset of data from a production instance of a host application.  For smaller plugins, this might not be necessary. Your set of test data may be very small.  Only you can decide what is appropriate for your plugin and your tests.  The technique in this tutorial is to manually create some test data.  Go to the command window or terminal on your system and do the following:

1.  Navigate to your `PLUGIN_HOME`.
2.  Start the application passing it the parameter to skip running any tests.

    ``` bash
    atlas-run -DskipTests=true
    ```

3.  Start your browser and log into JIRA.
4.  Create a project and add one or two issues to it.
5.  Return to the command line and stop the application.
6.  Make sure your current directory is your `PLUGIN_HOME`.
7.  Create a zip of the application home directory in your target.

    ``` bash
    atlas-create-home-zip
    ```

    This command creates a `PLUGIN_HOME/target/application/generated-test-resources.zip` file.  Since the target directory is often cleaned or removed, you want to copy this file to another location.

8.  Again, make sure your current directory is your `PLUGIN_HOME`.
9.  Copy the test resources to your `PLUGIN_HOME/src/test/resources` directory.

    ``` bash
    cp target/jira/generated-test-resources.zip PLUGIN_HOME/src/test/resources
    ```

    This directory is not cleared out when you run the `atlas-clean` command.

## Step 3. Configure Your Plugin with the Test Data

The ZIP archive you created in the previous step is now part of your plugin test data.  In this step, you configure your `pom.xml` file to load this data into the host application. Then, you'll run the application and confirm the data was loaded. 

1.  Return to the command line.
2.  Make sure your current directory is your `PLUGIN_HOME`.
3.  Go ahead and remove the target directory by entering the following command:

    ``` bash
    atlas-clean
    ```

    Cleaning the target directory from your project is not something you have to do often.  You do it at this point because you want to make sure that your project picks up the test data from your resources rather than anything left behind in the `target` directory.

4.  Edit your `pom.xml` file.
5.  Locate the `<build>` section of the file.
6.  Locate the `<configuration>` for the `com.atlassian.maven.plugins`.
7.  Add a `<productDataPath>`specification and point it to your test data ZIP archive.  
    When you are done your configuration will look similar to the following:

    ``` xml
    <configuration>
        <productVersion>${jira.version}</productVersion>
        <productDataVersion>${jira.version}</productDataVersion>                                                               
        <productDataPath>${basedir}/src/test/resources/generated-test-resources.zip</productDataPath>
    ...
    ```

8.  Save and close the file.
9.  Return to the command line and start the application in debug mode.

    ``` bash
    atlas-debug
    ```

    You could also use  `atlas-run -DskipTests=true` it is entirely your choice. 

10. After the build completes, log into the application.  
    You should find that your test data  also now is loaded into the application.

## Next Steps

You've completed the Writing and Running Plugin Test tutorial.  If you want to check your work, you can find the plugin source code on Atlassian Bitbucket. Bitbucket serves a public Git repository containing the tutorial's code. To clone the repository, issue the following command:

``` bash
git clone https://atlassian_tutorial@bitbucket.org/atlassian_tutorial/testtutorial.git
```

Alternatively, you can download the latest source here: <a href="https://bitbucket.org/atlassian_tutorial/testtutorial/downloads" class="uri external-link">https://bitbucket.org/atlassian_tutorial/testtutorial/downloads</a>.

The information in this tutorial was foundation information.  Meaning, you can use what you learned here regardless of which host application your plugin is for.  Documentation for each host application (available from this site) contains additional and more specific information about testing in those applications.











































































































































































































