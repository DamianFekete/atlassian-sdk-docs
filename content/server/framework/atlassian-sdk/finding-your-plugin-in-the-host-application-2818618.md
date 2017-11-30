---
aliases:
- /server/framework/atlassian-sdk/finding-your-plugin-in-the-host-application-2818618.html
- /server/framework/atlassian-sdk/finding-your-plugin-in-the-host-application-2818618.md
category: devguide
confluence_id: 2818618
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818618
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818618
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/development-cycle/finding-your-plugin-in-the-host-application
new_url: /server/framework/atlassian-sdk/finding-your-plugin-in-the-host-application
platform: server
product: atlassian-sdk
subcategory: learning
title: Finding your plugin in the host application
---
# Finding your plugin in the host application

After starting the host application [with your plugin installed](/server/framework/atlassian-sdk/start-a-host-application-with-a-plugin-installed), you can verify the installation from the application's administration console. In addition to showing the status of the plugin and its component modules, the console presents any configuration settings exposed by the plugin.

## Checking your Plugin in UPM

The Universal Plugin Manager (UPM) provides a common administration interface for managing add-ons in Atlassian applications. The interface is the same whether using Confluence, JIRA, Bamboo, Stash, or Fisheye/Crucible. 

To see your plugin in the console:

1.  Open the administration console for the application. For example, in JIRA, as a system administrator, click the Administration link.
2.  In the Administration Console page, click Manage Add-ons.  
    The page shows the add-ons that are installed in the application in two groups: user installed and system add-ons.
3.  Find your plugin in the user-installed add-ons list, and click it to expand its view.  
    <img src="/server/framework/atlassian-sdk/images/customaddonview.png" width="650" />

For more information about using the UPM, see the <a href="https://confluence.atlassian.com/display/UPM/Universal+Plugin+Manager+Documentation" class="external-link">Universal Plugin Manager Documentation</a>.

## Checking your Plugin in the Refapp

In the RefApp, the procedure is slightly different. To see details of your plugin and other useful information in the refapp, go to <a href="http://localhost:5990/refapp/index.jsp" class="uri external-link">http://localhost:5990/refapp/index.jsp</a>.

## Verifying your Plugin in Crowd

Crowd does not currently have a plugin management interface. To verify your plugin, try some of the functionality provided by your plugin to make sure it works.

















































































































































