---
aliases:
- /server/framework/atlassian-sdk/create-a-helloworld-plugin-project-10422115.html
- /server/framework/atlassian-sdk/create-a-helloworld-plugin-project-10422115.md
category: devguide
confluence_id: 10422115
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=10422115
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=10422115
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/create-a-helloworld-plugin-project
new_url: /server/framework/atlassian-sdk/create-a-helloworld-plugin-project
platform: server
product: atlassian-sdk
subcategory: learning
title: Create a HelloWorld plugin project
---
# Create a HelloWorld plugin project

You now have a local development environment configured for the Atlassian SDK and you're ready to build your first Atlassian Server plugin! 

**Important**: This guide explains how to build a plugin for Atlassian Server. If you meant to developing an app for Atlassian Cloud then [view the JIRA Cloud Getting Started guide](https://developer.atlassian.com/cloud/jira/platform/getting-started/).

The plugin is going to be fairly simple, but you'll learn the fundamental steps for creating a plugin and starting up your application environment.  

If you get stuck at any point, you can compare your progress to our <a href="https://bitbucket.org/serverecosystem/myplugin" class="external-link">myPlugin source code</a>.  The tutorial is tested to work with the Atlassian Plugin SDK 6.2.9.

 

## Step 1. Use the Atlassian SDK to build a plugin skeleton

1.  Navigate to the directory on your system where you'd like to create your plugin.  The command we are about to run will create a folder with the plugin directories inside. 

2.  Create an add-on project using the `atlas-create-jira-plugin` command from a **Command Prompt **window:

    ``` text
    atlas-create-jira-plugin
    ```

    This command is going to build a JIRA plugin skeleton using maven. Some logs appear on the screen showing maven commands that are being run and the version of JIRA that is being used. 

3.  You will be prompted to provide some information about your plugin. For the purposes of this tutorial respond to the prompts as follows:

    ``` text
    Define value for groupId: : com.atlassian.tutorial
    Define value for artifactId: : myPlugin
    Define value for version: 1.0.0-SNAPSHOT: : 1.0.0-SNAPSHOT
    Define value for package: com.atlassian.tutorial: : com.atlassian.tutorial.myPlugin
    ```

4.  You will then be prompted to confirm your configuration. Verify the details to ensure they are correct, and then type **Y** once you are ready to proceed:

    ``` text
    Confirm properties configuration:
    groupId: com.atlassian.tutorial
    artifactId: myPlugin
    version: 1.0.0-SNAPSHOT
    package: com.atlassian.tutorial.myPlugin
    Y: : Y
    ```

    The basic skeleton for your Atlassian JIRA plugin is created in a new `myPlugin` directory: 

    ``` p1
    .
    ├── LICENSE
    ├── README
    ├── pom.xml
    └── src
        ├── main
        │   ├── java
        │   │   └── com
        │   │       └── atlassian
        │   │           └── tutorial
        │   │               └── myPlugin
        │   │                   ├── api
        │   │                   │   └── MyPluginComponent.java
        │   │                   └── impl
        │   │                       └── MyPluginComponentImpl.java
        │   └── resources
        │       ├── META-INF
        │       │   └── spring
        │       │       └── plugin-context.xml
        │       ├── atlassian-plugin.xml
        │       ├── css
        │       │   └── myPlugin.css
        │       ├── images
        │       │   ├── pluginIcon.png
        │       │   └── pluginLogo.png
        │       ├── myPlugin.properties
        │       └── js
        │           └── myPlugin.js
        └── test
            ├── java
            │   ├── it
            │   │   └── com
            │   │       └── atlassian
            │   │           └── tutorial
            │   │               └── myPlugin
            │   │                   └── MyComponentWiredTest.java
            │   └── ut
            │       └── com
            │           └── atlassian
            │               └── tutorial
            │                   └── myPlugin
            │                       └── MyComponentUnitTest.java
            └── resources
                └── atlassian-plugin.xml
                  
    ```

    Feel free to take a moment to explore the different files created by the Atlassian SDK before you continue. 

## Step 2. Start up JIRA with your plugin installed

In this step, we'll use the `atlas-run` command to run the application (JIRA in this example) and install the plugin. Then we'll confirm that JIRA has started with the plugin created in *Step 1* already installed.   

1.  Change to the `myPlugin` directory and enter the following command: 

    ``` text
     atlas-run
    ```

    This is going to use the information in the plugin skeleton you created earlier to download JIRA and all of the other plugins it needs, then start JIRA with your plugin installed.  

    The first time you do this, it might take several minutes to complete.  

    Once JIRA has started, you'll see something like this in the Command Prompt window:

    ``` text
    [INFO] [talledLocalContainer] Aug 08, 2016 5:51:33 PM org.apache.catalina.startup.Catalina start
    [INFO] [talledLocalContainer] INFO: Server startup in 234207 ms
    [INFO] [talledLocalContainer] Tomcat 8.x started on port [2990]
    [INFO] jira started successfully in 332s at http://DESKTOP-EF2CA9N:2990/jira
    [INFO] Type Ctrl-D to shutdown gracefully
    [INFO] Type Ctrl-C to exit
    ```

2.  Open a browser window and navigate to **<a href="http://localhost:2990/jira" class="uri external-link">http://localhost:2990/jira</a>**.  To login, use the credentials:

    |          |       |
    |----------|-------|
    | Username | admin |
    | Password | admin |

3.  A Welcome dialog will appear and you'll be asked to configure some basic JIRA settings. 

    You'll only need to do this once for your plugin and the settings will be remembered the next time you use the `atlas-run` command.

4.  Type **gg**, and then type **manage**.**  **From the list that appears, select **Manage add-ons**.   
    (Alternatively you can click on the cog icon at the top of the screen to open the administration dialog, and then select **Add-ons** and finally when the Atlassian Marketplace Administration page opens, select **Manage add-ons** on the right hand side). 
5.  Locate the **myPlugin** listings in **User-installed add-ons** and click on them to expand.   
    One of the listings you see will be the plugin itself, the other will be the plugin tests. Notice that the plugins have a few basic modules that were created by the SDK.  
6.  Close your browser, and return to the **Command Prompt** window where JIRA was running. 
7.  Shutdown JIRA gracefully with **CTRL+D** (on OSX and Linux) or **CTRL+Z** (on Windows).

## Next step

You have a basic plugin skeleton, so lets learn how to modify and customise it to provide a new menu in JIRA. 

**[Modify the Plugin](/server/framework/atlassian-sdk/modify-the-plugin)**

## Additional Resources

The source code for this tutorial is available on Bitbucket at <a href="https://bitbucket.org/serverecosystem/myplugin" class="uri external-link">https://bitbucket.org/serverecosystem/myplugin</a>

Alternatively, check out the [Getting Started Tutorial FAQ](/server/framework/atlassian-sdk/getting-started-tutorial-faq)

 

Still need help? Request support at <a href="https://ecosystem.atlassian.net/servicedesk/customer/portal/14" class="external-link">Developer Technical Support Portal</a>





































































































































































































































































































































































































































































