---
aliases:
- /server/framework/atlassian-sdk/modify-the-plugin-using-quickreload-41236017.html
- /server/framework/atlassian-sdk/modify-the-plugin-using-quickreload-41236017.md
category: devguide
confluence_id: 41236017
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=41236017
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=41236017
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/modify-the-plugin-using-quickreload
new_url: /server/framework/atlassian-sdk/modify-the-plugin-using-quickreload
platform: server
product: atlassian-sdk
subcategory: learning
title: Modify the plugin using QuickReload
---
# Modify the plugin using QuickReload

So far you've discovered that you can [create a plugin](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/create-a-helloworld-plugin-project) for JIRA and you can [make changes to that plugin](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/modify-the-plugin), however starting and stopping JIRA can take several minutes each time.  QuickReload significantly reduces your plugin development iteration time by watching output directories for P2 JAR files and then uploads them into the running host application.  

 

## Step 1. Check QuickReload is enabled in your pom

1.  Open the `pom.xml` in your favourite text editor.
2.  Search for the `<build>` tags, you should see something similar to this:

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

                    <enableQuickReload>true</enableQuickReload>
                    <enableFastdev>false</enableFastdev>
                    ...
    ```

    Confirm that `<enableQuickReload>` is set to **true** and `<enableFastdev>` is set to **false**.  If not, update the pom to match the example above and then save your changes. 

3.  Open a **Command Prompt** window, and navigate to your` myPlugin` directory.  
4.  Enter the `atlas-run` command and wait for JIRA to start up.
5.  Login to JIRA and confirm that you can see the** myItem** menu which does not have a drop down menu when clicked.

## Step 2. Make a change to your plugin while JIRA is running

1.  Open a second **Command Prompt** window and navigate to your` myPlugin` directory.
2.  Enter the` atlas-create-jira-plugin-module` command and answer the prompts as follows:

    ``` text
    Choose a number (1/2/3/4/5/6/7/8/9/10/11/12/13/14/15/16/17/18/19/20/21/22/23/24/25/26/27/28/29/30/31/32
    /33/34):25
    Enter Plugin Module Name My Web Item: : Atlassian Developers Site
    Enter Section (e.g. system.admin/globalsettings): my-item-link/my-section
    Enter Link URL (e.g. /secure/CreateIssue!default.jspa): http://developer.atlassian.com/docs
    Show Advanced Setup? (Y/y/N/n) N: : N
    ```

3.  Enter **N **when prompted to create another module.
4.  Run the command:

    ``` text
    atlas-mvn package
    ```

    and wait for your plugin package to build, when it's finished you'll see:

    ``` text
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 9.084 s
    [INFO] Finished at: 2016-08-22T17:09:56+10:00
    [INFO] Final Memory: 32M/321M
    [INFO] ------------------------------------------------------------------------
    ```

5.  Return to the first command prompt window (the one you started JIRA in earlier using the `atlas-run` command), you'll notice there are some log entries appearing. When the plugin has finished loading you'll see:

    ``` text
    [INFO] [talledLocalContainer]     Quick Reload Finished (1727 ms) - 'myPlugin-1.0.0-SNAPSHOT.jar'
    ```

6.  Reload <a href="http://localhost:2990/jira" class="uri external-link">http://localhost:2990/jira</a> in your browser window, and you'll see that your menu is now showing the changes you just made:  
    <img src="/server/framework/atlassian-sdk/images/myplugin---atlassian-developer-site-menu-item.png" title="Atlassian Developers Site menu item in JIRA 7.2.2" alt="Atlassian Developers Site menu item in JIRA 7.2.2" width="680" height="178" />

## Need Help?

 The source code for this tutorial is available on Bitbucket at <a href="https://bitbucket.org/serverecosystem/myplugin" class="uri external-link">https://bitbucket.org/serverecosystem/myplugin</a>

Alternatively, check out the [Getting Started Tutorial FAQ](/server/framework/atlassian-sdk/getting-started-tutorial-faq)

Still need help? Request support at <a href="https://ecosystem.atlassian.net/servicedesk/customer/portal/14" class="external-link">Developer Technical Support Portal</a>

## Next step

If you'd like to keep learning about add-on development you may want to try out the Confluence tutorial below:

[Create a Confluence 'Hello World' Macro](/server/framework/atlassian-sdk/create-a-confluence-hello-world-macro)

Here are some other things you might like to do next:

-   Check out the [Learn the Development Platform by Example](/server/framework/atlassian-sdk/learn-the-development-platform-by-example) Tutorial to learn about developing plugins for any Atlassian application.  
-   Tackle another one of our Atlassian Developer [Tutorials](/server/framework/atlassian-sdk/tutorials).

## Additional resources

The following resources will allow you to learn more about some of the tasks we covered in this tutorial:

-   [Working with the POM](/server/framework/atlassian-sdk/working-with-the-pom)
-   [Plugin Modules](/server/framework/atlassian-sdk/plugin-modules)
-   [Writing and Running Plugin Tests](/server/framework/atlassian-sdk/writing-and-running-plugin-tests)











































































































