---
aliases:
- /server/framework/atlassian-sdk/44044634.html
- /server/framework/atlassian-sdk/44044634.md
category: devguide
confluence_id: 44044634
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=44044634
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=44044634
date: '2017-12-11'
guides: tutorials
legacy_title: Create a Confluence 'Hello World' Macro
platform: server
product: atlassian-sdk
subcategory: learning
title: Create a Confluence 'Hello World' macro
---
# Create a Confluence 'Hello World' macro

This tutorial builds on the concepts introduced in [Set Up the Atlassian SDK and Build a Project](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project). You'll delve a little deeper into the SDK environment and so to complete this tutorial successfully, you should have already installed the SDK and created a plugin project. 

 

## About this tutorial

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td>Pre requisites</td>
<td><ul>
<li>Atlassian Plugin SDK 6.2.x</li>
<li>Oracle Java JDK 8</li>
<li>It's a good idea to have completed <a href="https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project">Set Up the Atlassian SDK and Build a Project</a></li>
<li>A basic understanding of Java, javascript and css</li>
</ul></td>
</tr>
<tr class="even">
<td>Experience Level</td>
<td>BEGINNER</td>
</tr>
<tr class="odd">
<td>Recommended Environment</td>
<td><ul>
<li>Atlassian Plugin SDK 6.2.9</li>
<li>AMPS Version 6.2.6</li>
<li>Confluence Version</li>
</ul></td>
</tr>
<tr class="even">
<td>Source</td>
<td><a href="https://bitbucket.org/serverecosystem/myconfluencemacro/src" class="uri external-link">https://bitbucket.org/serverecosystem/myconfluencemacro/src</a></td>
</tr>
</tbody>
</table>

 

## Create the plugin skeleton

Just like in the last tutorial, you'll use the Atlassian Plugin SDK to create a skeleton for our plugin.  This time you will use the `atlas-create-confluence-plugin` command because you're creating a plugin to work in Confluence.

{{% tip %}}

You can find a list of all the **atlas-** commands in the [Command reference](https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference)

{{% /tip %}}

1.  Open a terminal window and navigate to the directory where you'd like to create your plugin.
2.  Run the command `atlas-create-confluence-plugin` and fill in the plugin details as follows:

    ``` bash
    Define value for groupId: : com.atlassian.tutorial
    Define value for artifactId: : myConfluenceMacro
    Define value for version:  1.0.0-SNAPSHOT: : 
    Define value for package:  com.atlassian.tutorial: : 
    Confirm properties configuration:
    groupId: com.atlassian.tutorial
    artifactId: myConfluenceMacro
    version: 1.0.0-SNAPSHOT
    package: com.atlassian.tutorial
     Y: : Y
    ```

3.  The plugin skeleton will be created automatically and you'll receive a confirmation message as follows:

    ``` bash
    [INFO] ------------------------------------------------------------------------
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 02:53 min
    [INFO] Finished at: 2016-10-10T15:39:56+10:00
    [INFO] Final Memory: 16M/309M
    [INFO] ------------------------------------------------------------------------
    ```

4.  Now, navigate to the **myConfluenceMacro** directory that was created by the Atlassian Plugin SDK in the last step. 
5.  Update the organization details for your plugin in the pom.xml file (see [modify the plugin - step 1](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/modify-the-plugin#ModifythePlugin-Step1.UpdatetheorganizationdetailsthatappearonthePlugin) from the [Set up the Atlassian Plugin SDK and Build a Project tutorial](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project) if you're stuck).
6.  Start up confluence with your plugin installed (and download all the necessary files to do that) by running the command `atlas-run.`
7.  Check that Confluence started up with your plugin installed by navigating to <a href="http://localhost:1990/confluence/plugins/servlet/upm/manage/all" class="uri external-link">http://localhost:1990/confluence/plugins/servlet/upm/manage/all</a> (you can login using **username: admin, password: admin** just like you did in the last tutorial).
8.  Leave Confluence up and running now

## Create a Macro Element in Confluence

In the previous tutorial, we used the `atlas-create-jira-plugin-module` command to create a JIRA menu module which we then customised.  This command essentially modified the** /src/main/resources/atlassian-plugin.xml** file in your plugin directory to create some extra elements in JIRA.  

In this tutorial, you will create the plugin elements manually rather than using an SDK command.  This is because `atlas-create-confluence-plugin-module` command doesn't have an option for the Module type you need to use.

1.  Open the **atlassian-plugin.xml **file in your favourite editor.
2.  Locate the end of the &lt;web-resource&gt;...&lt;/web-resource&gt; section in the file and enter the following:

    ``` xml
    <xhtml-macro name="helloworld" class="com.atlassian.tutorial.macro.helloworld" key='helloworld-macro'>
        <description key="helloworld.macro.desc"/>
        <category name="formatting"/>
        <parameters/>
    </xhtml-macro>
    ```

    save the changes to your file.  Note: your macro name and macro key should both be lower case. 

3.  Open the file **/src/main/resources/myConfluenceMacro.properties** and add the following line at the bottom of the file:

    ``` bash
    helloworld.macro.desc="Hello World"
    ```

    save the changes to you file. 

4.  Next you need to create the java class that you made reference to in Step 2. Because you'll be creating a couple of macros in this tutorial, you can create a **macro **folder to keep things tidy.
5.  Open a new terminal window so you can create a new folder in the **/src/main/java/com/atlassian/tutorial **directory called **macro**:

     

    ``` bash
    cd /src/main/java/com/atlassian/tutorial
    mkdir macro
    cd macro
    ```

6.  In the folder, create a file called **helloworld.java** and open it in your favourite editor.

7.  Enter the following code into **helloworld.java**:

    ``` java
    package com.atlassian.tutorial.macro;

    import com.atlassian.confluence.content.render.xhtml.ConversionContext;
    import com.atlassian.confluence.macro.Macro;
    import com.atlassian.confluence.macro.MacroExecutionException;

    import java.util.Map;

    public class helloworld implements Macro {

        public String execute(Map<String, String> map, String s, ConversionContext conversionContext) throws MacroExecutionException {
            return "<h1>Hello World</h1>";
        }

        public BodyType getBodyType() { return BodyType.NONE; }

        public OutputType getOutputType() { return OutputType.BLOCK; }
    }
    ```

    This is the minimum skeleton your Macro will require to implement the [confluence Macro class](https://developer.atlassian.com/static/javadoc/confluence/4.0/reference/com/atlassian/confluence/macro/Macro.html) and display a Macro object in Confluence.  

8.  In your terminal window, change directory back to the top directory for your plugin (eg `cd <home>/AtlassianTutorial/myConfluenceMacro`)
9.  Run the command `atlas-mvn package` to re-package your add-on and reinstall it using QuickReload. You should see a confirmation message:

    ``` bash
    [INFO] BUILD SUCCESS
    [INFO] ------------------------------------------------------------------------
    [INFO] Total time: 4.656 s
    [INFO] Finished at: 2016-10-10T18:33:09+10:00
    [INFO] Final Memory: 37M/433M
    [INFO] ------------------------------------------------------------------------
    ```

10. Monitor the window where confluence was run originally and confirm that QuickReload finished loading. You should see a confirmation message:

    ``` bash
    [INFO] [talledLocalContainer] 2016-10-10 18:33:16,082 INFO [QuickReload - Plugin Installer] [atlassian.plugin.manager.DefaultPluginManager] updatePlugin Updating plugin 'com.atlassian.tutorial.myConfluenceMacro-tests' from version '1.0.0-SNAPSHOT' to version '1.0.0-SNAPSHOT'
    [INFO] [talledLocalContainer] 2016-10-10 18:33:16,083 INFO [QuickReload - Plugin Installer] [atlassian.plugin.manager.DefaultPluginManager] broadcastPluginDisabling Disabling com.atlassian.tutorial.myConfluenceMacro-tests
    [INFO] [talledLocalContainer] 2016-10-10 18:33:17,512 INFO [QuickReload - Plugin Installer] [plugins.quickreload.install.PluginInstallerMechanic] installPluginImmediately 
    [INFO] [talledLocalContainer]                       ^
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer] 
    [INFO] [talledLocalContainer]       A watched plugin never boils!
    [INFO] [talledLocalContainer] 
    [INFO] [talledLocalContainer] Quick Reload Finished (5954 ms) - 'myConfluenceMacro-1.0.0-SNAPSHOT-tests.jar'
    ```

11. Now you can try adding the Macro to a test page in Confluence (you'll need to make a new Confluence Space and Page before you can test it out so go ahead and do that first).

    {{% note %}}

    Note

    Note: It can take the Confluence macro browser a little bit of time to realise that there's a new macro available, so if it doesn't show up right away give it a little while and try again.  

    {{% /note %}}

    <img src="/server/framework/atlassian-sdk/images/confluence-macro-browser-showing-helloworld-macro.png" title="Macro Browser" alt="Confluence macro browser showing helloworld macro" width="500" height="305" />  
    <img src="/server/framework/atlassian-sdk/images/helloworld-macro-on-page-in-edit-view.png" title="Helloworld Macro - Edit Mode" alt="Helloworld macro showing on confluence page in edit mode" width="500" height="268" />

    <img src="/server/framework/atlassian-sdk/images/helloworld-macro-showing-message-after-saving-page.png" title="Helloworld Macro - Confluence Page" alt="Helloworld Macro shown on Confluence page that has been saved" width="880" height="250" />

## Customize the Hello World macro

Now, you will allow the user to specify their name using a parameter to learn about how parameters can be set, and used.

1.  Open the **atlassian-plugin.xml **file in your favourite editor.
2.  Locate the `<parameters/>` element within the` <xhtml-macro>` element you created in the first part of this tutorial.  
3.  Replace the `<parameters/>` element with the following:

    ``` xml
    <parameters>
        <parameter name="Name" type="string" />
    </parameters>
    ```

    This specifies that the parameter is called 'Name' and is of type 'string'.  You can find the full list of types under the **Parameters** heading in the [macro module documentation](https://developer.atlassian.com/confdev/confluence-plugin-guide/confluence-plugin-module-types/macro-module/including-information-in-your-macro-for-the-macro-browser)

4.  Save and close the changes you made to **atlassian-plugin.xml**
5.  Open **helloworld.java **(it'll be in the /src/main/java/com/atlassian/tutorial/macro directory)
6.  Modify the **execute **function as follows:

    ``` java
    public String execute(Map<String, String> map, String s, ConversionContext conversionContext) throws MacroExecutionException {
        if (map.get("Name") != null) {
            return ("<h1>Hello " + map.get("Name") + "!</h1>");
        } else {
            return "<h1>Hello World!<h1>";
        }
    }
    ```

7.  Save your changes to **helloworld.java**
8.  In your terminal window, make sure you're in the top directory for your project (eg &lt;home&gt;/AtlassianTutorial/myConfluenceMacro) and run the command:

    ``` bash
    atlas-mvn package
    ```

9.  Monitor the terminal window where Confluence is running to confirm that the plugin has been reloaded by QuickReload.  
10. Log in and check your changes are working:  
    <img src="/server/framework/atlassian-sdk/images/updated-macro---macro-editor.png" width="462" height="250" />  
    <img src="/server/framework/atlassian-sdk/images/updated-macro---confluence-editor.png" width="466" height="250" />  
    <img src="/server/framework/atlassian-sdk/images/updated-macro---saved-macro-test-page.png" width="754" height="250" />

## Format the macro appearance using css

At the moment, all the formatting work is being done in the **execute **function. In this section you'll set up a [Web Resource Plugin Module](/server/framework/atlassian-sdk/web-resource-plugin-module) to allow css to control the appearance of your macro.  

1.  Open the **atlassian-plugin.xml **file in your favourite editor.
2.  Notice that the &lt;`web-resource> `parameter already exists:

    ``` xml
    <web-resource key="myConfluenceMacro-resources" name="myConfluenceMacro Web Resources">
        <dependency>com.atlassian.auiplugin:ajs</dependency>
        
        <resource type="download" name="myConfluenceMacro.css" location="/css/myConfluenceMacro.css"/>
        <resource type="download" name="myConfluenceMacro.js" location="/js/myConfluenceMacro.js"/>
        <resource type="download" name="images/" location="/images"/>

        <context>myConfluenceMacro</context>
    </web-resource>
    ```

    In this tutorial you don't need to make any changes to the web-resource module itself. 

3.  Below your `<parameter name="Name" type="string" />`, add a new `<parameter name="Color" type="enum">` as follows:

    ``` xml
    <parameter name="Color" type="enum">
        <value name="red"/>
        <value name="green"/>
        <value name="blue"/>
    </parameter>
    ```

    This will create a drop down menu in the macro editor for the user to select their color as either red, green or blue. 

4.  Save your changes to atlassian-plugin.xml and close the file.
5.  Next, open the **src/main/resources/css/myConfluenceMacro.css** file
6.  Add the following css to the file:

    ``` css
    .blue h1 {
        color: blue;
    }

    .red h1 {
        color: red;
    }

    .green h1 {
        color: green;
    }
    ```

     This css will change the text colour for a .blue, .green and .red h1 element (once you've updated your helloworld.java of course).

7.  Save your changes to myConfluenceMacro.css and close the file. 
8.  Now, open the **src/main/java/com/atlassian/tutorial/macro/helloworld.java** file. 
9.  Modify the **execute **function to create &lt;div&gt; elements as follows:

    ``` java
    public String execute(Map<String, String> map, String s, ConversionContext conversionContext) throws MacroExecutionException {
        String output = "<div class =\"helloworld\">";
        output = output + "<div class = \"" + map.get("Color") + "\">";
        if (map.get("Name") != null) {
            output = output + ("<h1>Hello " + map.get("Name") + "!</h1>");
        } else {
            output = output + "<h1>Hello World!<h1>";
        }
        output = output + "</div>" + "</div>";
        return output;
    }
    ```

    Notice that you are now creating a &lt;div .../&gt; element with a class matching the users nominated color.

10. Next, under the existing imports in your java file, add the following new lines:

    ``` java
    import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
    import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
    import com.atlassian.webresource.api.assembler.PageBuilderService;
    import org.springframework.beans.factory.annotation.Autowired;
    ```

    These are required so you can use <a href="https://bitbucket.org/atlassian/atlassian-spring-scanner" class="external-link">spring scanner</a>, along with the PageBuilderService to ensure the css you've created is being included in Confluence.  

11. Above the `public class helloworld implements Macro` definition, add the following Spring annotations:

    ``` java
    @Scanned
    ```

    The `@scanned` annotation is an instruction for <a href="https://bitbucket.org/atlassian/atlassian-spring-scanner" class="external-link">spring scanner</a>.  In this tutorial we used spring scanner 1.2.13 - so we needed to tell spring scanner to scan this class. 

12. Now, within the `helloworld` class definition, add a `PageBuilderService` variable, as well as a constructor for your `helloworld` class as follows:

    ``` java
    public class helloworld implements Macro {

        private PageBuilderService pageBuilderService;

        @Autowired
        public helloworld(@ComponentImport PageBuilderService pageBuilderService) {
            this.pageBuilderService = pageBuilderService;
        }
    ```

    The pageBuilderService is required for the [Web Resource Plugin Module](/server/framework/atlassian-sdk/web-resource-plugin-module)  

13. Finally, add the following line to your execute function:

    ``` java
    pageBuilderService.assembler().resources().requireWebResource("com.atlassian.tutorial.myConfluenceMacro:myConfluenceMacro-resources");
    ```

    Notice that you're using the pageBuilderService to require the web-resource key that was generated automatically (see step 2).

14. Save your changes and run `atlas-mvn package` to update your plugin.  

15. Make sure your plugin is working with the new changes:

    {{% note %}}

    Note

    You might need to hold down the shift key while reloading the page to see the changes to the page itself!

    {{% /note %}}

      
    <img src="/server/framework/atlassian-sdk/images/final-changes-with-css.png" width="502" height="250" />

## Need Help?

The source code for this tutorial is available <a href="https://bitbucket.org/serverecosystem/myconfluencemacro/src" class="external-link">on Bitbucket</a>  

Or, check out the questions on <a href="http://answers.atlassian.com/" class="external-link">Atlassian Answers</a> or create a request in our <a href="https://ecosystem.atlassian.net/servicedesk/customer/portal/14" class="external-link">Developer Technical Support Portal</a>.

## Resources

-   The source code for this tutorial is available <a href="https://bitbucket.org/serverecosystem/myconfluencemacro/src" class="external-link">on Bitbucket</a>  
-   You can find documentation for Spring Scanner at <a href="https://bitbucket.org/atlassian/atlassian-spring-scanner" class="uri external-link">https://bitbucket.org/atlassian/atlassian-spring-scanner</a>
-   Learn more about the [Web Resource Plugin Module](/server/framework/atlassian-sdk/web-resource-plugin-module)
-   [L](https://developer.atlassian.com/confdev/confluence-plugin-guide/confluence-plugin-module-types/macro-module/including-information-in-your-macro-for-the-macro-browser)earn more about the [Macro Module](https://developer.atlassian.com/confdev/confluence-plugin-guide/confluence-plugin-module-types/macro-module)



















































































































































































