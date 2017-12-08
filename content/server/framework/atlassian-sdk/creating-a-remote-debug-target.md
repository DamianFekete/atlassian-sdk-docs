---
aliases:
- /server/framework/atlassian-sdk/creating-a-remote-debug-target-2818651.html
- /server/framework/atlassian-sdk/creating-a-remote-debug-target-2818651.md
category: devguide
confluence_id: 2818651
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818651
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818651
date: '2017-12-08'
guides: guides
legacy_title: Creating a Remote Debug Target
platform: server
product: atlassian-sdk
subcategory: learning
title: Creating a remote debug target
---
# Creating a remote debug target

This page describes how to set up standard IDE debugging tools to work with Atlassian plugins.

 

## About Remote Debug Targets

Since plugin are deployed as part of another application (e.g., Confluence or JIRA), you can't just start your IDE in debug mode to debug the plugin. Your IDE must connect to the Atlassian application that hosts the plugin. In terms of your IDE configuration, the Atlassian host application needs to be configured as the remote debug target.

To connect to an Atlassian application, you need to connect to it in debug mode. With the SDK, you use the [atlas-debug](/server/framework/atlassian-sdk/atlas-debug) command to start the application in debug mode. By default, this command opens port 5005 as the debug port, the default for Java debugging. But you can specify another using the `--jvm-debug-port` parameter. When setting up your debug target, configure this port value as the debug port, as described below

## Creating a remote debug target in IDEA

1.  From the IDEA main menu, click **Run** &gt; **Edit Configurations**.
2.  Click the plus button and choose **Remote**.  
      
    <img src="/server/framework/atlassian-sdk/images/intellijideadebugging-03.png" width="650" />  
    The new remote target configuration appears with default settings, including a default debug port of 5005. If you start the Atlassian application using the default settings for the `atlas-debug` command, you do not need to change the default target values.
3.  Enter a descriptive name for your profile in the **Name** field and click **OK**. (Or click the **Debug** button if you created your profile from the **Run** &gt; **Debug** menu.) 
4.  If you have not already done so, start the Atlassian application using the `atlas-debug` command. For example:

    ``` bash
    atlas-debug --product confluence
    ```

5.  When the Atlassian application finishes starting up, go to **Run** &gt; **Debug** and choose your new remote target profile.

You can now attempt to use your plugin in the Atlassian application to generate and receive debugging information in IDEA.  
<img src="/server/framework/atlassian-sdk/images/intellijideadebugging-01.png" width="650" /> 

## Creating a remote debug target in Eclipse

1.  From the Eclipse main menu, click **Run** &gt; **Debug Configurations**.
2.  Double-click **Remote Java Application**.
3.  In the **Name** field, enter a descriptive name for your profile.
4.  Set the **Port** field to 5005, or the port number you will use to start the Atlassian application in debug mode.  
    <img src="/server/framework/atlassian-sdk/images/eclipsedebugging-01.jpg" width="650" />  
      
5.  Click **Apply** to save your configuration, or just **Debug** to save your configuration and start debugging.

You can now start the Atlassian application in debug mode and connect to it from Eclipse.




















































































































































