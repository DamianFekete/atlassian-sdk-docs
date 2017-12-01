---
aliases:
- /server/framework/atlassian-sdk/creating-an-admin-configuration-form-2818695.html
- /server/framework/atlassian-sdk/creating-an-admin-configuration-form-2818695.md
category: devguide
confluence_id: 2818695
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818695
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818695
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/creating-an-admin-configuration-form
new_url: /server/framework/atlassian-sdk/creating-an-admin-configuration-form
platform: server
product: atlassian-sdk
subcategory: learning
title: Creating an admin configuration form
---
# Creating an admin configuration form

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Applicable:</p></td>
<td><p>This tutorial describes how to create plugins that work across Atlassian products. It does so by creating a plugin that works with RefApp 3.3.6.</p></td>
</tr>
<tr class="even">
<td><p>Level of experience:</p></td>
<td><p>This is an advanced tutorial. You should have completed at least one intermediate tutorial before working through this tutorial. See the <a href="/server/framework/atlassian-sdk/tutorials">list of tutorials in DAC</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Time estimate:</p></td>
<td><p>It should take you approximately 2 hours to complete this tutorial.</p></td>
</tr>
</tbody>
</table>

## Overview of the tutorial

This tutorial shows how to create a plugin that generates a simple web form that can appear in the UI of any Atlassian product.

To test our work, we'll use the [Atlassian Reference Application](/server/framework/atlassian-sdk/about-the-atlassian-refapp) (or RefApp for short). The RefApp is an Atlassian application that encapsulates the common base features of Atlassian products. It's useful for testing cross-application plugins, such as the one we develop in this tutorial.

Along the way, this tutorial introduces these concepts:

-   [Shared Access Layer (SAL) API](/server/framework/atlassian-sdk/about-sal-development) is a programming interface that exposes many common services to plugins, such as persistence and user authorization. It does so in a way that works with any Atlassian application.
-   <a href="https://studio.atlassian.com/wiki/display/ATR/Home" class="external-link">Atlassian Template Renderer (ATR)</a> is a plugin that enables other plugins to render templates, typically Velocity templates.
-   <a href="https://studio.atlassian.com/browse/AJS" class="external-link">Atlassian User Interface (AUI)</a> gives user interface elements the Atlassian look-and-feel. 
-   [REST module](/server/framework/atlassian-sdk/rest-plugin-module) forms the communication mechanism between the browser and the server.

Your completed plugin will consist of:

-   Java classes encapsulating the plugin logic.
-   Resources for display of the plugin user interface (UI).
-   A plugin descriptor (XML file) to enable the plugin module in the Atlassian application.

### Prerequisite knowledge

To complete this tutorial, you need to know the following: 

-   The basics of Java development: classes, interfaces, methods, how to use the compiler, and so on.
-   How to create an Atlassian plugin project using the [Atlassian Plugin SDK](https://developer.atlassian.com/display/DOCS/Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project). 

### Plugin source

We encourage you to work through this tutorial. If you want to skip ahead or check your work when you have finished, you can find the plugin source code on Atlassian Bitbucket. Bitbucket serves a public Git repository containing the tutorial's code. To clone the repository, issue the following command:

``` bash
git clone git@bitbucket.org:serverecosystem/xproduct-admin-ui-plugin.git
```

Alternatively, you can download the source using the **get source** option here: <a href="https://bitbucket.org/serverecosystem/xproduct-admin-ui-plugin" class="uri external-link">https://bitbucket.org/serverecosystem/xproduct-admin-ui-plugin</a>.

{{% note %}}

About these Instructions

You can use any supported combination of OS and IDE to construct this plugin. These instructions were written using Ubuntu 10.04. If you are using another OS or an IDE, you should use the equivalent operations for your specific environment.

{{% /note %}}

## Step 1. Create the plugin project

In this step, you use an `atlas-` command to generate stub code for your plugin. The `atlas-` commands are part of the Atlassian Plugin SDK, and automate much of the work of plugin development for you.

1.  Open a terminal and navigate to the directory where you want to create your tutorial project directory.
2.  Enter the following command:

    ``` bash
    atlas-create-refapp-plugin
    ```

3.  When prompted, enter the following information to identify your plugin:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>group-id</p></td>
    <td><p><code>com.atlassian.plugins.tutorial</code></p></td>
    </tr>
    <tr class="even">
    <td><p>artifact-id</p></td>
    <td><p><code>xproduct-admin-ui-plugin</code></p></td>
    </tr>
    <tr class="odd">
    <td><p>version</p></td>
    <td><p><code>1.0</code></p></td>
    </tr>
    <tr class="even">
    <td><p>package</p></td>
    <td><p><code>com.atlassian.plugins.tutorial</code></p></td>
    </tr>
    </tbody>
    </table>

4.  Confirm your entries when prompted.

The command creates a directory named `xproduct-admin-ui-plugin`, which contains all your initial project files. This tutorial refers to this directory as your project root. Unless otherwise indicated, all directory paths are relative to the project root.

## Step 2. Review and tweak the generated project

It's a good idea to familiarise yourself with the generated project files. In this section, we'll check a version value and tweak the generated files. We'll also start up the RefApp and have a look around.

### Delete the tests folder

Since we won't be writing any tests, to prevent any interference with the build process, delete the `src/test` folder.

### Add plugin metadata to the POM

The POM (Project Object Model definition file) is located at the root of your project and declares the project dependencies and other information.

Add some metadata about your plugin and your company or organisation.

1.  Edit the `pom.xml` file in the root folder of your plugin.
2.  Add your company or organisation name and your website to the `organization` element:

    ``` xml
    <organization>
      <name>Example Company</name>
      <url>http://www.example.com/</url>
    </organization>
    ```

3.  Update the `description` element:

    ``` xml
    <description>Provides a custom field to store money amounts.</description>
    ```

4.  Save the file.

### Verify your host application version

As mentioned in the overview, the host application for the plugin you are creating in this tutorial is the RefApp. When you generated the stub files, a default version specification was included in your `pom.xml` file for the RefApp. Take a moment and examine the dependency:

1.  If it's not already open, open the `pom.xml` file.
2.  Scroll to the bottom of the file.
3.  Find the `properties` element.  
    This section lists the version of the RefApp and also the version of the `atlas-` commands you are running.
4.  Verify that the RefApp version is the one you want. If you are not sure which version you need, check the version table at the top of this tutorial.
5.  Save and close the `pom.xml` file.

### Review the generated plugin descriptor

Your stub code contains a plugin descriptor file `atlassian-plugin.xml`. This is an XML file that identifies the plugin to the host application (HOSTAPP) and defines the required plugin functionality. In a text editor or IDE (integrated development environment, such as Eclipse or IDEA) open the descriptor file located in your project under `src/main/resources`. It should look like this:

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
    <resource type="i18n" name="i18n" location="xproduct-admin-ui-plugin"/>
    
    <!-- add our web resources -->
    <web-resource key="xproduct-admin-ui-plugin-resources" name="xproduct-admin-ui-plugin Web Resources">
        <dependency>com.atlassian.auiplugin:ajs</dependency>
        
        <resource type="download" name="xproduct-admin-ui-plugin.css" location="/css/xproduct-admin-ui-plugin.css"/>
        <resource type="download" name="xproduct-admin-ui-plugin.js" location="/js/xproduct-admin-ui-plugin.js"/>
        <resource type="download" name="images/" location="/images"/>

        <context>xproduct-admin-ui-plugin</context>
    </web-resource>
    
</atlassian-plugin>
```

### Start and view the RefApp

Although you haven't modified the generated code yet, try starting the RefApp application now. It's always a good idea to check your work periodically by making sure the application compiles and starts up.

1.  At the command line, change directory to your plugin project root (the `xproduct-admin-ui-plugin` directory created earlier).

2.  Enter the `atlas-run` command.

This triggers the RefApp startup process. When finished, you should see output similar to:

``` text
...
[INFO] [talledLocalContainer] Tomcat 6.x started on port [5990]
[INFO] refapp started successfully in 42s at http://atlas-laptop:5990/refapp
[INFO] Type Ctrl-D to shutdown gracefully
[INFO] Type Ctrl-C to exit 
```

Notice the URL for the RefApp: you can substitute your hostname for `atlas-laptop`, or simply use the URL:

<a href="http://localhost:5990/refapp/" class="uri external-link">http://localhost:5990/refapp/</a>

Open the RefApp in a browser and have a look around, although there isn't much to see yet.  

## Step 3. Add the web form servlet

Let's add a servlet to the RefApp that presents a webform in the RefApp UI. The form won't do anything yet, but it gives us something to add to as we go.

### Create the servlet

Let's add a servlet to the project.

1.  Change directories to  
    `src/main/java/com/atlassian/plugins/tutorial/`
2.  Make a new directory at that location, named `xproductadminui`.
3.  In the new directory, create a new file named `AdminServlet.java` with the following contents:

    ``` java
    package com.atlassian.plugins.tutorial.xproductadminui;

    import java.io.IOException;

    import javax.servlet.ServletException;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;

    public class AdminServlet extends HttpServlet
    {
      @Override
      public void doGet(HttpServletRequest request, HttpServletResponse response) throws IOException, ServletException
      {
      }
    }
    ```

4.  Save and close the file.

Optionally, run the application again (using the `atlas-run` command from the project root), just to make sure everything compiles and starts up okay.

### Add a credential check

Our web application first checks whether the user is logged in. If not, it redirects the user to the login page. We use the SAL User Manager feature to make sure that the current user is an administrator. This dependency has already been added to pom.xml, look for the following:

``` xml
<dependency>
  <groupId>com.atlassian.sal</groupId>
  <artifactId>sal-api</artifactId>
  <scope>provided</scope>
</dependency>
```

With SAL added as a build dependency, we can import SAL and use it in our servlet.

1.  Navigate to the directory:  
    `src/main/java/com/atlassian/plugins/tutorial/xproductadminui/`
2.  Open `AdminServlet.java` for editing. 
3.  Add the following import statements alongside the existing statements:

    ``` java
    import java.net.URI;
    import com.atlassian.sal.api.auth.LoginUriProvider;
    import com.atlassian.sal.api.user.UserManager;
    ```

4.  Replace the entire `AdminServlet` class declaration with the following:

    ``` java
    public class AdminServlet extends HttpServlet
    {
      private final UserManager userManager;
      private final LoginUriProvider loginUriProvider;

      public AdminServlet(UserManager userManager, LoginUriProvider loginUriProvider)
      {
        this.userManager = userManager;
        this.loginUriProvider = loginUriProvider;
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
      }
    }
    ```

In our `doGet` method, we check whether the user is logged in (that is, username is not `null`) and that the user is an administrator, thanks to the `UserManager` class. If either are false, we redirect the user to the application login page by calling the `redirectToLogin` method, which we haven't implemented yet. 

Add the following two methods, `redirectToLogin` and `getUri` methods to the `AdminServlet` class immediately after `doGet`:

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

Notice that the `getUri` method returns the current URI to the `LoginUriProvider` so that the user is redirected back to our admin UI when they are properly authenticated.

### Render the form with the Atlassian Template Renderer

Now let's get to rendering! As mentioned in the [Overview](#overview), we can use the Atlassian Template Renderer for that. Once again, before we can write the code, we need to tell Maven that we'll be using it.

Find the `dependencies` section in the `pom.xml` file and add the following `dependency`

``` xml
<dependency>
  <groupId>com.atlassian.templaterenderer</groupId>
  <artifactId>atlassian-template-renderer-api</artifactId>
  <scope>provided</scope>
</dependency>
```

In `AdminServlet.java`, add the following import statement to the existing ones:

``` java
import com.atlassian.templaterenderer.TemplateRenderer;
```

  
We need to instantiate the renderer object in the constructor and call it in the `doGet` method. Add the `renderer` variable declaration to the existing ones and replace the entire `AdminServlet` constructor and `doGet` method with the following:

``` java
private final TemplateRenderer renderer;

public AdminServlet(UserManager userManager, LoginUriProvider loginUriProvider, TemplateRenderer renderer)
{
  this.userManager = userManager;
  this.loginUriProvider = loginUriProvider;
  this.renderer = renderer;
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
  renderer.render("admin.vm", response.getWriter());
}
```

We've added a dependency on a `TemplateRenderer` to our constructor. This is the renderer we use to display our form. In the `doGet` method, after applying our authorization check, we set the response content type to `text/html` and then make a call to the `templateRenderer`, telling it to render our `admin.vm` template. We will create the template shortly.

### Modify the Atlassian plugin descriptor

Before we go any further, let's tell the plugin system about our servlet.

Open `atlassian-plugin.xml` for editing and add the following servlet declaration statements. You can add it anywhere within the `atlassian-plugin` element, such as after the existing servlet declaration.

``` xml
<servlet key="admin-servlet" class="com.atlassian.plugins.tutorial.xproductadminui.AdminServlet">
  <url-pattern>/xproduct/admin</url-pattern>
</servlet>
```

### Add the necessary Annotations

In order to get Spring scanner to import components for us, we need to annotate a few things.

First we need to add the following annotation imports to `AdminServlet.java`:

``` java
import javax.inject.Inject;
import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
```

Add a @Scanned annotation to the class definition to tell the scanner to scan our class:

``` java
@Scanned
public class AdminServlet extends HttpServlet
```

Add `@ComponentImport` annotations to the members of the `AdminServlet` class, the result should look like:

``` java
@ComponentImport
private final UserManager userManager;
@ComponentImport
private final LoginUriProvider loginUriProvider;
@ComponentImport
private final TemplateRenderer renderer;
```

Finally add an `@Inject` annotation to the constructor:

``` java
@Inject
public AdminServlet(UserManager userManager, LoginUriProvider loginUriProvider, TemplateRenderer renderer)
```

### Create the Velocity template

A Velocity template determines the HTML presentation produced by our application.

Create a Velocity template file named `admin.vm` in the `src/main/resources` directory. To start, we keep it simple. Add this to the file:

``` xml
<html>
  <head>
    <title>XProduct Admin</title>
  </head>
  <body>
    <form id="admin">
      <div>
        <label for="name">Name</label>
        <input type="text" id="name" name="name">
      </div>
      <div>
        <label for="time">Time</label>
        <input type="text" id="time" name="time">
      </div>
      <div>
        <input type="submit" value="Save">
      </div>
    </form>
  </body>
</html>
```

With that done, let's test the login redirect logic we've added. Start the RefApp by running the `atlas-run` command again and go to:

<a href="http://localhost:5990/refapp/plugins/servlet/xproduct/admin" class="uri external-link">http://localhost:5990/refapp/plugins/servlet/xproduct/admin</a>

A login prompt should appear. Log in using the credentials admin/admin. Once logged in, you should see the HTML in `admin.vm` rendered on the webpage.

## Step 4. Edit the Velocity template

The template we have from the previous step is a start, but it's also, well, ugly. It is missing application template features, such as the Atlassian logo and menus. Let's fix that.

### Add some decoration

To style the page, open `admin.vm` for editing again and add this `meta` tag. Add it to the `head` element, after the existing `title` element.

``` xml
<meta name="decorator" content="atl.admin">
```

This tells the application that it needs to use the admin decorator around the body of this page.

Now the page looks like something the application would actually display.  
Now we're getting somewhere. But the form itself still doesn't look so good. AUI to the rescue!

### Style it

First we need to include AUI in our header. Add the following line after the meta tag in the `admin.vm` file.

``` java
$webResourceManager.requireResource("com.atlassian.auiplugin:ajs")
```

What is `$webResourceManager` and where does it come from? It's the web resource manager from the plugin system used to manage CSS, JavaScript and other resources that are usually linked at the top of pages using `<script>`. Calling `requireResource` will include all the resources for the `web-resource` module along with its dependencies.

But where did the `WebResourceManager` come from? It was automatically added to the Velocity context by the `TemplateRenderer`. It makes a few things that are commonly useful available, like the `WebResourceManager`. We'll see another one that is included automatically below, when we get to internationalizing our template.

Next, we improve the appearance of the form by adding class attributes.

``` xml
<form id="admin" class="aui">
  <div class="field-group">
    <label for="name">Name:</label>
    <input type="text" id="name" name="name" class="text">
   </div>
   <div class="field-group">
     <label for="time">Time:</label>
     <input type="text" id="time" name="time" class="text">
   </div>
   <div class="field-group">
     <input type="submit" value="Save" class="button">
   </div>
</form>
```

The changes were small. We added `class="aui"` to the `form` element, `class="text"` to each of our text input boxes, `class="button"` to our submit button, and `class="field-group"` to our div tags. And for such little work we get a nice looking form in any Atlassian application, and consistent with the application look and feel!

### I18n it

We can also add internationalization support to our user interface pretty easily. Notice that the following line in `atlassian-plugin.xml` specifies the i18n resource:

``` xml
<resource type="i18n" name="i18n" location="xproduct-admin-ui-plugin"/>
```

In the file `src/main/resources/xproduct-admin-ui-plugin.properties`, add this text:

``` java
xproduct.admin.label=XProduct Admin
xproduct.admin.name.label=Name:
xproduct.admin.time.label=Time:
xproduct.admin.save.label=Save
```

These properties define the labels that will appear in our UI. For example, the label for the `time` field is 'Time'.

Next, replace the hard-coded text values in the `admin.vm` template with lookups for internationalized text.

``` xml
<html>
  <head>
    <title>$i18n.getText("xproduct.admin.label")</title>
    <meta name="decorator" content="atl.admin" />
    $webResourceManager.requireResource("com.atlassian.auiplugin:ajs")
  </head>
  <body>
    <form id="admin" class="aui">
      <div class="field-group">
        <label for="name">$i18n.getText("xproduct.admin.name.label")</label>
        <input type="text" id="name" name="name" class="text">
      </div>
      <div class="field-group">
        <label for="time">$i18n.getText("xproduct.admin.time.label")</label>
        <input type="text" id="time" name="time" class="text">
      </div>
      <div class="field-group">
        <input type="submit" value="$i18n.getText("xproduct.admin.save.label")" class="button">
      </div>
    </form>
  </body>
</html>
```

`$i18n` is an instance of SAL's <a href="http://docs.atlassian.com/sal-api/2.0.16-SNAPSHOT/com/atlassian/sal/api/message/I18nResolver.html" class="external-link">I18nResolver</a>, which comes automatically with `TemplateRenderer`, just like the `WebResourceManager`. We use it to resolve our message keys to actual text. Feel free to experiment with the labels in the properties file.

If we refresh the page right now, the i18n changes will not be reflected correctly. To load the changes we've made, we need to reload the plug-in. Instead of taking down the refapp instance and restarting it, we can take advantage of QuickReload: run `atlas-mvn package` in the project root to reload the plug-in, and you should see that i18n is working as intended.

To localize an application for an actual deployment, the only thing left to do would be to get the properties file translated.

Now we have our basic UI. It's time to make it do something!

## Step 5. Make the JavaScript and REST happen

Our form is pretty simple. You can't post anything with it yet. To be able to post and display data in the form, we'll use JavaScript to make AJAX requests to a REST resource. The resource returns the data as JSON, which our form displays.

### Add our JavaScript to the template

The recommended way to add JavaScript to pages is to create a `web-resource` module in your `atlassian-plugin.xml` file. Using this method, you can also specify dependencies on other `web-resource` modules, like AUI.

This has already been done for you, notice the line in `atlassian-plugin.xml`:

``` xml
<resource type="download" name="xproduct-admin-ui-plugin.js" location="/js/xproduct-admin-ui-plugin.js"/>
```

Now edit the `admin.vm` template. Replace the existing `$webResourceManager.requireResource` call with:

``` java
$webResourceManager.requireResource("com.atlassian.plugins.tutorial.xproduct-admin-ui-plugin:resources")
```

Now we can write some JavaScript!

### JavaScript for GETting the configuration

Populating our form is pretty easy. AUI supports jQuery, which we use to communicate with our REST resources. Start out by making a GET request to set the values of the input fields.

In the file located at `src/main/resources/js/xproduct-admin-ui-plugin.js`, add the following JavaScript code to the file:

``` javascript
(function ($) { // this closure helps us keep our variables to ourselves.
// This pattern is known as an "iife" - immediately invoked function expression
 
    // form the URL
    var url = AJS.contextPath() + "/rest/xproduct-admin/1.0/";
 
    // wait for the DOM (i.e., document "skeleton") to load. This likely isn't necessary for the current case,
    // but may be helpful for AJAX that provides secondary content.
    $(document).ready(function() {
        // request the config information from the server
        $.ajax({
            url: url,
            dataType: "json"
        }).done(function(config) { // when the configuration is returned...
            // ...populate the form.
            $("#name").val(config.name);
            $("#time").val(config.time);
        });
    });

})(AJS.$ || jQuery);
```

This JavaScript creates a URL by combining the root context path of our application from `AJS.contextPath()` (which might be something like "/jira", "/stash", or even an empty string, "") with the hard-coded relative URL of our REST resource. Then it queries the server to find the current config. Once done, it populates the name and time elements with our data.

Next we write the REST resource that serves the data.

### Serve the configuration from a REST resource

The JavaScript we've added makes a request to a configuration resource for populating our form. Since it doesn't exist yet, we need to create this resource. But before we write the code for that, we need to add a few more dependencies in Maven. The [Atlassian REST module](/server/framework/atlassian-sdk/rest-plugin-module) uses <a href="http://jersey.dev.java.net/" class="external-link">Jersey</a>, an implementation of the <a href="https://jsr311.dev.java.net/" class="external-link">JAX-RS</a> API. We'll add a dependency for this JAX-RS API. We'll also use JAXB to serialize our configuration object for us, to avoid having to manually construct JSON, so we need to add a dependency for that as well.

Open the `pom.xml` file and add these `dependency` elements to the `dependencies` section:

``` xml
<dependency>
  <groupId>javax.xml.bind</groupId>
  <artifactId>jaxb-api</artifactId>
  <version>2.1</version>
  <scope>provided</scope>
</dependency>
```

Now we can write our REST resource class.

### Retrieve the configuration with `GET`

Again, start with a simple class and build it up from there.

Create a new file named `ConfigResource.java` in the directory:

`src/main/java/com/atlassian/plugins/tutorial/xproductadminui/`

Add the following:

``` java
package com.atlassian.plugins.tutorial.xproductadminui;

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

import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
import javax.inject.Inject;

import com.atlassian.sal.api.pluginsettings.PluginSettings;
import com.atlassian.sal.api.pluginsettings.PluginSettingsFactory;
import com.atlassian.sal.api.transaction.TransactionCallback;
import com.atlassian.sal.api.transaction.TransactionTemplate;
import com.atlassian.sal.api.user.UserManager;

@Path("/")
@Scanned
public class ConfigResource
{
    @ComponentImport
    private final UserManager userManager;
    @ComponentImport
    private final PluginSettingsFactory pluginSettingsFactory;
    @ComponentImport
    private final TransactionTemplate transactionTemplate;

    @Inject
    public ConfigResource(UserManager userManager, PluginSettingsFactory pluginSettingsFactory,
                          TransactionTemplate transactionTemplate)
    {
        this.userManager = userManager;
        this.pluginSettingsFactory = pluginSettingsFactory;
        this.transactionTemplate = transactionTemplate;
    }
}
```

This contains all the import statements we need, as well as a simple class constructor.

To populate the application web form, we issue a GET request to the resource that returns the data as JSON. JAXB serializes our configuration object for us, making life a bit easier.

First, add an inner class that encapsulates our configuration data.

``` java
@XmlRootElement
@XmlAccessorType(XmlAccessType.FIELD)
public static final class Config
{
  @XmlElement private String name;
  @XmlElement private int time;
        
  public String getName()
  {
    return name;
  }
        
  public void setName(String name)
  {
    this.name = name;
  }
        
  public int getTime()
  {
    return time;
  }
        
  public void setTime(int time)
  {
    this.time = time;
  }
}
```

Here we've created a class that will encapsulate a few properties, a `String` and an `int`. The `@XmlRootElement` and `@XmlElement` annotations are JAXB annotations. The `@XmlRootElement` annotation declares that instances of this type can be serialized to XML, and with a little magic in the REST module, to JSON as well. The `@XmlElement` annotations declare that the attributes should be treated as XML elements or JSON object properties.

If we were to serialize an instance of this class to XML, it would look like this:

``` xml
<config>
  <name>Charlie</name>
  <time>5</time>
</config>
```

And in JSON, like this:

``` javascript
{
  "name": "Charlie",
  "time": 5
}
```

Now let's implement the GET method, which returns a `Response` with an instance of the `Config` type we've just created as the entity.

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
                
      String time = (String) settings.get(Config.class.getName() + ".time");
      if (time != null)
      {
        config.setTime(Integer.parseInt(time));
      }
      return config;
    }
  })).build();
}
```

This method first performs our now familiar user check.

We then construct a Response with an entity that is returned from a call to a funky <a href="http://docs.atlassian.com/sal-api/2.0.16-SNAPSHOT/com/atlassian/sal/api/transaction/TransactionTemplate.html#execute%28com.atlassian.sal.api.transaction.TransactionCallback%29" class="external-link">transactionTemplate.execute</a> method, providing it with an instance of <a href="http://docs.atlassian.com/sal-api/2.0.16-SNAPSHOT/com/atlassian/sal/api/transaction/TransactionCallback.html" class="external-link">TransactionCallback</a>. If you've used Spring's <a href="http://static.springsource.org/spring/docs/1.2.9/api/org/springframework/transaction/support/TransactionTemplate.html" class="external-link">TransactionTemplate</a>, this should look familiar to you. For everyone spoiled by AOP, the summary is that we are accessing data that is coming from a database--well, it's not in Fisheye or Crucible, but work with me here!

To ensure that reads and writes don't clash and give us inconsistent data, we need to protect ourselves any time we access `PluginSettings` data. The `TransactionTemplate` frees us from needing to know the application-specific transaction creation and usage semantics. If we didn't use the `TransactionTemplate`, we'd need code something like this:

``` javascript
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

But `TransactionTemplate` takes care of managing the transaction for us, by calling `TransactionCallback` to perform the real work. The return value of the `TransactionTemplate.execute` method is the return value of calling `TransactionCallback.doInTransaction`.

Inside our `TransactionCallback.doInTransaction` method, we use the `PluginSettingsFactory` to create a reference to the global, application-wide settings data. We need to use the global settings object because we're configuring a plugin. If we were storing data associated with a project (in JIRA, Bamboo, Fisheye or Crucible) or a space (in Confluence), we'd instead use the `PluginSettingsFactory.createSettingsForKey` method, where the `key` is the project or space the configuration data should be associated with.

Once we have a reference to a `PluginSettings` object, things are pretty easy. `PluginSettings` can be thought of as a persistent map. Just use `get` to retrieve data and `put` to add or update values.

{{% note %}}

Namespace your keys!

Because this is **global** application configuration data, it is important that you do some kind of namespacing with your keys. Whether you use your plugin key, a class name or something else entirely is up to you. Just make sure it is unique enough that conflicts with other configuration data won't occur.

{{% /note %}}

## Step 6. Updating the configuration

Now that our form can be populated with our current configuration, we want to allow the admin user to update the configuration.

### JavaScript for PUTting an updated configuration

Add the following function to the end of the file `xproduct-admin-ui-plugin.js.`

``` javascript
function updateConfig() {
  AJS.$.ajax({
    url: baseUrl + "/rest/xproduct-admin/1.0/",
    type: "PUT",
    contentType: "application/json",
    data: '{ "name": "' + AJS.$("#name").attr("value") + '", "time": ' +  AJS.$("#time").attr("value") + ' }',
    processData: false
  });
}
```

This is the function we call to update the server configuration. It's very minimal; we haven't included error checking and we really should be escaping quotes and other special characters when creating our data, but that is left as an exercise for the reader.

Now, we just need to hook that function up to our form. Within the block with the comment that says "...populate the form", add the following to the end of that block:

``` javascript
    AJS.$("#admin").submit(function(e) {
        e.preventDefault();
        updateConfig();
    });
```

Now, whenever the form is submitted, instead of the usual, default action of POSTing the form data, our `updateConfig()` method is called and our updated configuration is submitted as a `PUT` request to the configuration resource.

### Update the configuration with `PUT`

To handle the `PUT` requests from the client, add this method to the `ConfigResource.java` file you created earlier: ``

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
      pluginSettings.put(Config.class.getName()  +".time", Integer.toString(config.getTime()));
      return null;
    }
  });
  return Response.noContent().build();
}
```

The `@Consumes` annotation declares that we expect a request with a `application/json` body. We expect JSON in a form that matches the serialized form of the `Config` object we created earlier, so that the REST module can deserialize to a `Config` object, which it then passes to the `put` method.

Next, we do the authentication and authorization check to make sure no one can modify the configuration except admin users. Then, we wrap our modifications in `TransactionCallback`, which we pass to the `transactionTemplate`, just like we did when we were retrieving the configuration. Since `PluginSettings` is just a persistent map, we just use the `put` method to put the new configuration values into it and we're done.

Finally, we return `204 No Content`, which tells the client that the update succeeded and there's nothing left to be said.

### Wire things together

Finally, we need to add a few items to the `atlassian-plugin.xml` file. We need to add the `rest` module, so that the plugin system knows about the REST resource and where to find it.

Add the following lines to `atlassian-plugin.xml`:

``` xml
<rest key="rest" path="/xproduct-admin" version="1.0">
  <description>Provides REST resources for the admin UI.</description>
</rest>
```

## Step 7. Add menu items

The last thing we need to do is to make it easy for the admin user to find our configuration administration UI. We'll create links in the administration menu by adding [Web item](/server/framework/atlassian-sdk/web-item-plugin-module) elements to `atlassian-plugin.xml`. Unfortunately, not every Atlassian product uses the same layout for menus, so we need to add a link entry for each product.

Fortunately, the `application` attribute will come to our rescue (mostly)!

To add a link in the 'Global Settings' menu in JIRA's administration area, add the following `web-item` element.

``` xml
<web-item key="jira-menu-item" name="XProduct Admin" section="system.admin/globalsettings" weight="10" application="jira">
  <description>Link to xproduct-admin page.</description> 
  <label key="xproduct.admin.label" /> 
  <link linkId="xproduct-admin-link">/plugins/servlet/xproduct/admin</link> 
</web-item> 
```

To add a link in the 'Plugins' menu in Bamboo's administration area, add the following `web-item` element.

``` xml
<web-item key="bamboo-menu-item" name="XProduct Admin" section="system.admin/plugins" weight="10" application="bamboo"> 
  <description>Link to xproduct-admin page.</description> 
  <label key="XProduct Admin" /> 
  <link linkId="xproduct-admin-link">/plugins/servlet/xproduct/admin</link> 
</web-item> 
```

Looking carefully, you'll notice that the `label` `key` attribute isn't really a key. This is because Bamboo doesn't do any internationalization yet, so the value of the `key` attribute will be the text that is displayed.

To add a link in the 'Configuration' menu in Confluence's administration area, add the following `web-item` element.

``` xml
<web-item key="conf-menu-item" name="XProduct Admin" section="system.admin/configuration" weight="10"> 
  <description>Link to xproduct-admin page.</description> 
  <label key="xproduct.admin.label" /> 
  <link linkId="xproduct-admin-link">/plugins/servlet/xproduct/admin</link> 
</web-item> 
```

Astute readers will notice the suspicious lack of the `application` tag on that `web-item` element. Well, in Confluence, if you add the `application` attribute, your `web-item` won't show up at all. We'll leave it off here, which is safe because none of the other Atlassian applications have a `system.admin/configuration` section--at least, at the time of this writing they don't.

To add a link in the 'General menu' in the RefApp's administration area.

``` xml
<web-item key="refapp-menu-item" name="XProduct Admin" section="system.admin/general" weight="10" application="refapp"> 
  <description>Link to xproduct-admin page.</description> 
  <label key="xproduct.admin.label" /> 
  <link linkId="xproduct-admin-link">/plugins/servlet/xproduct/admin</link> 
</web-item> 
```

That's it! We're done! Let's run it!

## Step 8. Build, install and run the plugin

Start your RefApp application again by entering the `atlas-run` command, or use a command below to try the application in another product. After the application starts, navigate to the plugin page by appending the plugin path to the base application URL. For example, for JIRA the path would be:

<a href="http://localhost:2990/jira/plugins/servlet/xproduct/admin" class="uri external-link">http://localhost:2990/jira/plugins/servlet/xproduct/admin</a>

The startup commands are:

-   For JIRA

    ``` bash
    atlas-run --product jira --version 6.4.14
    ```

-   For Confluence

    ``` bash
    atlas-run --product confluence --version 5.10.8
    ```

-   For Bamboo

    ``` bash
    atlas-run --product bamboo --version 5.14.1
    ```

If a link to the plugin does not exist, check that the plug-in we created is loaded via "Manage add-on", selecting the option to see "All add-ons" and looking for the entry `xproduct-admin-ui-plugin`.

{{% tip %}}

Congratulations, that's it

Have a chocolate!

{{% /tip %}}

##### RELATED TOPICS

[About the Atlassian RefApp](/server/framework/atlassian-sdk/about-the-atlassian-refapp)

<a href="http://docs.atlassian.com/sal-api/2.0.16-SNAPSHOT/com/atlassian/sal/api/user/UserManager.html" class="external-link">SAL UserManager</a>

<a href="http://docs.atlassian.com/atlassian-plugins-webresource/2.1.5/atlassian-plugins-webresource/apidocs/com/atlassian/plugin/webresource/WebResourceManager.html" class="external-link">WebResourceManager</a>

<a href="/pages/createpage.action?spaceKey=AUI&amp;title=Forms" class="createlink">AUI class attributes</a>












































































































































































