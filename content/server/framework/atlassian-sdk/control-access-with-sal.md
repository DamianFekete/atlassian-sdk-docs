---
aliases:
- /server/framework/atlassian-sdk/control-access-with-sal-16352154.html
- /server/framework/atlassian-sdk/control-access-with-sal-16352154.md
category: devguide
confluence_id: 16352154
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16352154
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16352154
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/getting-started/learn-the-development-platform-by-example/control-access-with-sal
new_url: /server/framework/atlassian-sdk/control-access-with-sal
platform: server
product: atlassian-sdk
subcategory: learning
title: Control access with SAL
---
# Control access with SAL

By now, you're well-acquainted with the environment your plugin runs in. In this section, you'll add SAL (Secure Access Layer) modules to your plugin and update the subsequent dependencies in your `pom.xml`. This section includes the following concepts and instructions:

 

## Learn more about SAL

SAL is a component library of the Atlassian development platform. SAL supplies core plugin services shared between all Atlassian applications. Since your plugin is compatible with all Atlassian applications, SAL is an apt API to use in development.

## Step 1. Check that SAL modules have been added

The `atlas-create-refapp-plugin` command has already generated `com.atlassian.sal` as a dependency. In `pom.xml`, look for the following dependency:

``` xml
<dependency>
    <groupId>com.atlassian.sal</groupId>
    <artifactId>sal-api</artifactId>
    <scope>provided</scope>
</dependency>
```

## Step 2. Update `MyPluginServlet.java`

Now that you've added additional APIs to your project you'll update the `import` statements as well as the body of the class. 

1.  Open `MyPluginServlet.java` in Eclipse.
2.  Replace your class with the following: 

    ``` java
    package com.atlassian.plugins.tutorial.refapp;
    import org.slf4j.Logger;
    import org.slf4j.LoggerFactory;
    import javax.servlet.*;
    import javax.servlet.http.HttpServlet;
    import javax.servlet.http.HttpServletRequest;
    import javax.servlet.http.HttpServletResponse;
    import java.io.IOException;
    import java.net.URI;
    import com.atlassian.sal.api.auth.LoginUriProvider;
    import com.atlassian.sal.api.user.UserManager;

    import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
    import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
    import javax.inject.Inject;

    @Scanned
    public class MyPluginServlet extends HttpServlet
    {
        private static final Logger log = LoggerFactory.getLogger(MyPluginServlet.class);
        @ComponentImport
        private final UserManager userManager;
        @ComponentImport
        private final LoginUriProvider loginUriProvider;

        @Inject
        public MyPluginServlet(UserManager userManager,
                               LoginUriProvider loginUriProvider) {
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
            response.setContentType("text/html");
            response.getWriter().write("<html><body>Hi again! Looking good.</body></html>");
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
    }
    ```

    The new contents of `MyPluginServlet` add import statements for `UserManager` and `LoginUriProvider`. The class now checks to see if the user is logged in (if their username isn't null). If users aren't logged in, `sendRedirect` will prompt the user to log in.

    You haven't yet added anything in `MyPluginServlet.java`  corresponding to `TemplateRenderer `or `PluginSettingsFactory`. You'll add dependencies in future steps.

3.  Save your changes and close `MyPluginServlet`.

## Step 3. Run QuickReload to Update Changes

In order to load the changes in JIRA and verify that your `UserManager` and `LoginUriProvider` services are working with your plugin, instead of taking down the JIRA instance and restarting using atlas-run, it is quicker and easier to use QuickReload to reload the plugin.

1.  Run `atlas-mvn package` in the project root `adminUI` to reload the plugin.
2.  Navigate to your running instance of JIRA in your browser.  
    JIRA is usually accessible at **<a href="http://localhost:2990/jira/secure/Dashboard.jspa" class="uri external-link">http://localhost:2990/jira/secure/Dashboard.jspa</a>**.
3.  Navigate to your plugin at **<a href="http://localhost:2990/jira/plugins/servlet/test" class="uri external-link">http://localhost:2990/jira/plugins/servlet/test</a>**.  
    If already logged in, you should see the "Hi again! Looking good" message.  
    If you're not logged in, you'll be prompted to log in with your credentials (`admin/admin`):  
    When you click **Login**, you'll be redirect to the plugin as depicted earlier.  
      

## Next Steps

You've added SAL services to your plugin and verified that your dependencies are correctly configured. Now, [create a GUI using Atlassian User Interface (AUI) resources and templates](https://developer.atlassian.com/display/DOCS/Create+a+GUI+with+templates+and+AUI).

































































































































































