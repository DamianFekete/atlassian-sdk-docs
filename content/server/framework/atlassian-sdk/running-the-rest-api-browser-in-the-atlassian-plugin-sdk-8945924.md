---
title: Running the REST API Browser in the Atlassian Plugin Sdk 8945924
aliases:
    - /server/framework/atlassian-sdk/running-the-rest-api-browser-in-the-atlassian-plugin-sdk-8945924.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8945924
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8945924
confluence_id: 8945924
platform:
product:
category:
subcategory:
---
# Documentation : Running the REST API Browser in the Atlassian Plugin SDK

The Atlassian REST API Browser (RAB) is a tool for discovering the REST APIs and other remote APIs available in Atlassian applications, including JIRA, Confluence, and the other Atlassian products.

RAB shows you all the REST and JSON-RPC resources in the application, displays the methods for each resource, and allows you to make test calls against the methods. If you have installed a plugin that creates additional REST resources for the application, RAB will also discover those resources.

## Quick start

Already using the [Atlassian Plugin SDK](https://developer.atlassian.com/display/DOCS/Working+with+the+SDK)? Then you already have RAB. This is a quick start guide to using it:

1.  Do an `atlas-run` or `atlas-debug` or `atlas-run-standalone` as usual. The Atlassian application (JIRA, Confluence, or any of the others) will be installed with the REST API Browser plugin enabled.
2.  Go to the application's administration screen in your web browser.
3.  Click **REST API Browser** on the administration screen.
4.  Choose an API from the dropdown list at the top left of the screen.
5.  Choose a resource from the list on the left of the screen. The REST API Browser will show you the methods (GET, POST, PUT, etc) and the parameters available for that resource.
6.  To test the resource, enter the parameter values as prompted then click **Execute**.

## More detail about the above steps

This section has more detail about getting the Atlassian Plugin SDK, using it to run an Atlassian application such as JIRA or Confluence, and then finding the REST API Browser.

The Atlassian Plugin SDK is a tool for developers who want to create a plugin (add-on) for an Atlassian application. The SDK includes Maven, a correctly-configured Maven `settings.xml` file, and a number of shell scripts to speed up and simplify plugin development.

Even if you do not want to develop a plugin, you can use the SDK to start up an Atlassian application in plugin development mode. This will give you access to the REST API Browser and other development tools.

### Step 1. Get the Atlassian Plugin SDK

Follow the guide to [installing the Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project). You can skip the last step, which sets up an IDE (Eclipse, IDEA or NetBeans), if you do not need a development environment.

### Step 2. Use the Atlassian Plugin SDK to run an application

Follow the steps for option 1 or option 2.

**Option 1: Standalone application.** This will run the application without installing a sample plugin. Let's assume that you want to run the REST API Browser in JIRA:

1.  Create a directory in your file system to store the application executables. For example, `myjira`.
2.  Open a command window.
3.  Go to the new directory, `myjira`.
4.  Run `atlas-run-standalone --product APPLICATION`. For example, `atlas-run-standalone --product jira`.
    -   *Note:* There are two dashes in front of the word `product`.
    -   Replace the word `APPLICATION` with the correct application name: `jira`, `confluence`, `crowd`, `fecru`, `bamboo`.

**Option 2: Application with sample plugin.** If you want to install the application with a sample 'hello world' plugin for further development, follow these steps:

1.  Run `atlas-create-APPLICATION-plugin`. For example, `atlas-create-jira-plugin`. Details are in [Creating a Plugin Skeleton with the Atlassian SDK](/server/framework/atlassian-sdk/creating-a-plugin-skeleton-with-the-atlassian-sdk).
2.  Go to the new folder, created in the above step, where your plugin's `pom.xml` is located.
3.  Run `atlas-run`. Details are in [Start a Host Application with a Plugin Installed](/server/framework/atlassian-sdk/start-a-host-application-with-a-plugin-installed).
4.  Brew some hot chocolate. The download may take a while.

### Step 3. Find the REST API Browser in the application

After following the above steps, you will have the application running on your computer. When all the downloads and installation are complete, you will see a message in your command window that includes the URL for the local installation of the application. For JIRA, the message will look something like this:

    [INFO] jira started successfully in 174s at http://localhost:2990/jira
    [INFO] Type CTRL-D to shutdown gracefully
    [INFO] Type CTRL-C to exit

Now you can access the application in your browser and use the REST API Browser from the application user interface:

1.  Go to your web browser and enter the URL given for your application. For example, `http://localhost:2990/jira`.
2.  Enter the username and password: `admin` / `admin`.
3.  Go to the application's administration screen. For example:
    -   In JIRA: Click **Administration** at top right of the screen.
    -   In Confluence: Click **Browse** &gt; **Confluence Admin**.
4.  Click **REST API Browser**.

### Step 4. View and test the APIs and resources

Quick start:

1.  Choose an API from the dropdown list at the top left of the screen.
2.  Choose a resource from the list on the left of the screen.
3.  Examine the methods (GET, POST, PUT, etc) and the parameters available for that resource.
4.  To test the resource, enter the parameter values as prompted then click **Execute**.

For details, see [how to use RAB](/server/framework/atlassian-sdk/browsing-and-testing-rest-apis-in-your-application-8947336.html).

##### RELATED TOPICS

<a href="/pages/createpage.action?spaceKey=RAB&amp;title=Overview+of+the+Atlassian+REST+API+Browser" class="createlink">Overview of the Atlassian REST API Browser</a>  
[Browsing and Testing REST APIs in your Application](/server/framework/atlassian-sdk/browsing-and-testing-rest-apis-in-your-application-8947336.html)  
[Documenting your APIs with the Atlassian REST API Browser](/server/framework/atlassian-sdk/documenting-your-apis-with-the-atlassian-rest-api-browser)  
[atlas-run-standalone](/server/framework/atlassian-sdk/atlas-run-standalone)





















































































































































































































































