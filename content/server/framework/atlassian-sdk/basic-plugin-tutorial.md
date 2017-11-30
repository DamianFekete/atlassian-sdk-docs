---
aliases:
- /server/framework/atlassian-sdk/basic-plugin-tutorial-13631708.html
- /server/framework/atlassian-sdk/basic-plugin-tutorial-13631708.md
category: devguide
confluence_id: 13631708
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=13631708
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=13631708
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/creating-an-admin-configuration-form/basic-plugin-tutorial
new_url: /server/framework/atlassian-sdk/basic-plugin-tutorial
platform: server
product: atlassian-sdk
subcategory: other
title: Basic plugin tutorial
---
# Basic plugin tutorial

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Applicable:</p></td>
<td><p>This tutorial applies to JIRA 5.0 or higher.</p></td>
</tr>
<tr class="even">
<td><p>Level of experience:</p></td>
<td><p>This is an advanced tutorial. You should have completed at least one intermediate tutorial before working through this tutorial. See the <a href="/server/framework/atlassian-sdk/tutorials">list of tutorials in DAC</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Time estimate:</p></td>
<td><p>It should take you approximately 1 hour to complete this tutorial.</p></td>
</tr>
</tbody>
</table>

 

## Overview of the Tutorial

This tutorial shows you how to PLUGIN PURPOSE in HOST APPLICATION. Your completed plugin will consist of the following components:

-   Java classes encapsulating the plugin logic.
-   Resources for display of the plugin UI.
-   A plugin descriptor (XML file) to enable the plugin module in the Atlassian application.

When you are done, all these components will be packaged in a single JAR file.

### Prerequisite Knowledge

To complete this tutorial, you must already understand the basics of Java development: classes, interfaces, methods, how to use the compiler, and so on. You should also understand:

-   -   Java classes encapsulating the plugin logic
    -   Resources for display of the plugin UI
    -   Plugin descriptor to enable the plugin module in Atlassian applications

All these components will be contained within a single JAR file. Each component is further discussed in the examples below.

We'll be making extensive use of [SAL](/server/framework/atlassian-sdk/about-sal-development), which exports a bunch of services that can be used for persistence, user authorization, and other common tasks in a way that will work in any Atlassian application.

For rendering the form, we'll use the <a href="https://studio.atlassian.com/wiki/display/ATR/Home" class="external-link">Atlassian Template Renderer</a>. ATR is a plugin that provides services to other plugins that allow them to render templates, typically in Velocity.

For styling our forms to make them look good and for communicating with the server via ajax, we'll be using <a href="https://studio.atlassian.com/browse/AJS" class="external-link">AUI</a>.

To create our REST resources, which our JavaScript will communicate with, we'll use the [REST module](/server/framework/atlassian-sdk/rest-plugin-module).

### Plugin Source

We encourage you to work through this tutorial. If you want to skip ahead or check your work when you are done, you can find the plugin source code on Atlassian Bitbucket. Bitbucket serves a public Git repository containing the tutorial's code. To clone the repository, issue the following command:

``` bash
git clone https://bitbucket.org/atlassian_tutorial/REPO_NAME
```

Alternatively, you can download the source using the **get source** option here: <a href="https://bitbucket.org/atlassian_tutorial/REPO_NAME" class="uri external-link">https://bitbucket.org/atlassian_tutorial/REPO_NAME</a>. You can check out the source code <a href="http://svn.atlassian.com/svn/public/contrib/tutorials/xproduct-admin-ui-plugin" class="external-link">here</a>.

{{% note %}}

About these Instructions

You can use any supported combination of OS and IDE to construct this plugin. These instructions were written using Eclipse Classic Version 3.7.1 on a MacBook Air running Mac OS X. If you are using another combination, you should use the equivalent operations for your specific environment.

{{% /note %}}

## Step 1. Create the Plugin Project

In this step, you'll use the two `atlas-` commands to generate stub code for your plugin and setup the stub code as an Eclipse project. The `atlas-` commands are part of the Atlassian Plugin SDK, and automate much of the work of plugin development for you.

1.  Open a terminal and navigate to your Eclipse workspace directory.
2.  Enter the following command to create a XXX plugin skeleton:

    ``` bash
    atlas-create-refapp-plugin
    ```

    When prompted, enter the following information to identify your plugin:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>group-id</p></td>
    <td><p><code>com.atlassian.plugins.tutorial.refapp</code></p></td>
    </tr>
    <tr class="even">
    <td><p>artifact-id</p></td>
    <td><p>adminUI</p></td>
    </tr>
    <tr class="odd">
    <td><p>version</p></td>
    <td><p><code>1.0-SNAPSHOT</code></p></td>
    </tr>
    <tr class="even">
    <td><p>package</p></td>
    <td><p><code>com.atlassian.plugins.tutorial.refapp.adminui</code></p></td>
    </tr>
    </tbody>
    </table>

3.  Confirm your entries when prompted.
4.  Change to the adminUI directory created by the previous step.
5.  Run the command:

    ``` bash
    atlas-mvn eclipse:eclipse
    ```

6.  Start Eclipse.
7.  Select **File-&gt;Import**.   
    Eclipse starts the **Import** wizard.
8.  Filter for **Existing Projects into Workspace** (or expand the **General** folder tree).
9.  Press **Next** and enter the root directory of your workspace.   
    Your Atlassian plugin folder should appear under **Projects**.
10. Select your plugin and click **Finish**.   
    Eclipse imports your project.

#### What the Plugin Generator Creates

-   **pom.xml** - a Maven project object model (POM) file
-   **src/main/rec/atlassian-plugin.xml** - an Atlassian plugin descriptor file
-   **src/main/java/com/atlassian/plugins/tutorial/refapp/** - **Directory Containing Source Files**
    -   **MyPlugin.java** - a file to hold the plugin source code
-   **src/test/java/com/atlassian/plugins/tutorial/refapp/adminui** - **Directory Containing Test Files**
    -   **MyPluginTest.java** - a test file  
-   **src/test/java/it** - **Directory Containing Test Files**
    -   **MyPluginTest.java** - a test file

## Step 2. Review and Tweak (Optional) the Generated Stub Code

It is a good idea to familiarize yourself with the stub plugin code. In this section, we'll check a version value and tweak a generated stub class. Open your plugin project in Eclipse and follow along in the next sessions to tweak some.

### Add Plugin Metadata to the POM

Now you need to edit your POM (Project Object Model definition file) to add some metadata about your plugin and your company or organisation.

1.  Edit the `pom.xml` file in the root folder of your plugin.
2.  Add your company or organisation name and your website to the `<organization>`element:

    ``` xml
     <organization> 
        <name>Example Company</name> 
        <url>http://www.example.com/</url> 
    </organization> 
    ```

3.  Update the `<description>`element:

    ``` xml
     <description>This plugin has an admin UI that can be used in any Atlassian product.</description> 
    ```

4.  Save the file.

### Verify Your JIRA Version

When you generated the stub files, a default JIRA version was included in your `pom.xml` file (Project Object Model definition file). This file is located at the root of your project and declares the project dependencies. Take a moment and examine the JIRA dependency:

1.  Open the `pom.xml` file.
2.  Scroll to the bottom of the file.
3.  Find the `<properties>` element.  
    This section lists the version of the JIRA and also the version of the `atlas-` commands you are running.
4.  Verify that the JIRA version is the one you want.
5.  Save the `pom.xml` file

### Review the Generated Plugin Descriptor

Your stub code contains a plugin descriptor file `atlassian-plugin.xml`. This is an XML file that identifies the plugin to the host application (JIRA) and defines the required plugin functionality. In your IDE, open the descriptor file which is located in your project under `src/main/resources` and you should see something like this:

``` xml
<atlassian-plugin key="${project.groupId}.${project.artifactId}" name="${project.artifactId}" plugins-version="2">
    <plugin-info>
        <description>${project.description}</description>
        <version>${project.version}</version>
        <vendor name="${project.organization.name}" url="${project.organization.url}" />
    </plugin-info>
</atlassian-plugin>
```

## Step 3. Add a Servlet Module

For this tutorial, you will need a [Servlet plugin module](https://developer.atlassian.com/display/JIRADEV/Servlet+Plugin+Module). You'll add this the `atlas-create-refapp-plugin-module` command.

1.  Open a command window and go to the plugin root folder (where the `pom.xml` is located).
2.  Run `atlas-create-refapp-plugin-module`.

3.  Choose the option labeled `21: Servlet`.
4.  Supply the following information as prompted:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter New Classname</p></td>
    <td><p><code>MyServlet</code> (This is the default.)</p></td>
    </tr>
    <tr class="even">
    <td><p>Package Name</p></td>
    <td><p><code>com.atlassian.plugins.tutorial.refapp.adminui.servlet</code></p></td>
    </tr>
    </tbody>
    </table>

5.  Choose `N` for **Show Advanced Setup**.
6.  Choose `N` for **Add Another Plugin Module**.
7.  Confirm your choices.  
    The generation runs and the command exits. 
8.  At the root of your project directory, run the command:

    ``` bash
    atlas-mvn eclipse:eclipse
    ```

    This command updates the `.classpath`and other key Eclipse resources. 

9.  Return to Eclipse and **Refresh** your project.

{{% note %}}

Remember to run `atlas-mvn eclipse:eclipse` and refresh step each time you edit your `pom.xml` and or modify your plugin source with an Atlassian command. It will ensure that your Eclipse project has what it needs.

{{% /note %}}

#### What the Module Generator Did

Each module generator does generates a different structure and modifications.  This generator did the following:

-   **pom.xml** - added the servlet depedencies
-   **src/main/rec/atlassian-plugin.xml** - added servlet resources
-   **src/main/java/com/atlassian/plugins/tutorial/refapp/** - **Directory**
    -   **adminUI.properties** - a file for internationalization strings
    -   **servlet/MyServlet.java** - a file containing servlet code  
-   **src/test/java/com/atlassian/plugins/tutorial/refapp/adminui** - **Directory**
    -   ****servlet/MyServletTest**.java** - a test file
-   **src/test/java/it** - **Directory**
    -   ****com/atlassian/plugins/tutorial/refapp/adminui/servlet/**MyServletFuncTest.java** - a test file

This module generation added the following dependencies to the project `pom.xml` file:

``` xml
  <dependency>
     <groupId>javax.servlet</groupId>
     <artifactId>servlet-api</artifactId>
     <version>2.4</version>
     <scope>provided</scope>
 </dependency>
 <dependency>
     <groupId>org.apache.httpcomponents</groupId>
     <artifactId>httpclient</artifactId>
     <version>4.1.1</version>
     <scope>test</scope>
 </dependency>
 <dependency>
     <groupId>org.mockito</groupId>
     <artifactId>mockito-all</artifactId>
     <version>1.8.5</version>
     <scope>test</scope>
 </dependency>
```

The `javax.servlet` has a scope of `provided`. Maven resolves this for your locally for you to compile your plugin. At runtime, the OSGi service platform provided by Apache Felix container resolves this dependency.  The `test` scope for the `org.apache.httpcomponents` and the `org.mockito` dependencies tells Maven that the dependency need only be available for the testing phases. Apache Felix does not need to resolve these.

The generated also added a number o the `atlassian-plugin.xml` descriptor file, the generator added the following:

``` xml
<resource type="i18n" name="i18n" location="com.atlassian.plugins.tutorial.refapp.adminUI"/>
<servlet name="My Servlet" i18n-name-key="my-servlet.name" key="my-servlet" class="com.atlassian.plugins.tutorial.refapp.adminui.servlet.MyServlet">
    <description key="my-servlet.description">The My Servlet Plugin</description>
    <url-pattern>/myservlet</url-pattern>
</servlet>
```

The i18n resource supports internationalization of the servlet UI.   The 

## Step 4. Build, install and run the plugin

Follow these steps to build and install your plugin, so that you can test your code.

1.  Make sure you have saved all your code changes to this point.
2.  Open a terminal window and navigate to the plugin root folder (where the `pom.xml` file is).
3.  Run the following command:

    ``` bash
    atlas-run
    ```

    This command builds your plugin code, starts a refapp instance, and installs your plugin in it. This may take several seconds. When the process has finished, you will see many status lines on your screen concluding with something like the following:

    ``` bash
    [INFO] HOSTAPP started successfully in 71s at http://localhost:XXXX/HOSTAPP
    [INFO] Type CTRL-D to shutdown gracefully
    [INFO] Type CTRL-C to exit
    ```

4.  Open your browser and navigate to the local refapp instance started by `atlas-run`.  
    For example, the default address is <a href="http://localhost:2990/jira" class="external-link">http://localhost:2990/refapp</a> for refapp. See [Plugin SDK Supported Applications and Default Ports](/server/framework/atlassian-sdk/-plugin-sdk-supported-applications-and-default-ports-2818466.html) for other applications.
5.  At the refapp login screen, enter a username of `admin` and a password of `admin`. 
6.  Navigate to your servlet location:  
    <a href="http://localhost:2990/jira/plugins/servlet/myservlet" class="uri external-link">http://localhost:2990/jira/plugins/servlet/myservlet</a>   
    You should see something similar to the following:  
     <img src="/server/framework/atlassian-sdk/images/baseline-servlet.png" width="500" />  
      

At this point, all of your servlet code is generated. You haven't added any bells and whistles. Things are about to change.

## Step 5. Add Velocity and User Management Modules

By default, the servlet module is not pre-configured to use Velocity templates (Atlassian's preferred template engine for servlets). Let's set up Velocity so that we don't write HTML inside our servlet code. We'll use the plugin module generator to import the `TemplateRenderer` which imports the Velocity template renderer. We'll also import `UserManager` a feature of the shared access layer (SAL) that will allow us to get information about the logged in user. To add these components, do the following:

1.  Open a command window and go to the plugin root folder (where the `pom.xml` is located).
2.  Run `atlas-create-refapp-plugin-module`.
3.  Choose the option labeled `Component Import`.
4.  Follow the prompts to add the `TemplateRenderer`

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter the fully qualified path name</p></td>
    <td><p><code>com.atlassian.templaterenderer.TemplateRenderer</code></p></td>
    </tr>
    <tr class="even">
    <td><p>Module Key</p></td>
    <td><p>Press return to take the default <code>TemplateRenderer</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>Filter (not require)</p></td>
    <td><p>Press return to accept the default which is none.</p></td>
    </tr>
    </tbody>
    </table>

5.  Choose `Y` for **Add Another Plugin Module**.
6.  Choose the option labeled `Component Import`.
7.  Follow the prompts to add the `UserManager`

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter the fully qualified path name</p></td>
    <td><p><code>com.atlassian.sal.api.user.UserManager</code></p></td>
    </tr>
    <tr class="even">
    <td><p>Module Key</p></td>
    <td><p>Press return to take the default <code>userManager</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>Filter (not require)</p></td>
    <td><p>Press return to accept the default which is none.</p></td>
    </tr>
    </tbody>
    </table>

8.  Choose `Y` for **Add Another Plugin Module**.
9.  Choose the option labeled `Component Import`.
10. Follow the prompts to add the `UserManager`

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter the fully qualified path name</p></td>
    <td><pre><code>com.atlassian.sal.api.auth.LoginUriProvider</code></pre></td>
    </tr>
    <tr class="even">
    <td><p>Module Key</p></td>
    <td><p>Press return to take the default <code>loginUriProvider</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>Filter (not require)</p></td>
    <td><p>Press return to accept the default which is none.</p></td>
    </tr>
    </tbody>
    </table>

11. `Y` for **Add Another Plugin Module**.  
    Allow the generation to finish. The generator updates your `atlassian-plugin.xml` with a component for the `TemplateRenderer` and two for SAL:

    ``` xml
     <component-import key="templateRenderer" interface="com.atlassian.templaterenderer.TemplateRenderer" filter=""/>
     <component-import key="userManager" interface="com.atlassian.sal.api.user.UserManager" filter=""/>
     <component-import key="loginUriProvider" interface="com.atlassian.sal.api.auth.LoginUriProvider" filter=""/>
    ```

    The `component-import` plugin module allows you to access Java components shared by other plugins, even if the component is upgraded at runtime. 

### Update your dependencies

1.  Open the `pom.xml` file inside the root of your project.
2.  Find the `<dependencies>` section.
3.  Insert the following inside the `<dependencies>`section:

    ``` xml
    <dependency>
      <groupId>com.atlassian.templaterenderer</groupId>
      <artifactId>atlassian-template-renderer-api</artifactId>
      <version>1.3.1</version>
      <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.sal</groupId>
        <artifactId>sal-api</artifactId>
        <version>2.7.1</version>
        <scope>provided</scope>
    </dependency>
    ```

4.  Save your file.
5.  Return to your terminal.
6.  At the root of your project directory, run the command:

    ``` bash
    atlas-mvn eclipse:eclipse
    ```

    This command updates the `.classpath`and other key Eclipse resources. 

7.  Return to Eclipse and **Refresh** your project.

## Step 6. Update Your Servlet Code

In this step, you use code from the SAL and template renderer dependencies to add functionality to your plugin.

### Add a Check for Admin Privileges 

The shared access layer (SAL) gives your plugin access to the most common Atlassian services. These servers include but are not limited to:

-   job scheduling
-   internationalization lookups
-   persistence for plugin settings
-   plugin upgrade framework

Because this project creates an admin page, the servlet should check that the user is an administrator.  The SAL <a href="http://docs.atlassian.com/sal-api/2.0.16-SNAPSHOT/com/atlassian/sal/api/user/UserManager.html" class="external-link"><code>UserManager</code></a> provides that functionality to your servlet.  In Eclipse, locate the `MyServlet.java` class and do the following:

1.  Add the following additional `import` listings to your class:

    ``` bash
    import java.net.URI;
    import com.atlassian.sal.api.auth.LoginUriProvider;
    import com.atlassian.sal.api.user.UserManager;
    ```

2.  Add the following fields and constructor to your `MyServlet` class:

    ``` java
        private final UserManager userManager;
        private final LoginUriProvider loginUriProvider;
        
        public MyServlet(UserManager userManager, LoginUriProvider loginUriProvider)
        {
            this.userManager = userManager;
            this.loginUriProvider = loginUriProvider;
        }
    ```

    The constructor instantiates an instance of the `UserManager and a loginUriProvider.`

3.  Replace the generated `doGet` method with the following:

    ``` java
    public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException
        {
            String username = userManager.getRemoteUsername(request);
            if (username == null || !userManager.isSystemAdmin(username))
            {
                redirectToLogin(request, response);
                return;
            }
            response.setContentType("text/html");
            response.getWriter().write("<html><body>Hello World</body></html>");
        }
    ```

    The `doGet` method uses `getRemoteUsername` to check that the user is logged in (the username is not `null`)` `and that the user is an administrator (`isSystemAdmin`). If the user is neither logged in or an administrator, the code calls redirectToLogin to  call a helper method to redirect the user to the application login page.

4.  Add the `redirectToLogin` method and its supporting `getURI` method to the `MyServlet` class:

    ``` java
    private void redirectToLogin(HttpServletRequest request, HttpServletResponse response) throws IOException
        {
            response.sendRedirect(loginUriProvider.getLoginUri(getUri(request)).toASCIIString());
        }
      
        private URI getUri(HttpServletRequest request)
        {
            StringBuffer builder = request.getRequestURL();
            if (request.getQueryString() != null)
            {
                builder.append("?");
                builder.append(request.getQueryString());
            }
            return URI.create(builder.toString());
        } 
    ```

    The `redirectToLogin` method uses another service provided by SAL, the <a href="http://docs.atlassian.com/sal-api/2.0.16-SNAPSHOT/com/atlassian/sal/api/auth/LoginUriProvider.html" class="external-link"><code>LoginUriProvider</code></a>. The servlet uses this API to construct a URI to the application's login page. The method also provides the page with a URI parameter representing the page the user is redirected to. The servlet passes it the current URI redirecting the user back to the admin UI where they can properly authenticate. Passing a `LoginUriProvider` instance to the constructor ensures that the UI is injected by the plugin system.

5.  Close and save the `MyServlet.java` file.

### Create a Velocity Template for the Page

1.  Create an `admin.vm` file in `PLUGIN_ROOT/src/main/resources` directory.
2.  Edit the file.
3.  Add the following code to the file:

    ``` xml
    <html>
      <head>
        <title>My Admin</title>
      </head>
      <body>
        <form id="admin">
          <div>
            <label for="name">Name</label>
            <input type="text" id="name" name="name">
          </div>
          <div>
            <label for="age">Age</label>
            <input type="text" id="age" name="age">
          </div>
          <div>
            <input type="submit" value="Save">
          </div>
        </form>
      </body>
    </html>
    ```

    This velocity template renders a simple HTML form that looks like the following:  
     ![](/server/framework/atlassian-sdk/images/screenshot-017.png)

4.  Close and save the `admin.vm` file.

### Render the Form in Your Servlet

You use the Atlassian template renderer API to render the form.   In Eclipse, open the `MyServlet.java` class and do the following:

1.  Add an `TemplateRenderer` to the import section. 

    ``` java
    import com.atlassian.templaterenderer.TemplateRenderer;
    ```

2.  Update the `MyServlet` class with the following code:

    ``` java
    public class MyServlet extends HttpServlet{
        private static final Logger log = LoggerFactory.getLogger(MyServlet.class);
        
        private final UserManager userManager;
        private final LoginUriProvider loginUriProvider;
        private final TemplateRenderer templateRenderer;
         
        public MyServlet(UserManager userManager, LoginUriProvider loginUriProvider, TemplateRenderer templateRenderer)
        {
            this.userManager = userManager;
            this.loginUriProvider = loginUriProvider;
            this.templateRenderer = templateRenderer;
        }
        @Override
        public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException
        {
            String username = userManager.getRemoteUsername(request);
            if (username == null || !userManager.isSystemAdmin(username))
                {
                      redirectToLogin(request, response);
                      return;
                }
             
            response.setContentType("text/html;charset=utf-8");
            templateRenderer.render("admin.vm", response.getWriter());
        }


        // redirectToLogin and getUri methods NOT DISPLAYED for brevity
    ```

    This code includes a new `renderer` field. Initialize that field in the `MyServlet` constructor.  The response has changed, now instead of returning an HTML output you use a Velocity template and write the contents of that template.

3.  Close and save the file.

### Test Your Changes

1.  Open a terminal window and navigate to the plugin root folder (where the `pom.xml` file is).
2.  Run the `atlas-run` command to start the JIRA instance, and install your plugin in it. 
3.  After atlas-run complete, open your browser and navigate to our servlet location:  
    <a href="http://localhost:2990/jira/plugins/servlet/myservlet" class="external-link">http://localhost:2990/refapp/plugins/servlet/myservlet</a>
4.  The `UserManager` code recognizes you haven't logged in yet. JIRA prompts you for a login.
5.  At the JIRA login screen, enter a username of `admin` and a password of `admin`.   
    JIRA displays your form.
6.  Enable live reload and leave JIRA running.  
    Live reload allows you to view changes to Velocity resources, Javascript and other non-compiled resources as you make them. 

## Step 7.  Improve the Form's Look and Feel

The form you added is very plain. Moreover, it appears in JIRA without all the "standard" look-n-feel of JIRA. By customizing the Velocity template you can add the look and feel users expect in a JIRA page.  There are a number of [standard page decorators](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Ensuring+Standard+Page+Decoration+in+your+Plugin+UI) available to all Atlassian plugins.

### Add the Atlassian Admin Decorator

A page decorator allows your form to appear in appear in an Atlassian application without the need for you to actually generate headers, footers, sidebars and so forth.

1.  Edit the admin.vm file.
2.  Add the `atl.admin` decorator to the page in the &lt;head&gt; element.  
    When you are done the `<head>` element appears as follows:

    ``` xml
    <head>
        <title>MyServlet Admin</title>
        <meta name="decorator" content="atl.admin">
    </head>
    ```

    This code decorates your page for you.

3.  Save the `admin.vm` file.
4.  Switch back to your browser running your servlet in JIRA.  
    At this point your page should have reloaded and should appear as follows:  
    <img src="/server/framework/atlassian-sdk/images/decorator.png" width="700" />   
    If for some reason you don't see this, try refreshing your page. 

###  Include Atlassian User Interface (AUI) Components

AUI is a set of reusable, cross-browser-tested components (markup, CSS, and Javavscript. In this step, you add the `WebResourceManager` to your plugin. It is this manager that gives your plugin access to the CSS, Javascript, and other resources that typically appear in `<script>` and `<link>` tags in standard HTML. By `requireResource` you include all the resources for the `web-resource` module plus all of its dependencies. 

The Velocity context created by the TemplateRenderer automatically gives your plugin access to the `WebResourceManager`  The Velocity context makes a  number of commonly useful available APIs available, like the `WebResourceManager`. We'll see another one that is included automatically below, when we get to internationalizing our template.

1.  Edit the adin.vm  file.
2.  Include the resource manager in the `<head>` element.  
    When you are done your template looks like the following:

    ``` xml
    <head>
        <title>MyServlet Admin</title>
        <meta name="decorator" content="atl.admin">
        $webResourceManager.requireResource("com.atlassian.auiplugin:ajs")
    </head>
    ```

3.  Add some class attributes to the existing form and its components:

    ``` xml
    <html>
      <head>
        <title>MyServlet Admin</title>
        <meta name="decorator" content="atl.admin">
        $webResourceManager.requireResource("com.atlassian.auiplugin:ajs")
      </head>
      <body>
        <form id="admin" class="aui">
            <div class="field-group">
                 <label for="name">Name:</label>
                 <input type="text" id="name" name="name" class="text">
            </div>
            <div class="field-group">
                 <label for="age">Age:</label>
                 <input type="text" id="age" name="age" class="text">
            </div>
            <div class="field-group">
                <input type="submit" value="Save" class="button">
            </div>
        </form>
      </body>
    </html>
    ```

    In an AUI page, the aui, field-group, text, and button classes  are defined for you.  There is no need to create your own .CSS file. You can see the <a href="/pages/createpage.action?spaceKey=AUI&amp;title=Forms" class="createlink">Forms</a> page for detailed information about forms in AUI.

4.  Save the `admin.vm` file.  
    At this point, live reload reflects your changes - a nicely aligned set of components!  
     <img src="/server/framework/atlassian-sdk/images/aui-classes.png" width="700" />  
      

### Add Support for Internationalization (i18n)

You'll find  add internationalization pretty easily, the code generator has already done a lot of work for you.  When you added a servlet module, the code generator assumed you would want to internationalize your plugin at some point.  So, the generator added the i18n resource to your `atlassian-plugin.xml` file and that resources references the `src/main/resources/com/atlassian/plugins/tutorial/refapp/adminUI.properties` file the generator also added.  

The adminUI.properties file has some values defined already, for example the `my-servlet.name` and the `my-servlet.description` property.

1.  Edit the `adminUI.properties` file.
2.  Add new properties that represent the labels in your forms.  
    The file should like this when you are done:

    ``` bash
    my-servlet.name=My Servlet
    my-servlet.description=The My Servlet Plugin
    adminUI.admin.label=My Servlet Admin 
    adminUI.admin.name.label=Name 
    adminUI.admin.age.label=Age 
    adminUI.admin.save.label=Save
    ```

3.  Replace the  the hard-coded text values in the `admin.vm` template with lookups for the internationalized text.  
    The file contents should look like the following:

    ``` xml
    <html>
      <head>
        <title>$i18n.getText("adminUI.admin.label")</title>
        <meta name="decorator" content="atl.admin" />
        $webResourceManager.requireResource("com.atlassian.auiplugin:ajs")
      </head>
      <body>
        <form id="admin" class="aui">
          <div class="field-group">
            <label for="name">$i18n.getText("adminUI.admin.name.label")</label>
            <input type="text" id="name" name="name" class="text">
          </div>
          <div class="field-group">
            <label for="age">$i18n.getText("adminUI.admin.age.label")</label>
            <input type="text" id="age" name="age" class="text">
          </div>
          <div class="field-group">
            <input type="submit" value="$i18n.getText("adminUI.admin.save.label")" class="button">
          </div>
        </form>
      </body>
    </html>
    ```

    `$i18n` is an instance of SAL's `I18nResolver` API.  The `TemplateRenderer` supplies the resolver just like the `WebResourceManager`. You used it to resolve your message keys to actual text.  Since these changes are in a properties file, they aren't picked up by live reload.

4.  Reload your plugin with FastDev to see your changes.

 Now, all that is left to do for full internationalization is to translate the values in the properties file. You won't do that in this tutorial.

## Step 8. Add Support through SAL and REST

Your form is pretty simple. It doesn't include any data and the servlet doesn't support POSTs for updates. To display data in the form and update the configuration, you'll use JavaScript to make AJAX requests to a REST resource.  To populate the form we will make a GET request to a resource that will return the configuration as JSON.

Before we can start writing our JavaScript in earnest there are a few things we need to do. We need to know the applications base URL for making our ajax requests. We also need to tweak our template a little bit so that it will include the JavaScript that we're writing in addition to the AUI stuff.

### Add Another SAL Module

To find out what the application base URL is, you'll use another SAL API, the `ApplicationProperties` interface. 

1.  Open a command window and go to the plugin root folder (where the `pom.xml` is located).
2.  Run `atlas-create-refapp-plugin-module`.
3.  Choose the option labeled `Component Import`.
4.  Follow the prompts to add the `ApplicationProperties`

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter the fully qualified path name</p></td>
    <td><p><code>com.atlassian.sal.api.ApplicationProperties</code></p></td>
    </tr>
    <tr class="even">
    <td><p>Module Key</p></td>
    <td><p>Press return to take the default <code>applicationProperties</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>Filter (not require)</p></td>
    <td><p>Press return to accept the default which is none.</p></td>
    </tr>
    </tbody>
    </table>

5.  Choose Y for **Add Another Plugin Module**.
6.  Choose the option labeled Template Context item
7.  Follow the prompts to add the item:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><strong>Prompt</strong></td>
    <td><strong>Response</strong></td>
    </tr>
    <tr class="even">
    <td><p><strong>Enter Plugin Module Name</strong></p></td>
    <td><p><code>Application Properties Context Item</code></p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Enter Context Key</strong></p></td>
    <td><p><code>applicationProperties</code></p></td>
    </tr>
    <tr class="even">
    <td><p>Enter Component-Ref Key (leave blank to specify class): </p></td>
    <td><p><code>applicationProperties</code></p></td>
    </tr>
    <tr class="odd">
    <td>Global Access? </td>
    <td>N</td>
    </tr>
    <tr class="even">
    <td>Show Advanced Setup?</td>
    <td>N</td>
    </tr>
    </tbody>
    </table>

8.  Choose Y for **Add Another Plugin Module**.
9.  Choose the option labeled **Web Resource**:
10. Follow the prompts to add the `item`:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><strong>Prompt</strong></td>
    <td><strong>Response</strong></td>
    </tr>
    <tr class="even">
    <td><p><strong>Enter Plugin Module Name</strong></p></td>
    <td><p><code>Resources</code></p></td>
    </tr>
    <tr class="odd">
    <td><p><strong>Enter Resource Name</strong></p></td>
    <td><p><code>admin.js</code></p></td>
    </tr>
    <tr class="even">
    <td><p><strong>Enter Resource Type</strong></p></td>
    <td><p><code>download</code></p></td>
    </tr>
    <tr class="odd">
    <td><strong>Enter Location (path to resource file)</strong></td>
    <td><code>admin.js</code></td>
    </tr>
    <tr class="even">
    <td><strong>Add Resource Parameter? </strong></td>
    <td>N</td>
    </tr>
    <tr class="odd">
    <td><strong>Add Resource </strong></td>
    <td>N</td>
    </tr>
    <tr class="even">
    <td><strong>Show Advanced Setup?</strong></td>
    <td>Y</td>
    </tr>
    <tr class="odd">
    <td><strong>Module Key [resources]: </strong></td>
    <td>Press enter.</td>
    </tr>
    <tr class="even">
    <td><strong>Module Description [The Resources Plugin]:</strong> </td>
    <td>Press enter.</td>
    </tr>
    <tr class="odd">
    <td><strong>i18n Name Key [resources.name]: </strong></td>
    <td>Press enter.</td>
    </tr>
    <tr class="even">
    <td><strong>i18n Description Key [resources.description]: </strong></td>
    <td>Press enter.</td>
    </tr>
    <tr class="odd">
    <td><strong>Add Dependency?</strong></td>
    <td>Y</td>
    </tr>
    <tr class="even">
    <td><strong>Enter Dependency</strong></td>
    <td><code>com.atlassian.auiplugin:ajs</code></td>
    </tr>
    <tr class="odd">
    <td><strong>Add Dependency? </strong></td>
    <td>N</td>
    </tr>
    <tr class="even">
    <td><strong>Add Web Resource Context?</strong> </td>
    <td>N</td>
    </tr>
    <tr class="odd">
    <td><strong>Add Web Resource Transformation? </strong></td>
    <td>N</td>
    </tr>
    <tr class="even">
    <td><strong>Add Conditions?</strong></td>
    <td>N</td>
    </tr>
    </tbody>
    </table>

11. Choose N for **Add Another Plugin Module**.  
    The generator updates your project. 
12. At the root of your project directory, run the `atlas-mvn eclipse:eclipse` command. 

### What the Generator Added

The generated added a number lines to your `atlassian-plugin.xml` file:

``` xml
<template-context-item name="Application Properties Context Item" i18n-name-key="application-properties-context-item.name" key="application-properties-context-item" context-key="applicationProperties" global="false" component-ref="applicationProperties">
    <description key="application-properties-context-item.description">The Application Properties Context Item Plugin</description>
  </template-context-item>
  <web-resource name="Resources" i18n-name-key="resources.name" key="resources">
    <description key="resources.description">The Resources Plugin</description>
    <resource name="admin.js" type="download" location="admin.js"/>
    <dependency>com.atlassian.auiplugin:ajs</dependency>
  </web-resource>
```

### Modify the Generated Code

1.  Return to Eclipse and **Refresh** your project.
2.  Edit the atlassin-plugin.xml descriptor

### Add a REST Module

To find out what the application base URL is, you'll use another SAL API, the `ApplicationProperties` interface. 

1.  Open a command window and go to the plugin root folder (where the `pom.xml` is located).
2.  Run `atlas-create-refapp-plugin-module`.
3.  Choose the option labeled REST Plugin Module
4.  Follow the prompts to add the following:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter New Classname</p></td>
    <td><p><code>ConfigResource</code></p></td>
    </tr>
    <tr class="even">
    <td><p>Enter Package Name:</p></td>
    <td><p><code>com.atlassian.plugins.tutorial.refapp.adminui.rest</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>Enter REST path</p></td>
    <td><p><code>configresource</code></p></td>
    </tr>
    <tr class="even">
    <td>Enter Version</td>
    <td>1.0</td>
    </tr>
    <tr class="odd">
    <td>Show Advanced Setup</td>
    <td>N</td>
    </tr>
    </tbody>
    </table>

5.  Choose Y for **Add Another Plugin Module**.
6.  Choose the option labeled **Component Import** and follow the prompts to enter the following:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter the fully qualified path name</p></td>
    <td><p><code>com.atlassian.sal.api.pluginsettings.PluginSettingsFactory</code></p></td>
    </tr>
    <tr class="even">
    <td><p>Module Key</p></td>
    <td><p>Press return to take the default <code>pluginSettingsFactory</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>Filter (not require)</p></td>
    <td><p>Press return to accept the default which is none.</p></td>
    </tr>
    </tbody>
    </table>

7.  Choose Y for **Add Another Plugin Module**.

8.  Choose the option labeled **Component Import **and follow the prompts to enter the following:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>Enter the fully qualified path name</p></td>
    <td><p><code>com.atlassian.sal.api.transaction.TransactionTemplate</code></p></td>
    </tr>
    <tr class="even">
    <td><p>Module Key</p></td>
    <td><p>Press return to take the default transactionTemplate</p></td>
    </tr>
    <tr class="odd">
    <td><p>Filter (not require)</p></td>
    <td><p>Press return to accept the default which is none.</p></td>
    </tr>
    </tbody>
    </table>

9.  Choose N for **Add Another Plugin Module**.
10. Allow the plugin generation to complete.

#### What the Generator Added

The generated added a number lines to your atlassian-plugin.xml file:

``` xml
 <component-import key="pluginSettingsFactory" interface="com.atlassian.sal.api.pluginsettings.PluginSettingsFactory" />
<component-import key="transactionTemplate" interface="com.atlassian.sal.api.transaction.TransactionTemplate" />
  <rest name="Config Resource" i18n-name-key="config-resource.name" key="config-resource" path="/configresource" version="1.0">
    <description key="config-resource.description">The Config Resource Plugin</description>
  </rest>
```

### Step 9.  Write Some REST Code

The REST code builds a configuration resource your plugin will use to store configuration data.  

### Edit the Configuration Resource Class

1.  Open the `ConfigResource.java` in your project.
2.  Replace the existing content with the following code:  
     

    ``` java
    package com.atlassian.plugins.tutorial.refapp.adminui.rest;

    import javax.servlet.http.HttpServletRequest;
    import javax.ws.rs.Consumes;
    import javax.ws.rs.GET;
    import javax.ws.rs.PUT;
    import javax.ws.rs.Path;
    import javax.ws.rs.Produces;
    import javax.ws.rs.core.Context;
    import javax.ws.rs.core.MediaType;
    import javax.ws.rs.core.Response;
    import javax.ws.rs.core.Response.Status;
    import javax.xml.bind.annotation.XmlAccessType;
    import javax.xml.bind.annotation.XmlAccessorType;
    import javax.xml.bind.annotation.XmlElement;
    import javax.xml.bind.annotation.XmlRootElement;
    import com.atlassian.sal.api.pluginsettings.PluginSettings;
    import com.atlassian.sal.api.pluginsettings.PluginSettingsFactory;
    import com.atlassian.sal.api.transaction.TransactionCallback;
    import com.atlassian.sal.api.transaction.TransactionTemplate;
    import com.atlassian.sal.api.user.UserManager;
    import com.atlassian.plugins.rest.common.security.AnonymousAllowed;

    @Path("/config")
    public class ConfigResource
    {
        private final UserManager userManager;
        private final PluginSettingsFactory pluginSettingsFactory;
        private final TransactionTemplate transactionTemplate;
        
    public ConfigResource(UserManager userManager, PluginSettingsFactory pluginSettingsFactory, TransactionTemplate transactionTemplate)
        {
            this.userManager = userManager;
            this.pluginSettingsFactory = pluginSettingsFactory;
            this.transactionTemplate = transactionTemplate;
        }
    }
    ```

    This contains all the import statements we need, as well as a simple class constructor.  To populate the application web form, we issue a GET request to the resource that returns the data as JSON. JAXB serializes our configuration object for us, making life a bit easier.

3.  Add an inner class the encapsulates the configuration data:  
     

    ``` java
    @XmlRootElement
    @XmlAccessorType(XmlAccessType.FIELD)
    public static final class Config
    {
      @XmlElement private String name;
      @XmlElement private int age;
            
      public String getName()
      {
        return name;
      }
            
      public void setName(String name)
      {
        this.name = name;
      }
            
      public int getAge()
      {
        return age;
      }
            
      public void setAge(int age)
      {
        this.age = age;
      }
    }
    ```

    This inner class encapsulates a few properties, a `String` and an `int`. The `@XmlRootElement` and `@XmlElement` annotations are JAXB annotations. The `@XmlRootElement` annotation declares that instances of this type can be serialized to XML, and with a little magic in the REST module, to JSON as well. The `@XmlElement` annotations declare that the attributes should be treated as XML elements or JSON object properties.  If we were to serialize an instance of this class to XML, it would look like this:

    ``` xml
    <config>
      <name>Charlie</name>
      <age>5</age>
    </config>
    ```

    And in JSON, like this:

    ``` javascript
    {
      "name": "Charlie",
      "age": 5
    }
    ```

4.  Add a GET method, which returns a `Response` with an instance of the `Config` type we've just created as the entity.

    ``` java
    @GET
        @Produces(MediaType.APPLICATION_JSON)
        public Response get(@Context HttpServletRequest request)
        {
            String username = userManager.getRemoteUsername(request);
            if (username == null || !userManager.isSystemAdmin(username))
                {
                        return Response.status(Status.UNAUTHORIZED).build();
                }
            return Response.ok(transactionTemplate.execute(new TransactionCallback()
            {
                public Object doInTransaction()
                {
                    PluginSettings settings = pluginSettingsFactory.createGlobalSettings();
                    Config config = new Config();
                    config.setName((String) settings.get(Config.class.getName() + ".name"));
                    
                    String age = (String) settings.get(Config.class.getName() + ".age");
                    if (age != null)
                    {
                        config.setAge(Integer.parseInt(age));
                    }
                    return config;
                }
            })).build();
        }
    ```

    The GET method first performs the now familiar user check. We then construct a `Response` with an entity that is returned from a call to a funky <a href="http://docs.atlassian.com/sal-api/2.0.16-SNAPSHOT/com/atlassian/sal/api/transaction/TransactionTemplate.html#execute%28com.atlassian.sal.api.transaction.TransactionCallback%29" class="external-link"><code>transactionTemplate.execute</code></a> method, providing it with an instance of <a href="http://docs.atlassian.com/sal-api/2.0.16-SNAPSHOT/com/atlassian/sal/api/transaction/TransactionCallback.html" class="external-link"><code>TransactionCallback</code></a>. If you've used Spring's <a href="http://static.springsource.org/spring/docs/1.2.9/api/org/springframework/transaction/support/TransactionTemplate.html" class="external-link"><code>TransactionTemplate</code></a>, this should look familiar to you. For everyone spoiled by AOP, the summary is that we are accessing data that is coming from a database--well, it's not in Fisheye or Crucible, but work with me here!  

    Once we have a reference to a `PluginSettings` object, things are pretty easy. `PluginSettings` can be thought of as a persistent map. Just use `get` to retrieve data and `put` to add or update values.

    {{% note %}}

    Namespace your keys!

    Because this is **global** application configuration data, it is important that you do some kind of namespacing with your keys. Whether you use your plugin key, a class name or something else entirely is up to you. Just make sure it is unique enough that conflicts with other configuration data won't occur.

    {{% /note %}}

5.  Add a `PUT` method.  ``

    ``` java
        @PUT
        @Consumes(MediaType.APPLICATION_JSON)
        public Response put(final Config config, @Context HttpServletRequest request)
        {
            String username = userManager.getRemoteUsername(request);
            if (username == null || !userManager.isSystemAdmin(username))
                {
                   return Response.status(Status.UNAUTHORIZED).build();
                }
            transactionTemplate.execute(new TransactionCallback()
            {
                public Object doInTransaction()
                {
                    PluginSettings pluginSettings = pluginSettingsFactory.createGlobalSettings();
                    pluginSettings.put(Config.class.getName() + ".name", config.getName());
                    pluginSettings.put(Config.class.getName()  +".age", Integer.toString(config.getAge()));
                    return null;
                }
            });
            
            return Response.noContent().build();
        }
    ```

    The `@Consumes` annotation declares that we expect a request with a `application/json` body. We expect JSON in a form that matches the serialized form of the `Config` object we created earlier, so that the REST module can deserialize to a `Config` object, which it then passes to the `put` method.

    Next, we do the authentication and authorization check to make sure no one can modify the configuration except admin users. Then, we wrap our modifications in `TransactionCallback`, which we pass to the `transactionTemplate`, just like we did when we were retrieving the configuration. Since `PluginSettings` is just a persistent map, we just use the `put` method to put the new configuration values into it and we're done.

    Finally, we return `204 No Content`, which tells the client that the update succeeded and there's nothing left to be said.

6.  Close and save the `ConfigResource.java` file.

#### Why did we Use TransactionTemplate?

To ensure that reads and writes don't clash and give us inconsistent data, we need to protect ourselves any time we access `PluginSettings` data. The `TransactionTemplate` frees us from needing to know the application-specific transaction creation and usage semantics. If we didn't use the `TransactionTemplate`, we'd need code something like this:

``` java
Transaction tx = // go out and find or create transaction in application specific way
tx.start();
try
{
  // access plugin settings and do other work
  tx.commit();
}
catch (Exception e)
{
  tx.rollback();
}
```

But `TransactionTemplate` takes care of managing the transaction for us, by calling `TransactionCallback` to perform the real work. The return value of the `TransactionTemplate.execute` method is the return value of calling `TransactionCallback.doInTransaction`.

Inside our `TransactionCallback.doInTransaction` method, we use the `PluginSettingsFactory` to create a reference to the global, application-wide settings data. We need to use the global settings object because we're configuring a plugin. If we were storing data associated with a project (in JIRA, Bamboo, Fisheye or Crucible) or a space (in Confluence), we'd instead use the `PluginSettingsFactory.createSettingsForKey` method, where the `key` is the project or space the configuration data should be associated with.

## Step 9. Use Javascript to Wire REST and the Form

You have added a REST resource that is capable of getting and setting values in the database.  This resource is loaded along with your plugin into the container.  You use the JQuery implementation in AUI to populate your form. You'll make use of jQuery's <a href="http://docs.jquery.com/Ajax/jQuery.ajax" class="external-link"><code>ajax</code></a> method to communicate with your REST resources.

### Add JavaScript for GETting the configuration

We'll start out by making a GET request and setting the values of the input fields.

1.  Create a `src/main/resources/admin.js` file in your project.
2.  Edit the file and add the following function:

    ``` javascript
    AJS.toInit(function() {
        var baseUrl = AJS.$("meta[name='application-base-url']").attr("content");
         
      function populateForm() {
        AJS.$.ajax({
          url: baseUrl + "/rest/configresource/1.0/config",
          dataType: "json",
          success: function(config) {
            AJS.$("#name").attr("value", config.name);
            AJS.$("#age").attr("value", config.age);
          }
        });
      }
      
      populateForm();
      
    });
    ```

    This is pretty straight forward JavaScript if you are familiar with jQuery. `AJS.toInit` is equivalent to using `jQuery(function() {...})` or `jQuery(document).ready(function() {...})` to have some JavaScript executed when the document is ready. Our first task is to find the application base URL in the document that we added previously. Having done that, we can go on to query the server to find the current config. Once we have the config, we can populate our data.

3.  Add the following function to `admin.js`, after the `populateForm` function but before the call to `populateForm`.

    ``` javascript
      function updateConfig() {
          AJS.$.ajax({
            url: baseUrl + "/rest/configresource/1.0/config",
            type: "PUT",
            contentType: "application/json",
            data: '{ "name": "' + AJS.$("#name").attr("value") + '", "age": ' +  AJS.$("#age").attr("value") + ' }',
            processData: false
          });
        }
         
    ```

    This is the function we call to update the server configuration. It's very minimal; we haven't included error checking and we really should be escaping quotes and other special characters when creating our data, but that is left as an exercise for the reader. Now, we just need to hook that function up to our form.

4.  After the call to `populateForm()` in `admin.js` add:

    ``` java
         AJS.$("#admin").submit(function(e) {
              e.preventDefault();
              updateConfig();
          });
    ```

    Now, whenever the form is submitted, instead of the usual, default action of POSTing the form data, our `updateConfig()` method is called and our updated configuration is submitted as a `PUT` request to the configuration resource.

5.  Save and close the file.

### Access the Application Properties from Your Template

The `template-context-item`  allow you to put objects into the Velocity or other renderer's context so that you can use them in your templates. As an alternative, we could pass the `ApplicationProperties` component into our servlet, which is where we'll do the rendering from, and pass put it into the rendering context when we call the render method. Using the context item just makes that automatic, and if we were using the renderer in multiple places, makes the ApplicationProperties object available in all contexts without a bunch of duplicated code.

We use the `ApplicationProperties.getBaseUrl()` method to find the application base URL.

1.  Edit the `admin.vm` template.
2.  Replace the existing `$webResourceManager.requireResource` call with the following:

    ``` java
    $webResourceManager.requireResource("com.atlassian.plugins.tutorial.refapp.adminUI:resources")
    ```

3.  Add a new `<meta>` tag to the `<head>` element.

    ``` xml
    <meta name="application-base-url" content="$applicationProperties.getBaseUrl()">
    ```

    At this point the `admin.vm` file should look like the following:

    ``` xml
     <html>
      <head>
        <title>$i18n.getText("adminUI.admin.label")</title>
        <meta name="decorator" content="atl.admin" />
        $webResourceManager.requireResource("com.atlassian.plugins.tutorial.refapp.adminUI:resources")
        <meta name="application-base-url" content="$applicationProperties.getBaseUrl()">
      </head>
      <body>
        <form id="admin" class="aui">
          <div class="field-group">
            <label for="name">$i18n.getText("adminUI.admin.name.label")</label>
            <input type="text" id="name" name="name" class="text">
          </div>
          <div class="field-group">
            <label for="age">$i18n.getText("adminUI.admin.age.label")</label>
            <input type="text" id="age" name="age" class="text">
          </div>
          <div class="field-group">
            <input type="submit" value="$i18n.getText("adminUI.admin.save.label")" class="button">
          </div>
        </form>
      </body>
    </html>
    ```

4.  Save and close the file.

### Build, install and run the plugin

1.  Open a terminal window and navigate to the plugin root folder (where the `pom.xml` file is).
2.  Enter` atlas-run` to build your plugin.

3.  Open your browser and navigate to the local JIRA instance started by `atlas-run`.  
    For example, the default address is <a href="http://localhost:2990/jira" class="external-link">http://localhost:2990/refapp</a> for JIRA. See [Plugin SDK Supported Applications and Default Ports](/server/framework/atlassian-sdk/-plugin-sdk-supported-applications-and-default-ports-2818466.html) for other applications.
4.  At the JIRA login screen, enter a username of `admin` and a password of `admin`. 
5.  Navigate to your servlet location:  
    <a href="http://localhost:2990/jira/plugins/servlet/myservlet" class="external-link">http://localhost:2990/refapp/plugins/servlet/myservlet</a>   
    You should see something similar to the following:












