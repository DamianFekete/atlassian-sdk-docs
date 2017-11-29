---
title: Plugin Tutorial Step Build and Test 2818459
aliases:
    - /server/framework/atlassian-sdk/-plugin-tutorial-step-build-and-test-2818459.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818459
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818459
confluence_id: 2818459
platform:
product:
category:
subcategory:
---
# Documentation : \_Plugin Tutorial Step - Build and Test

Follow these steps to build and install your plugin, so that you can test your code. If you have not already started the application, start it now:

-   Open a command window and go to the plugin root folder (where the `pom.xml` is located).
-   Run `atlas-run` (or `atlas-debug` if you might want to launch the debugger in your IDE).

From this point onwards, you can use [QuickReload](https://developer.atlassian.com/docs/developer-tools/automatic-plugin-reinstallation-with-quickreload) to reinstall your plugin behind the scenes as you work, simply by rebuilding your plugin.

{{% warning %}}

FastDev and atlas-cli have been deprecated. Please use [Automatic Plugin Reinstallation with QuickReload](https://developer.atlassian.com/docs/developer-tools/automatic-plugin-reinstallation-with-quickreload) instead.

{{% /warning %}}

 

To trigger the reinstallation of your plugin:

1.  Make the changes to your plugin module.
2.  Open the Developer Toolbar.  
    <img src="/server/framework/atlassian-sdk/images/fastdev1.png" width="600" />
3.  Press the FastDev icon.  
    <img src="/server/framework/atlassian-sdk/images/fastdev2.png" width="600" />  
    The system rebuilds and reloads your plugin:  
    <img src="/server/framework/atlassian-sdk/images/fastdev3.png" width="600" />

Use live reload to view real-time updates to templates and other resources:

1.  Open the Developer Toolbar.
2.  Press the live reload icon.  
    The  icon starts to revolve indicating it is on.
3.  Edit your project resources.
4.  Save your changes:  
    Back in the host application, your plugin displays any user visible changes you make. 

Go back to the browser. The updated plugin has been installed into the application, and you can test your changes.

The full instructions are in the [SDK guide](/server/framework/atlassian-sdk/working-with-the-sdk-2818723.html).

























