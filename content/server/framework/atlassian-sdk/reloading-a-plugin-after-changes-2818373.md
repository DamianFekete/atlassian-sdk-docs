---
title: Reloading a Plugin After Changes 2818373
aliases:
    - /server/framework/atlassian-sdk/reloading-a-plugin-after-changes-2818373.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818373
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818373
confluence_id: 2818373
platform:
product:
category:
subcategory:
---
# Documentation : Reloading a Plugin after Changes

This page describes the various methods you can use to reload a plugin and check your changes.

## FastDev and Live Reload - The Fastest Way to Run your Changes

There is no need to manually install your plugin into the Atlassian application every time you change the code. Instead, you can use Fastdev in your browser to dynamically reinstall your plugin after each change.  FastDev can also handle reloads for multi-module maven projects that contain multiple plugins. You can also disable FastDev, or configure it to ignore changes in given files or use a different Maven command. Please refer to the [FastDev configuration guide](/server/framework/atlassian-sdk/automatic-plugin-reinstallation-with-fastdev).

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

## Using the CLI to Reload your Plugin

As an alternative to FastDev, you can keep the application running in one command window and use the CLI (command line interface) in another window to dynamically re-install your plugin after each change.

1.  Make your changes in your IDE.
2.  Open a new command window and go to the plugin's root folder (where the `pom.xml` is located).
3.  Run `atlas-cli` to start the CLI.
4.  Wait until you see a message, `Waiting for commands`.
5.  Run `pi` (plugin install) to compile, package and install the plugin.
6.  Go back to your browser.  
    The updated plugin is installed into the application, and you can test your changes. (You may need to refresh the browser page first.)
7.  Lather, rinse, repeat.

**Note:** You can use the shell script directly instead of using the CLI, although the performance is less efficient, just run `atlas-install-plugin`.

## Troubleshooting Reloading

-   The dynamic deployment method via FastDev or CLI will work *most* of the time, but not all plugins are eligible for dynamic installation. Specifically, some versions of some applications mark some module types as requiring a restart. If a plugin uses one of the module types that require a restart, the plugin will be installed but not activated until the application is restarted. And occasionally the host application fails to detect new changes. If you suspect this may be happening, just hit `ctrl-c` in the first window and type `atlas-run` again to completely restart the host app with your latest changes included. See the list of [plugin modules that cannot be dynamically reloaded](/server/framework/atlassian-sdk/plugins-that-cannot-be-reloaded-with-fastdev-or-pi).
-   [If you change pom.xml, you may need to restart the atlas-cli](/server/framework/atlassian-sdk/2818364.html).
-   For other errors, please refer to the [FAQ and troubleshooting section](/server/framework/atlassian-sdk/atlassian-plugin-sdk-faq).

## Other Handy Commands

-   Run `atlas-compile` to compile the plugin.
-   Run `atlas-unit-test` to run the unit tests.
-   Run `atlas-package` to produce the JAR.

The Atlassian Plugin SDK provides many more scripts supporting various goals, as described in the [detailed documentation](/server/framework/atlassian-sdk/working-with-the-sdk).

## Running in Debug Mode

You can use `atlas-debug` instead of `atlas-run`. This sets up the host application so that you can attach your IDE's remote debugger to it. Read the instructions on [setting up a remote debugger](/server/framework/atlassian-sdk/creating-a-remote-debug-target).

## Writing Tests for your Plugin

Atlassian plugins depend on Maven 2 to run their test suites. This is advantageous because all plugins are always tested the same way, and because Bamboo, our continuous integration server, can do likewise. Find out how to [make it happen](/server/framework/atlassian-sdk/writing-and-running-plugin-tests).

















































































































































































































































































































