---
aliases:
- /server/framework/atlassian-sdk/frequently-used-commands-13632968.html
- /server/framework/atlassian-sdk/frequently-used-commands-13632968.md
category: devguide
confluence_id: 13632968
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=13632968
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=13632968
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/frequently-used-commands
new_url: /server/framework/atlassian-sdk/frequently-used-commands
platform: server
product: atlassian-sdk
subcategory: learning
title: Frequently used commands
---
# Frequently used commands

In this section, we will look at some typical tasks and give examples of the SDK scripts you can use. The following topics are covered:

 

## Creating a New Plugin from Scratch

Say you want to create a new Confluence plugin skeleton. Simply open a command window, go to the directory where you want to create the plugin and type:

``` bash
 atlas-create-confluence-plugin
```

Similarly, you would enter one of the following to create a plugin for JIRA, Bamboo or the RefApp:

``` bash
atlas-create-jira-plugin
atlas-create-bamboo-plugin
atlas-create-refapp-plugin
```

## Running a Plugin in an Application

Say you want to install and run your plugin in your host Atlassian application. Go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-run
```

Note that the above shell script will work for any host application, including Confluence, JIRA, etc. The script will determine the application, based on your plugin's specifications.

## Specifying a Version of the Application

Say you want to run your plugin with Confluence 2.10.3. Go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-clean
atlas-run --version 2.10.3
```

Say you want to run your plugin with JIRA 4.0 snapshot. Go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-clean
atlas-run --version 4.0-SNAPSHOT
```

*Note:* Running `atlas-clean` will clear the previous version of the host application from your build output directory. You only need to do this if the previous application version was different from the one you need now.

Specifying an Application Server (Container)

Say you want to run your plugin with Confluence 2.10.3 and JBoss 4.2.x. Go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-run --version 2.10.3 --container jboss42x
```

## Specifying a Version of SAL

Say you want to run that plugin but with Confluence 2.10.3 and SAL 2.0.5:

``` bash
atlas-run --version 2.10.3 --sal-version 2.0.5
```

## Running Integration Tests against a Different Application

Say you have a RefApp plugin but want to run your integration tests against Confluence:

``` bash
atlas-integration-test --product confluence
```

## Running your Plugin in Multiple Applications

Say you want to run that RefApp plugin in multiple applications simultaneously. In three separate tabs in your terminal (command window):

-   Type the following to run the plugin in the RefApp:

    ``` bash
    atlas-run
    ```

-   Type the following to run the plugin in Confluence:

    ``` bash
    atlas-run --product confluence --version 3.0-m9
    ```

-   Type the following to run the plugin in JIRA:

    ``` bash
    atlas-run --product jira --version 4.0-SNAPSHOT
    ```

## Using the Maven Command Line Interface

The SDK bundles the <a href="http://wiki.github.com/mrdon/maven-cli-plugin" class="external-link">Maven CLI plugin</a> and pre-configures it properly with the `pi` and `pu` commands. To use it with your plugin's host application, go to the plugin's project directory (where you created the plugin) and type:

``` bash
atlas-cli
```

## Generating Test Data for Re-Use

Use the `atlas-create-home-zip` command to create a zip file of your application's home directory, and then load the contents of the home directory into the application every time you start it up.

For example, let's assume you want to prepopulate JIRA with a few projects and issues for testing on every clean startup. First, run JIRA using `atlas-run` and add your projects and issues. Stop JIRA, go to the project directory (where you created the plugin) and type:

``` bash
atlas-create-home-zip
```

Copy the `generated-test-resources.zip` file to the test `/src/test/resources/` directory. Then add the following element to the configuration of the maven-jira-plugin in your POM:

``` xml
<productDataPath>${basedir}/src/test/resources/generated-test-resources.zip</productDataPath>
```

See [atlas-create-home-zip](/server/framework/atlassian-sdk/atlas-create-home-zip).





















































































































































