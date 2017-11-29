---
aliases:
- /server/framework/atlassian-sdk/create-a-plugin-skeleton-16352143.html
- /server/framework/atlassian-sdk/create-a-plugin-skeleton-16352143.md
category: devguide
confluence_id: 16352143
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16352143
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16352143
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/getting-started/learn-the-development-platform-by-example/create-a-plugin-skeleton
new_url: /server/framework/atlassian-sdk/create-a-plugin-skeleton
platform: server
product: atlassian-sdk
subcategory: learning
title: Create a plugin skeleton
---
# Create a plugin skeleton

This section covers creating a plugin skeleton and launching it in the Atlassian Reference Application (RefApp). RefApp is a lightweight web application built for the sole purpose of developing plugins that work in any Atlassian application. If your plugin works in RefApp, you can run it in any other Atlassian application. 

 

## Get introduced to RefApp

We use RefApp intentionally in this tutorial. RefApp is a tool uniquely suited to plugin development: No Atlassian application is identical, but the RefApp provides the shared framework between all Atlassian applications. This means that you can develop your plugin without accidentally relying on dependencies or features specific to one application, or encountering an application-specific bug later on. Developing a plugin with RefApp eliminates guesswork about the functionality of your project. You can rest assured that since all Atlassian applications share at least the framework present in RefApp, your plugin will work as expected.  

RefApp features common components like SAL (Secure access layer) or the REST API browser (we won't be using REST in this tutorial). 

While the RefApp might not be much to look at, it's the perfect place to start your plugin development.

## Step 1. Create a skeleton

Here, you'll create the foundation for your plugin project in the form of a plugin skeleton. Maven builds the plugin skeleton as Java and XML files, and downloads dependencies necessary for your plugin project. 

1.  Create a directory called `atlastutorial`. 

    ``` bash
    $ mkdir atlastutorial
    ```

2.  Change to your new `atlastutorial` directory. 

    ``` bash
    $ cd atlastutorial
    ```

3.  Generate a skeleton for your add-on. 

    ``` bash
    $ atlas-create-refapp-plugin
    ```

4.  Create the following when prompted.

    Press `return` or `enter` to accept default values shown in brackets. 

    |              |                                         |
    |--------------|-----------------------------------------|
    | `groupId`    | `com.atlassian.plugins.tutorial.refapp` |
    | `artifactId` | `adminUI`                               |
    | `version`    | `1.0-SNAPSHOT`                          |
    | `package`    | `com.atlassian.plugins.tutorial.refapp` |

5.  Confirm your entries when prompted with `Y` or `y`.

    The code generation runs to completion. You'll see a message similar to the following: 

    ``` bash
    [INFO]
    -------------------------------------------------------------------- 
    [INFO] BUILD SUCCESSFUL 
    [INFO] 
    -------------------------------------------------------------------- 
    [INFO] Total time: 36 seconds [INFO] Finished at: Mon Jun 17 11:22:49 PDT 2013 
    [INFO]
     --------------------------------------------------------------------
    ```

6.  Change to the newly created `adminUI` project root.

    ``` bash
    $ cd adminUI/
    ```

      

7.  Remove the test directories.

    ``` bash
    $ rm -rf src/test/java/
    $ rm -rf src/test/resources/
    ```

    These directories are automatically created from `atlas-create-refapp-plugin`, but testing isn't part of this tutorial. Removing them simplifies your work in future steps.

8.  Remove Java classes from the `src/main/java` directory: 

    ``` bash
    $ rm ./src/main/java/com/atlassian/plugins/tutorial/refapp/*.java
    ```

    You'll create a single Java class encapsulating your plugin logic in later steps.

## Step 2. Start up the RefApp

When you generated the skeleton for your plugin, you specified a RefApp plugin skeleton. Your plugin has access to the shared application services and developer tools for all Atlassian applications. Here you'll start up the RefApp and get better acquainted with your resources.

1.  Change directory to your project root. 

    ``` bash
    $ cd adminUI
    ```

2.  Enter the following command to start up RefApp:

    ``` bash
    $ atlas-run
    ```

3.  Locate the RefApp URL.  
    After a few moments your terminal will display a message with the URL of the application. RefApp usually launches on port 5990. 

    ``` bash
    [INFO] [talledLocalContainer] Tomcat 6.x started on port [5990] 
    [INFO] refapp started successfully in 46s at http://localhost:5990/refapp 
    [INFO] Type Ctrl-D to shutdown gracefully [INFO] Type Ctrl-C to exit
    ```

4.  Copy the URL and paste it into your browser.   
      
5.  The URL will resemble **<a href="http://localhost:5990/refapp/plugins/servlet" class="external-link">http://localhost:5990/refapp</a>.**  
    **  
    **
6.  Click **Login** from the upper right-hand corner.  
     
7.  Log in with the username `admin` and the password `admin`.  
     
8.  Click **Login**.
9.  Click **A.D. Ministrator (Sysadmin)**.  
       
    Under the **General**, **Application Links**, and **Developer Toolbox** you'll see the core components shared by all Atlassian applications.

  

Optional: Import your project into Eclipse IDE

You've launched RefApp from your `adminUI` project root using just the command line. Now, let's import `adminUI` into Eclipse so you can make code changes more easily.

Start from a new tab in your terminal:

1.  Change directory to your project root. 

    ``` bash
    $ cd adminUI
    ```

2.  Make your project available to Eclipse. 

    ``` bash
    $ atlas-mvn eclipse:eclipse
    ```

3.  Start Eclipse.  
    You can open a new tab in your terminal and run the following commands to open Eclipse. 

    ``` bash
    $ cd ~/eclipse 
    $ ./eclipse
    ```

4.  Click **File &gt; Import**.  
      
5.  Under General, choose **Existing Projects into Workspace**.  
     ![](/server/framework/atlassian-sdk/images/1.6.jpeg)
6.  Click **Next**.  
      
7.  Choose **Select root directory**.  
      
8.  Click **Browse**.  
    ![](/server/framework/atlassian-sdk/images/1.7.jpeg)
9.  Choose your project's parent directory, `atlastutorial`.   
    ![](/server/framework/atlassian-sdk/images/1.8.jpeg)
10. Click **Open**.  
      
11. Confirm your `adminUI` project appears in the Projects window.  
    If you don't see your project, ensure you run `atlas-mvn eclipse:eclipse` while in your `adminUI` directory.  
      
12. Click **Finish**.

## Next Steps

Now that your plugin skeleton is built and imported into Eclipse, [you'll construct a servlet](https://developer.atlassian.com/display/DOCS/Convert+component+to+servlet+module).






























































































































































