---
aliases:
- /server/framework/atlassian-sdk/start-a-host-application-with-a-plugin-installed-2818619.html
- /server/framework/atlassian-sdk/start-a-host-application-with-a-plugin-installed-2818619.md
category: devguide
confluence_id: 2818619
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818619
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818619
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/development-cycle/start-a-host-application-with-a-plugin-installed
new_url: /server/framework/atlassian-sdk/start-a-host-application-with-a-plugin-installed
platform: server
product: atlassian-sdk
subcategory: learning
title: Start a host application with a plugin installed
---
# Start a host application with a plugin installed

You can use the Atlassian Plugin SDK to download the Atlassian host application binaries, run a plugin's unit tests, install a plugin (skeleton) and start the host application. When you are done, you can visit the application in your browser, log in as '**admin/admin**', and see your plugin in action.

1.  Open a command window and go to the folder where your plugin's `pom.xml` is located.  
    This is the folder where you created your plugin skeleton.
2.  Type `atlas-run` and press **Enter**.  
    The download can be slow the first time you do it. But the next time you execute the `run` command, it will be much faster because all the binaries are in your local Maven repository.

    {{% note %}}

    If you are on Windows, a Windows Security Alert may ask you if you want to allow the program to accept incoming network connections. Click '**Unblock**' to allow incoming network connections.

    {{% /note %}}

    When all the downloads and installation are complete, the system display a message similar to the following:

    ``` text
    [WARNING] [talledLocalContainer] INFO: Server startup in 87246 ms
    [INFO] [talledLocalContainer] Tomcat 6.x started on port [1990]
    [INFO] confluence started successfully and available at http://localhost:1990/confluence
    [INFO] Type CTRL-C to exit
    ```

3.  Open your browser and go to the URL given in the message.  
    For example, in the message above the URL is <a href="http://localhost:1990/confluence" class="uri external-link">http://localhost:1990/confluence</a> for Confluence. The application's login screen appears.
4.  Log in with username `admin` and password `admin`.
5.  [Find your plugin](/server/framework/atlassian-sdk/finding-your-plugin-in-the-host-application) to confirm that it was deployed.

#### Troubleshooting

-   [Maven Cannot Find Java Mail, Java Activation or JTA](/server/framework/atlassian-sdk/2818709.html)
-   [BeanCreationException from Spring Framework](/server/framework/atlassian-sdk/beancreationexception-from-spring-framework-2818633.html)
-   [Specifying a particular version of the host application](/server/framework/atlassian-sdk/specifying-a-particular-version-of-the-host-application-2818657.html)
-   For other errors, please refer to the [FAQ and troubleshooting section](/server/framework/atlassian-sdk/atlassian-plugin-sdk-faq-2818649.html).

#### About the Application Source Code

Please note: The plugin now knows about the host application's binaries, because it has downloaded the JAR files. But it has not downloaded the application source code. You do not need to have access to the host application's source code to be able to develop a plugin. The JAR files alone will enable you to go and write the plugin, using the application's API.

If you hold a commercial license for an Atlassian application with access to the source code, you can attach the application source code to your plugin project. See how to [use the Atlassian Plugin SDK with a source code license](/server/framework/atlassian-sdk/using-the-atlassian-plugin-sdk-with-a-source-code-license-2818656.html).














































































































































