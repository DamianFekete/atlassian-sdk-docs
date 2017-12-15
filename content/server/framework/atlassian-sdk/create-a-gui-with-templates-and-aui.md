---
aliases:
- /server/framework/atlassian-sdk/create-a-gui-with-templates-and-aui-16352157.html
- /server/framework/atlassian-sdk/create-a-gui-with-templates-and-aui-16352157.md
category: devguide
confluence_id: 16352157
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16352157
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16352157
date: '2017-12-08'
guides: tutorials
legacy_title: Create a GUI with templates and AUI
platform: server
product: atlassian-sdk
subcategory: learning
title: Create a GUI with templates and AUI
---
# Create a GUI with templates and AUI

You've added SAL modules and built the foundation for an interactive plugin by creating a servlet component. Now, you'll add a GUI for your users to input data. You can use resources Atlassian provides in the Atlassian User Interface (AUI). This section of the tutorial will walk you through creating and managing Velocity templates, adding CSS, and viewing your plugin in its GUI form. This section includes the following instructions: 

## Introduction to AUI (Atlassian User Interface)

AUI is a library of resources you can use to make your plugin visually integrated with Atlassian products. The AUI library includes CSS, JavaScript, and other templates. Using resources from this library ensures your plugin interface is compliant with Atlassian Design Guidelines (ADG). 

In earlier steps, you added a component module called `TemplateRenderer`. Here, you'll update your source code to import `TemplateRenderer`. You'll configure `TemplateRenderer` to use a Velocity template to format your user interface. Then, you'll  add AUI elements and templates for `TemplateRenderer` to display for an Atlassian look and feel.

## Step 1. Update dependencies in the `pom.xml`

Here, you'll update the dependencies to reflect the `TemplateRenderer` module you added earlier. 

1.  Open your `pom.xml`.
2.  Locate the `<dependency>` section.
3.  Find the `com.atlassian.sal` group.
4.  Add the `templateRenderer` in a dependency group above the `com.atlassian.sal` group.

    ``` xml
           <dependency>
                <groupId>com.atlassian.templaterenderer</groupId>
                <artifactId>atlassian-template-renderer-api</artifactId>
                <scope>provided</scope>
            </dependency>
    ```

5.  Save and close the file.

## Step 2. Create a Velocity template

Atlassian applications use both .soy (Soy) and .vm (Velocity) templates for rendering user interfaces. In this example, you'll create a Velocity template to support your GUI.

1.  Navigate to `src/main/resources` within the base directory `adminUI`.

2.  Create an** admin.vm** Velocity template, and fill in the contents with:

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

## Step 3. Update `MyPluginServlet` 

Up until this point, your servlet has been displaying HTML from your `MyPluginServlet` class. Now you'll update the class to render content using the `TemplateRenderer` component import you added earlier. `TemplateRenderer` will display the admin.vm template you just created. 

1.  Update `MyPluginServlet.java` to import `TemplateRenderer` and use your new admin.vm template.

    `MyPluginServlet` should look as follows: 

    ``` java
    package com.atlassian.plugins.tutorial.refapp;

    import javax.servlet.*;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import java.io.IOException;

    import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
    import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
    import javax.inject.Inject;

    import java.net.URI;
    import com.atlassian.sal.api.auth.LoginUriProvider;
    import com.atlassian.sal.api.user.UserManager;
    import com.atlassian.templaterenderer.TemplateRenderer;
     
    @Scanned
    public class MyPluginServlet extends HttpServlet
    {
        @ComponentImport
        private final UserManager userManager;
        @ComponentImport
        private final LoginUriProvider loginUriProvider;
        @ComponentImport
        private final TemplateRenderer templateRenderer;

        @Inject
        public MyPluginServlet(UserManager userManager, LoginUriProvider loginUriProvider, TemplateRenderer templateRenderer)
        {
            this.userManager = userManager;
            this.loginUriProvider = loginUriProvider;
            this.templateRenderer = templateRenderer;
        }

        @Override
        public void doGet(HttpServletRequest request, HttpServletResponse response) throws ServletException, IOException
        {
            String username = userManager.getRemoteUsername(request);
            if (username == null || !userManager.isSystemAdmin(username))
            {
                redirectToLogin(request, response);
                return;
            }
            templateRenderer.render("admin.vm", response.getWriter());
        }
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
        // This is what your MyPluginServlet.java class should look like after creating your admin.vm template
    }
    ```

2.  Save the changes and close the file.
3.  Use `atlas-mvn package` to reload your plugin.
4.  Return to** <a href="http://localhost:2990/jira/plugins/servlet/test" class="uri external-link">localhost:2990/jira/plugins/servlet/test</a>.**
5.  Your servlet reloads, now with fields from your admin.vm:   
      
## Step 4. Add a decorator and CSS

You have a GUI, but it's not much to look at. Now you can add some visual appeal to your plugin using Atlassian User Interface (AUI) resources and some CSS.

1.  Open your **admin.vm** Velocity template.

2.  Add a `<meta>` element directly after the title. 

    Insert `<meta name="decorator" content="atl.admin">`. This tag should be inside the `<head>` section.

    ``` xml
    <html>
      <head>
        <title>My Admin</title>
        <meta name="decorator" content="atl.admin">
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

3.  Save the file.   
    Leave the file open for future changes.
4.  Use QuickReload to update your changes.  
    The page loads and now uses an AUI decorator. 
5.  Return to your admin.vm file. 
6.  Add some CSS. 

    Replace your admin.vm contents with the following:

    ``` xml
    <html>
      <head>
        <title>MyServlet Admin</title>
        <meta name="decorator" content="atl.admin">
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

7.  Reload the plugin and return once again to your servlet at **<a href="http://localhost:2990/jira/plugins/servlet/test" class="uri external-link">localhost:2990/jira/plugins/servlet/test</a>**.

## Next steps

Your add-on looks great! Now you'll [add a `POST` method so it can store and retrieve user data](https://developer.atlassian.com/display/DOCS/Store+and+retrieve+plugin+data).
