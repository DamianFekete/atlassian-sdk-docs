---
title: Modify the Plugin 41236025
aliases:
    - /server/framework/atlassian-sdk/modify-the-plugin-41236025.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=41236025
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=41236025
confluence_id: 41236025
platform:
product:
category:
subcategory:
---
# Modify the plugin

In the [previous step](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/create-a-helloworld-plugin-project), you created a skeleton for a JIRA plugin. In this part of the tutorial, you'll modify your plugin to add a new link in the JIRA menu.  To do this you'll need to create a [Web Section Plugin Module](/server/framework/atlassian-sdk/web-section-plugin-module-852133.html) and a [Web Item Plugin Module](/server/framework/atlassian-sdk/web-item-plugin-module-852014.html) using the Atlassian SDK.

 

## Step 1. Update the organization details that appear on the Plugin

1.  You should still be in the myPlugin directory after shutting down JIRA. 
2.  Open the` pom.xml` file in your favourite editor. 
3.  Locate the **&lt;organization&gt;** element in the file. It should look something like this:

    ``` xml
        <organization>
            <name>Example Company</name>
            <url>http://www.example.com/</url>
        </organization>
    ```

4.  Update the element to include some personalized information, for example:

    ``` xml
        <organization>
            <name>Atlassian SDK Tutorial</name>
            <url>http://developer.atlassian.com/</url>
        </organization>
    ```

5.  Save and close the file.
6.  Return to the **command prompt **window, and enter atlas-run and wait for JIRA to start back up.
7.  Login if prompted
8.  Open the **Manage add-ons** page in your browser using the path: <a href="http://localhost:2990/jira/plugins/servlet/upm" class="uri external-link">http://localhost:2990/jira/plugins/servlet/upm</a>
9.  Expand the **myPlugin** plugin to see your changes.
10. When you're finished, shutdown JIRA gracefully using **Ctrl+D**. 

## Step 2. Add a custom menu to JIRA  

1.  Open the `/src/main/resources/atlassian-plugin.xml` file from your** **`myPlugin `directory in your favourite text editor.  
2.  The **atlassian-plugin.xml** file will look something like this: 

    ``` xml
    <atlassian-plugin key="${atlassian.plugin.key}" name="${project.name}" plugins-version="2">
        <plugin-info>
            <description>${project.description}</description>
            <version>${project.version}</version>
            <vendor name="${project.organization.name}" url="${project.organization.url}" />
            <param name="plugin-icon">images/pluginIcon.png</param>
            <param name="plugin-logo">images/pluginLogo.png</param>
        </plugin-info>
        <!-- add our i18n resource -->
        <resource type="i18n" name="i18n" location="myPlugin"/>
        <!-- add our web resources -->
        <web-resource key="myPlugin-resources" name="myPlugin Web Resources">
            <dependency>com.atlassian.auiplugin:ajs</dependency>
            <resource type="download" name="myPlugin.css" location="/css/myPlugin.css"/>
            <resource type="download" name="myPlugin.js" location="/js/myPlugin.js"/>
            <resource type="download" name="images/" location="/images"/>
            <context>myPlugin</context>
        </web-resource>
    </atlassian-plugin>
    ```

3.  Next, in **command prompt **make sure you're in the `myPlugin` folder and then run the following command:

    ``` bash
    atlas-create-jira-plugin-module
    ```

    You'll be prompted to choose a plugin module from a list of possible module types (check out [Plugin Modules](/server/framework/atlassian-sdk/plugin-modules-852136.html) for more information).

4.  Type **30** to select the `Web Section `plugin module type.

5.  Now, you'll be prompted to answer a few configuration questions, answer as follows:

    ``` text
    Enter Plugin Module Name My Web Section: : mySection
    Enter Location (e.g. system.admin/mynewsection): my-item-link
    Show Advanced Setup? (Y/y/N/n) N: : N
    ```

    At the moment the location `my-item-link` doesn't exist, but we'll create that in the next step.

6.  Next, you're prompted to enter another plugin module. Type **Y** to create another module. 

7.  Type **25** to select the `Web Item` plugin module and then answer the configuration questions as follows:

    ``` bash
    Enter Plugin Module Name My Web Item: : myItem
    Enter Section (e.g. system.admin/globalsettings): system.top.navigation.bar
    Enter Link URL (e.g. /secure/CreateIssue!default.jspa): deleteMe
    Show Advanced Setup? (Y/y/N/n) N: : N
    ```

8.  When you are prompted to enter another Plugin Module, type **N**.   
    The system will complete the creation of the modules and you'll receive a confirmation that the build was successful. 

## Step 3. Customise the menu

1.  Open the **atlassian-plugin.xml** file and you'll notice it has changed a little:

    ``` xml
    <?xml version="1.0" encoding="UTF-8"?>


    <atlassian-plugin key="${atlassian.plugin.key}" name="${project.name}" plugins-version="2">
      <plugin-info>
        <description>${project.description}</description>
        <version>${project.version}</version>
        <vendor name="${project.organization.name}" url="${project.organization.url}"/>
        <param name="plugin-icon">images/pluginIcon.png</param>
        <param name="plugin-logo">images/pluginLogo.png</param>
      </plugin-info>
      <!-- add our i18n resource -->
      <resource type="i18n" name="i18n" location="myPlugin"/>
      <!-- add our web resources -->
      <web-resource key="myPlugin-resources" name="myPlugin Web Resources">
        <dependency>com.atlassian.auiplugin:ajs</dependency>
        <resource type="download" name="myPlugin.css" location="/css/myPlugin.css"/>
        <resource type="download" name="myPlugin.js" location="/js/myPlugin.js"/>
        <resource type="download" name="images/" location="/images"/>
        <context>myPlugin</context>
      </web-resource>
      <web-section name="mySection" i18n-name-key="my-section.name" key="my-section" location="my-item-link" 
    weight="1000">
        <description key="my-section.description">The mySection Plugin</description>
        <label key="my-section.label"/>
      </web-section>
      <web-item name="myItem" i18n-name-key="my-item.name" key="my-item" section="system.top.navigation.bar" 
    weight="1000">
        <description key="my-item.description">The myItem Plugin</description>
        <label key="my-item.label"></label>
        <link linkId="my-item-link">deleteMe</link>
      </web-item>
    </atlassian-plugin>
    ```

2.  In the **web-section**, delete the following: 
    -   The `<label key="my-section.label"/>` line.
    -   The phrase `deleteMe` in the `<link linkId="my-item-link">`. 

    In this tutorial we don't want the 'myItem' menu to link anywhere, and we don't want to see the 'mySection' label in our menu.  
3.  Save your changes to the file.
4.  Return to the **Command Prompt **window, run the `atlas-run `command, and wait for JIRA to start up.  
5.  Once you've logged in, you will see the new JIRA menu.
6.  Shut down JIRA using **Ctrl+D**.

## Next Step

Starting and stopping JIRA can take several minutes each time.  QuickReload significantly reduces your plugin development iteration time, so in the next part of the tutorial, you'll learn how to use it to test a change to your plugin without restarting JIRA.

**[Modify the plugin using QuickReload](/server/framework/atlassian-sdk/modify-the-plugin-using-quickreload-41236017.html)**

## Additional Resources

The source code for this tutorial is available on Bitbucket at <a href="https://bitbucket.org/serverecosystem/myplugin" class="uri external-link">https://bitbucket.org/serverecosystem/myplugin</a>

Alternatively, check out the [Getting Started Tutorial FAQ](/server/framework/atlassian-sdk/getting-started-tutorial-faq-43648385.html)

 

Still need help? Request support at <a href="https://ecosystem.atlassian.net/servicedesk/customer/portal/14" class="external-link">Developer Technical Support Portal</a>

























