---
aliases:
- /server/framework/atlassian-sdk/run-your-plugin-in-the-container-16352147.html
- /server/framework/atlassian-sdk/run-your-plugin-in-the-container-16352147.md
category: devguide
confluence_id: 16352147
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16352147
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16352147
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/getting-started/learn-the-development-platform-by-example/run-your-plugin-in-the-container
new_url: /server/framework/atlassian-sdk/run-your-plugin-in-the-container
platform: server
product: atlassian-sdk
subcategory: learning
title: Run your plugin in the container
---
# Run your plugin in the container

In this section, you learn about the relationship between an Atlassian application(s) and your plugin. You'll also learn about the environment your plugin runs in. You should have already created a plugin skeleton, imported your project into Eclipse, and made some class and `atlassian-plugin.xml` modifications. This section contains the following topics: 

 

 

## Your plugin, the container, and Atlassian applications

Atlassian uses Tomcat as a container. Tomcat runs and maintains an Atlassian application and its plugins. Atlassian modified Tomcat with enhancements to ensure your plugin and our applications run smoothly together. The following diagram depicts an application and a plugin running inside of Tomcat.

<img src="/server/framework/atlassian-sdk/images/3.1.png" width="500" />

Apache Felix is an OSGi implementation which, together with the Spring Dynamic Module Facility, helps your plugin share resources with the Atlassian application.  For example, these facilities eliminate redundant dependencies by allowing your plugin to use those already provided by the Atlassian application. 

Operating within each Atlassian application is the Universal Plugin Manager (UPM). The UPM manages plugins installed in the Atlassian application. In this section of the tutorial, you'll run your plugin skeleton from JIRA. You'll build on the plugin skeleton to begin creating a fully-functional plugin.

## Step 1. Modify your `pom.xml` file

A Maven `pom.xml` file is essential to your project. Maven uses the `pom.xml` file to determine how to build your project from the `target` staging area. Here, you'll customize the `<organization>` section to make the add-on yours, and later you'll view these changes reflected in the UPM.

1.  Open the `pom.xml`.  
      
2.  Locate the `<organization>` tags.  
      
3.  Replace the content in the `<name>` tags with a company name of your choice.  
      
4.  Replace the content in the `<url>` tags with a different URL.

    Here's an example: 

    ``` javascript
        <organization>
            <name>Awesomeness Inc</name>
            <url>http://www.awesomebreedsmoarawesome.com/</url>
        </organization>
    ```

5.  Save and close the file.  
      
6.  If you made your changes in Eclipse, update your project with the changes.

        $ atlas-mvn eclipse:eclipse

7.  Click **File &gt; Refresh** in Eclipse.

## Step 2. Build your plugin in JIRA

When you generated the plugin skeleton, you specified a RefApp plugin with your command `atlas-create-refapp-plugin`. As mentioned, if your plugin works in RefApp, it'll work in any Atlassian application. Now you'll try out you plugin in a more feature-rich environment: JIRA. Here you'll verify that your `pom.xml` changes are reflected in the UPM and that you can still access the servlet.

1.  Shut down Refapp if it's still running by typing `CTRL+D` in your terminal.  
      
2.  Clear the target from your project root.

        $ atlas-clean

3.  Start JIRA 6.1.

        $ atlas-run --product jira --version 6.1

4.  Locate the URL to access JIRA locally.  
    Your terminal outputs `[INFO]` messages to display the URL.   
    JIRA usually runs on port 2990, with a URL like **<a href="http://localhost:2990/jira" class="uri external-link">http://localhost:2990/jira</a> **

        [INFO] [talledLocalContainer] INFO: Server startup in 100371 ms
        [INFO] [talledLocalContainer] Tomcat 7.x started on port [2990]
        [INFO] jira started successfully in 144s at http://localhost:2990/jira
        [INFO] Type Ctrl-D to shutdown gracefully
        [INFO] Type Ctrl-C to exit

5.  Copy the URL and access it from your browser.  
    We recommend Google Chrome or Mozilla Firefox for this tutorial.  
      
6.  Login with username and password **`admin/admin`.**  
    If the login screen isn't visible, click **Login** from the upper right-hand corner.  
      
7.  Navigate to **<a href="http://localhost:2990/jira/plugins/servlet/test" class="uri external-link">http://localhost:2990/jira/plugins/servlet/test</a> **access the servlet.  
    The page should be identical to the one you viewed while in RefApp.  
    ![](/server/framework/atlassian-sdk/images/3.2.jpeg)
8.  Click **Back** in your browser to return to the dashboard.  
    Now you'll begin to navigate to the UPM.
9.  Click the **cog icon &gt; Administration.**  
    **![](/server/framework/atlassian-sdk/images/add-onsjira.png)**
10. Under Atlassian Marketplace, click **Manage add-ons**.   
      
11. Locate your** **adminUI plugin.  
    You'll see the UPM displayed in JIRA. Your plugin may be under **User-Installed Plugins**.   
      
12. Confirm the changes you made to the `<company>` section in the `pom.xml` are displayed.  
    <img src="/server/framework/atlassian-sdk/images/adminuiinupm.png" title="adminUI plugin in UPM" alt="adminUI plugin in UPM" width="700" />

## Step 3. Open the developer toolbar

Atlassian includes several developer tools in its applications so you can develop and test add-ons. This section introduces you to these tools.

1.  In your running instance of JIRA expand the arrow on the bottom of the page.  
    This arrow should be visible on any page as long as you're logged in.  
      
    <img src="/server/framework/atlassian-sdk/images/3.6.jpeg" width="700" />
2.  Confirm the toolbar expands in the lower portion of your screen.  
    <img src="/server/framework/atlassian-sdk/images/3.11.jpeg" width="700" />  
    ![(info)](/server/framework/atlassian-sdk/images/icons/emoticons/information.png) If you don't see the toolbar, try using Google Chrome or Mozilla Firefox to access your local JIRA instance.  
    Now you can learn what resources you have available, and why you might use them in your add-on development.   
      
3.  Type **SAL** (short for Shared Access Layer) into the search field.  
    The search field is located on the right side of the developer tool bar. Instant results appear the search box.  
    The SAL is an API for aiding cross-application plugin development. When developing for multiple Atlassian applications, SAL handles services like job scheduling or internationalization lookups.  
      
4.  Explore documentation and APIs for the SAL.   
    You'll return to interact with SAL in future steps.   
      
5.  Click **admin &gt; Developer Toolbox**.  
    This offers a more comprehensive menu than the shortcut toolbar. This page gives quick access to the REST API browser or OSGi resources.  
      
6.  Click **FastDev . **  
    Choose this option from the <img src="https://extranet.atlassian.com/download/attachments/2132607152/image2013-6-21%2010%3A41%3A46.png?version=1&amp;modificationDate=1371836506655&amp;api=v2" class="confluence-external-resource" /> button in the lower toolbar, or **Scan and Reload** from the Developer Toolbox button. A keyboard shortcut is **SHIFT+F5.**  
    **  
    **
7.  Confirm no changes are found.  
    In future steps, you'll use this to reload your plugin after you change source code files.  
      
8.  Click **Highlight i18n**.   
    i18n, short for "Internationalization and localization" lets you localize your plugin. This means you can import translated label strings without having to recompile your plugin.
9.  View the i18n strings in JIRA.  
10. Click **Unhighlight i18n**.

  

Next steps

You've built the foundation and learned core concepts to develop your plugin in the Atlassian system, and become acquainted with the Developer Toolbox. Now you'll [add component modules](https://developer.atlassian.com/display/DOCS/Control+access+with+SAL).




































































































































