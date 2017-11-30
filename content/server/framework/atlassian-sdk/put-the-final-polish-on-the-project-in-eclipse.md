---
aliases:
- /server/framework/atlassian-sdk/put-the-final-polish-on-the-project-in-eclipse-10422292.html
- /server/framework/atlassian-sdk/put-the-final-polish-on-the-project-in-eclipse-10422292.md
category: devguide
confluence_id: 10422292
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=10422292
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=10422292
legacy_url: https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/put-the-final-polish-on-the-project-in-eclipse
new_url: /server/framework/atlassian-sdk/put-the-final-polish-on-the-project-in-eclipse
platform: server
product: atlassian-sdk
subcategory: other
title: Put the final polish on the project in Eclipse
---
# Put the final polish on the project in Eclipse

At this point, you have created an Atlassian Plugin project and edited that project. You have also configured Eclipse to work with Atlassian projects. Let's go ahead and bring the helloworld project you created into Eclipse and work on it there. The following topics are covered:

## Step 1: Learn a little about modules

After you bring your helloworld plugin into your project, you will add some modules to it to build up a custom menu. Each Atlassian product exposes a number of plugin modules. There are a set of modules that are common to all plugins and some modules are defined by and specific to the individual applications. For example, all products support a servlet plugin module, but only Confluence provides a macro plugin module. Later, as you become more knowledgeable, you can create your own modules.

You need to use just two module types to create your custom menu.

You use a `web-item` module to define the menu itself and another one for a menu item. You use a `web-section` to hold the menu. You define all of these using `atlas-` commands.

#### `helloworld` Source

If you want to check your work when you are done, you can find the `helloworld` source code on Atlassian bitbucket. bitbucket serves a public Git repository containing the tutorial's code. To clone the repository, issue the following command:

``` bash
git clone https://bitbucket.org/atlassian_tutorial/helloworld.git
```

If you aren't sure how to use Git, see the bitbucket <a href="http://confluence.atlassian.com/display/BITBUCKET/bitbucket+101" class="external-link">getting started guide</a>. Alternatively, you can download the source using the **get source** option here: <a href="https://bitbucket.org/atlassian_tutorial/helloworld/overview" class="uri external-link">https://bitbucket.org/atlassian_tutorial/helloworld/overview</a>.

## Step 2: Generate Eclipse configuration files

The `helloworld` project you created has everything you need for a Maven project. However, it is not ready to be imported into Eclipse. For that, the first step is to use the `atlas-mvn` command to generate Eclipse configuration files in the project.

1.  Go to your system's command line (DOS prompt for Windows, shell prompt for Linux).
2.  Navigate to the root of your `helloworld` project.  
    This is the directory where the `pom.xml` file is. If you have followed this tutorial exactly up to this point, the directory is `atlastutorial/helloworld`.
3.  Enter the following command:

    ``` bash
    atlas-mvn eclipse:eclipse
    ```

    The command will print some informational messages and then return something like the following:

    ``` bash
    [INFO] Wrote settings to C:\atlastutorial\helloworld\.settings\org.eclipse.jdt.core.prefs
    [INFO] Wrote Eclipse project for "helloworld" to C:\atlastutorial\helloworld.
    [INFO]
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESSFUL
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 37 seconds
    [INFO] Finished at: Sun May 20 17:24:27 PDT 2012
    [INFO] Final Memory: 52M/125M
    [INFO] ------------------------------------------------------------------------
    ```

    This means you are ready for the next step.

## Step 3: Import helloworld into Eclipse

Now, import your project into the Eclipse IDE. Start Eclipse and do the following:

1.  Select **File &gt; Import**.  
    Eclipse starts the Import wizard.
2.  Expand the **General** folder tree.
3.  Filter for **Existing Projects into Workspace** and press **Next**.
4.  Choose **Select root directory** and then **Browse** to the root directory of your workspace.  
    Your Atlassian plugin folder should appear under **Projects**.
5.  Select your plugin project and click **Finish**.  
    Eclipse imports your project.
6.  Navigate to your `atlassian-plugin.xml` file and open it.  
    At this point, your file will look similar to the following:

    ``` xml
    <atlassian-plugin key="${project.groupId}.${project.artifactId}" name="${project.name}" plugins-version="2">
        <plugin-info>
            <description>${project.description}</description>
            <version>${project.version}</version>
            <vendor name="${project.organization.name}" url="${project.organization.url}" />
        </plugin-info>
    </atlassian-plugin>
    ```

## Step 4: Create the Menu

In this step, you add a new menu called **Client Sites** to your project using the `atlas-create-jira-plugin-module` command. The menu will contain a link to Radio Paradise, an online radio station.

1.  Open a command prompt in Eclipse using the launcher on your desktop.  
    You can also just go to a command line outside of Eclipse.
2.  Navigate to your project directory.
3.  Enter the `atlas-create-jira-plugin-module` command.  
    The command prompts you for a module to add.
4.  Select the 30 `Web Section` item by entering `30`.  
    The system prompts you with a series of questions.
5.  Answer each question as follows:

    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>Question</p></th>
    <th><p>Value</p></th>
    <th><p>Description</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Enter Plugin Module Name:</p></td>
    <td><p><code>mySection</code></p></td>
    <td><p>A human-readable name for the section. This is only visible to administrators working with the Universal Plugin Manager (UPM).</p></td>
    </tr>
    <tr class="even">
    <td><p>Enter Location:</p></td>
    <td><p><code>client-sites-link</code></p></td>
    <td><p>A unique location representing this web section.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Show Advanced Setup?</p></td>
    <td><p>N</p></td>
    <td><p>Not applicable for this tutorial</p></td>
    </tr>
    </tbody>
    </table>

    The system displays information about what kinds of changes the additional module generates.

    ``` xml
    Enter Plugin Module Name [My Web Section]: mySection
    Enter Location (e.g. system.admin/mynewsection): client-sites-link
    Show Advanced Setup? (Y/y/N/n) [N]: n
    [INFO] Adding the following items to the project:
    [INFO]   [dependency: org.mockito:mockito-all]
    [INFO]   [module: web-section]
    [INFO]   i18n strings: 3
    Add Another Plugin Module? (Y/y/N/n) [N]: 
    ```

6.  Press Y to add another Plugin Module.  
    A web section simply provides a container for web items. You must add a web-item representing the menu.
7.  Choose `25: Web Item`

    <table>
    <colgroup>
    <col style="width: 33%" />
    <col style="width: 33%" />
    <col style="width: 33%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>Question</p></th>
    <th><p>Value</p></th>
    <th><p>Description</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p>Enter Plugin Module Name</p></td>
    <td><p><code>Client Sites</code></p></td>
    <td><p>This is the name that will appear on the new menu.</p></td>
    </tr>
    <tr class="even">
    <td><p>Enter Section</p></td>
    <td><p><code>system.top.navigation.bar</code></p></td>
    <td><p>The location in the JIRA menu where you want your custom menu to appear.</p></td>
    </tr>
    <tr class="odd">
    <td><p>Enter Link URL</p></td>
    <td><p><code>deleteMe</code></p></td>
    <td><p>More about this later.</p></td>
    </tr>
    <tr class="even">
    <td><p>Show Advanced Setup?</p></td>
    <td><p>N</p></td>
    <td><p>Not applicable for this tutorial</p></td>
    </tr>
    </tbody>
    </table>

    The system displays something similar to the following:

    ``` bash
    [INFO] Adding the following items to the project:
    [INFO]   [dependency: org.mockito:mockito-all]
    [INFO]   [module: web-item]
    [INFO]   i18n strings: 3
    ```

8.  Answer `N` when prompted to add another module.  
    The system completes its operation and provides you with the following informational messages:

    ``` bash
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESSFUL
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 15 minutes 15 seconds
    [INFO] Finished at: Mon May 14 14:29:58 PDT 2012
    [INFO] Final Memory: 41M/117M
    [INFO] ------------------------------------------------------------------------
    ```

## Step 5: Tweak the module description

At this point, you have used the SDK to generate a new module. The generation tools are intended for general cases. This means, that you may occasionally need to edit what was created by a generation command. This is the case for this tutorial. If you haven't already done so, open Eclipse and do the following:

1.  Refresh the Eclipse project.  
    Eclipse picks up the dependency changes in the `pom.xml` and the modules added to the `atlassian-plugin.xml`. The command also added an i18n resource in `src\main\resources\com\atlassian\tutorial` directory called `helloworld.properties`.
2.  Open the `atlassian-plugin.xml` in the **Source** view and look for the web-section and web-item entries.  
    These entries were added for you when you added the modules.  You should see something similar to the following:

    ``` xml
    <atlassian-plugin key="${project.groupId}.${project.artifactId}" name="${project.name}" plugins-version="2">
      
      ... code not shown ...
     
      <!-- publish our component -->
      <component key="myPluginComponent" class="com.atlassian.tutorial.helloworld.MyPluginComponentImpl" public="true">
        <interface>com.atlassian.tutorial.helloworld.MyPluginComponent</interface>
      </component>
      <!-- import from the product container -->
      <component-import key="applicationProperties" interface="com.atlassian.sal.api.ApplicationProperties"/>
      <web-section name="mySection" i18n-name-key="my-section.name" key="my-section" location="client-sites-link" weight="1000">
        <description key="my-section.description">The mySection Plugin</description>
        <label key="my-section.label"/>
      </web-section>
      <web-item name="Client Sites" i18n-name-key="client-sites.name" key="client-sites" section="system.top.navigation.bar" weight="1000">
        <description key="client-sites.description">The Client Sites Plugin</description>
        <label key="client-sites.label"></label>
        <link linkId="client-sites-link">deleteMe</link>
      </web-item>
    </atlassian-plugin>
    ```

    (If you don't see this, make sure you are looking at the **Source** view of the file, not the **Design** view.)  
    By default, the plugin generator adds a `<label>` element to the `web-section`. You won't need this.

3.  Remove the `<label>` element from the `web-section`.
4.  Locate the `<link>` element in the `web-item`.  
    This `web-item` becomes the menu label for your menu. You don't want that item to actually link anywhere. So the `deleteMe` URL value is not necessary.
5.  Remove the URL from the `<link>` element but leave the link item.  
    When you are done the `<link>` element should look like this:

    ``` xml
    <link linkId="client-sites-link"></link>
    ```

6.  Save the `atlassian-plugin.xml` file.  
    Your `atlassian-plugin.xml` descriptor file should look like this:

    ``` xml
     <atlassian-plugin key="${project.groupId}.${project.artifactId}" name="${project.name}" plugins-version="2">
      
      ... code not shown ...
      <web-section name="mySection" i18n-name-key="my-section.name" key="my-section" location="client-sites-link" weight="1000">
        <description key="my-section.description">The mySection Plugin</description>
      </web-section>
      <web-item name="Client Sites" i18n-name-key="client-sites.name" key="client-sites" section="system.top.navigation.bar" weight="1000">
        <description key="client-sites.description">The Client Sites Plugin</description>
        <label key="client-sites.label"></label>
        <link linkId="client-sites-link"></link>
      </web-item>
    </atlassian-plugin>
    ```

## Step 6: View the Menu in JIRA

In this step, you view the menu you just created in JIRA. At this point the menu has no items in it. We'll add one in a moment.

1.  Open a command prompt in the root of your project.
2.  Enter the following to build your plugin JAR:

    ``` bash
    atlas-run
    ```

    The command builds your JAR and the JIRA container in the target directory. When it completes successfully, the command echoes back something similar to the following:

    ``` bash
    [WARNING] [talledLocalContainer] INFO: Server startup in 695 ms
    [INFO] [talledLocalContainer] Tomcat 6.x started on port [2990]
    [INFO] jira started successfully in 46s at http://manthony-PC:2990/jira
    [INFO] Type Ctrl-D to shutdown gracefully
    [INFO] Type Ctrl-C to exit
    ```

3.  Go to a browser and open JIRA.  
    You should see your new "Client Sites" menu immediately.
4.  Click on the menu.  
    Nothing happens except that the page refreshes. Let's fix this.
5.  Leave JIRA up and running and start another command prompt.
6.  Go to the root of your project and add another `web-item` module:

    ``` bash
    atlas-create-jira-plugin-module
    ```

7.  Enter `25: Web Item` when prompted.
8.  Complete the module as follows:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter Plugin Module Name My Web Item:</p></td>
    <td><p><code>Radio Paradise</code></p></td>
    </tr>
    <tr class="even">
    <td><p>Enter Section (e.g. system.admin/globalsettings):</p></td>
    <td><p><code>client-sites-link/my-section</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>Enter Link URL (e.g. /secure/CreateIssue!default.jspa):</p></td>
    <td><p><a href="http://www.radioparadise.com" class="uri external-link">http://www.radioparadise.com</a></p></td>
    </tr>
    <tr class="even">
    <td><p>Show Advanced Setup? (Y/y/N/n) N:</p></td>
    <td><p><code>n</code></p></td>
    </tr>
    </tbody>
    </table>

9.  Enter `n` when prompted to add another module.
10. Go back to Eclipse and refresh the `atlassian-plugin.xml` file.  
    At this point, your file should look like the following:

    ``` xml
    <atlassian-plugin key="${project.groupId}.${project.artifactId}" name="${project.name}" plugins-version="2">
      
      ... code not shown ...
     
    <web-section name="mySection" i18n-name-key="my-section.name" key="my-section" location="client-sites-link" weight="1000">
        <description key="my-section.description">The mySection Plugin</description>
      </web-section>
      <web-item name="Client Sites" i18n-name-key="client-sites.name" key="client-sites" section="system.top.navigation.bar" weight="1000">
        <description key="client-sites.description">The Client Sites Plugin</description>
        <label key="client-sites.label"/>
        <link linkId="client-sites-link"/>
      </web-item>
      <web-item name="Radio Paradise" i18n-name-key="radio-paradise.name" key="radio-paradise" section="client-sites-link/my-section" weight="1000">
        <description key="radio-paradise.description">The Radio Paradise Plugin</description>
        <label key="radio-paradise.label"></label>
        <link linkId="radio-paradise-link">http://www.radioparadise.com</link>
      </web-item>
    </atlassian-plugin>
    ```

## Step 7: Use the FastDev (fast development) feature

At this point, you left code running and made some changes to your code. Rather than rebuild the JAR, use the FastDev feature to reload your changes while JIRA is running.

1.  Return to the browser.
2.  Navigate to the FASTDEV page for your project. The URL for this page has a format of `http://HOSTNAME:PORT/jira/plugins/servlet/fastdev`.  
    For example, you would enter something similar to the following:

    ``` bash
    http://manthony-pc:2990/jira/plugins/servlet/fastdev
    ```

    The FASTDEV dialog appears.

3.  Press **Scan and Reload**.  
    The system scans your projects for changes and reloads them into the JIRA instance. When it completes successfully, you see the following:  
    <img src="/server/framework/atlassian-sdk/images/reloaded.png" width="700" />
4.  Return to the JIRA dashboard and reload it.  
    After the reload your secondary menu should appear:  
    <img src="/server/framework/atlassian-sdk/images/menu-final.png" width="700" />

## Next steps

Congratulations, you have completed the first Atlassian tutorial and added your own custom menu to JIRA.

Where you go now depends upon your interests, but there are many more tutorials to explore. To continue learning with tutorials, follow one of these links:

-   [JIRA tutorials](https://developer.atlassian.com/display/JIRADEV/JIRA+platform)
-   [Confluence Tutorials](https://developer.atlassian.com/display/CONFDEV/Tutorials)


























































































































































































































































































































































