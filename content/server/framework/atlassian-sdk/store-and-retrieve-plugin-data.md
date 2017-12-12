---
aliases:
- /server/framework/atlassian-sdk/store-and-retrieve-plugin-data-16352160.html
- /server/framework/atlassian-sdk/store-and-retrieve-plugin-data-16352160.md
category: devguide
confluence_id: 16352160
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16352160
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16352160
date: '2017-12-08'
guides: tutorials
legacy_title: Store and retrieve plugin data
platform: server
product: atlassian-sdk
subcategory: learning
title: Store and retrieve plugin data
---
# Store and retrieve plugin data

Your plugin now has a sophisticated look and feel. In this last section of the tutorial you'll make your plugin fully functional. You'll add a `POST` method to the admin.vm template so you can enter and retrieve user data.

 

## About plugin data storage

When you added component import modules to your plugin, you added `PluginSettingsFactory`. This import allows you to use `PluginSettings`, a SAL service that manages your plugin data storage. The `POST` method you add to your admin.vm template will submit the form to the database, and `PluginSettings` permits you to retrieve stored submissions from the database.

## Step 1. Add a `POST` method to your admin.vm template

This is one of the most common HTTP requests. In this step, you'll add a line of code to your admin.vm file.

1.  Open your admin.vm file from `src/main/resources`.

2.  Add a `POST` method in the `<form>` tag.

    ``` xml
    <html>
      <head>
        <title>MyServlet Admin</title>
        <meta name="decorator" content="atl.admin">
      </head>
      <body>
        <form id="admin" class="aui" action="" method="POST">
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

3.  Save and close the file.

## Step 2. Update project files in Eclipse

In this step you'll update the dependencies in your `pom.xml` and `MyPluginServlet` so you can store and retrieve data. 

1.  Open `MyPluginServlet.java`.
2.  Replace the contents of the class with the following.

    ``` java
    package com.atlassian.plugins.tutorial.refapp;

    import java.util.HashMap;
    import java.util.Map;
    import java.io.IOException;
    import java.net.URI;

    import javax.servlet.*;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;

    import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
    import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
    import javax.inject.Inject;

    import com.atlassian.sal.api.auth.LoginUriProvider;
    import com.atlassian.sal.api.user.UserManager;
    import com.atlassian.templaterenderer.TemplateRenderer;
    import com.atlassian.sal.api.pluginsettings.PluginSettings;
    import com.atlassian.sal.api.pluginsettings.PluginSettingsFactory;

     
    @Scanned
    public class MyPluginServlet extends HttpServlet
    {
        private static final String PLUGIN_STORAGE_KEY = "com.atlassian.plugins.tutorial.refapp.adminui";
        @ComponentImport
        private final UserManager userManager;
        @ComponentImport
        private final LoginUriProvider loginUriProvider;
        @ComponentImport
        private final TemplateRenderer templateRenderer;
        @ComponentImport
        private final PluginSettingsFactory pluginSettingsFactory;

        @Inject
        public MyPluginServlet(UserManager userManager, LoginUriProvider loginUriProvider, TemplateRenderer templateRenderer, PluginSettingsFactory pluginSettingsFactory) {
            this.userManager = userManager;
            this.loginUriProvider = loginUriProvider;
            this.templateRenderer = templateRenderer;
            this.pluginSettingsFactory = pluginSettingsFactory;
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
            Map<String, Object> context = new HashMap<String, Object>();

            PluginSettings pluginSettings = pluginSettingsFactory.createGlobalSettings();

            if (pluginSettings.get(PLUGIN_STORAGE_KEY + ".name") == null){
                String noName = "Enter a name here.";
                pluginSettings.put(PLUGIN_STORAGE_KEY +".name", noName);
            }

            if (pluginSettings.get(PLUGIN_STORAGE_KEY + ".age") == null){
                String noAge = "Enter an age here.";
                pluginSettings.put(PLUGIN_STORAGE_KEY + ".age", noAge);
            }

            context.put("name", pluginSettings.get(PLUGIN_STORAGE_KEY + ".name"));
            context.put("age", pluginSettings.get(PLUGIN_STORAGE_KEY + ".age"));
            response.setContentType("text/html;charset=utf-8");
            templateRenderer.render("admin.vm", response.getWriter());

        }

        @Override
        protected void doPost(HttpServletRequest req, HttpServletResponse response)
                throws ServletException, IOException {
            PluginSettings pluginSettings = pluginSettingsFactory.createGlobalSettings();
            pluginSettings.put(PLUGIN_STORAGE_KEY + ".name", req.getParameter("name"));
            pluginSettings.put(PLUGIN_STORAGE_KEY + ".age", req.getParameter("age"));
            response.sendRedirect("test");
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

        // This is what your MyPluginServlet.java should look like in its final stages.

    }
    ```

3.  Save and close `MyPluginServlet`.

## Step 3. Enter and retrieve data 

The final step is to verify that your plugin can store and retrieve data. Here you'll make an entry and confirm that you can look it up using the `PLUGIN_STORAGE_KEY`. You'll perform your lookups in the Plugin Data Console.

1.  Reload your plugin and return to** <a href="http://localhost:2990/jira/plugins/servlet/test" class="uri external-link">http://localhost:2990/jira/plugins/servlet/test</a>**.**  
    **
2.  Make an entry such as Charlie/34 for Name/Age and click **Save**.
3.  Navigate to the **Plugin Data Editor**.  
    You can navigate directly to the editor at **<a href="http://localhost:2990/jira/plugins/servlet/pde" class="uri external-link">http://localhost:2990/jira/plugins/servlet/pde</a>**  
    Alternatively you can click **Question Mark &gt; Developer Toolbox &gt; Plugin Data Console**.
4.  Under Plugin Settings Query, choose **Global**.
5.  For the Data Key, enter `com.atlassian.plugins.tutorial.refapp.adminui.name` to query the names entered, or `com.atlassian.plugins.tutorial.refapp.adminui.age` to query the ages entered.  
    This is the `PLUGIN_STORAGE_KEY` value that you coded into your `MyPluginServlet` class.
6.  Click **Lookup**.

    You'll see your entries displayed in the **Results** section.

## Next steps

You've created a plugin complete with a GUI that accepts and stores data - no minor feat. You might consider learning more about [developer tools](https://developer.atlassian.com/display/DOCS/Developer+Tools), [creating plugin tests](https://developer.atlassian.com/display/DOCS/Writing+and+Running+Plugin+Tests), or [perusing the FAQ](https://developer.atlassian.com/display/DOCS/Plugin+Development+FAQ):  

[Developing plugins for Confluence](https://developer.atlassian.com/display/CONFDEV/Confluence+Plugin+Guide)

[Developing for the Marketplace](https://developer.atlassian.com/display/MARKET/Developing+for+the+Marketplace)

























































































































































































































