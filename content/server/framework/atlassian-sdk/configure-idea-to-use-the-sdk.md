---
aliases:
- /server/framework/atlassian-sdk/configure-idea-to-use-the-sdk-2818645.html
- /server/framework/atlassian-sdk/configure-idea-to-use-the-sdk-2818645.md
category: devguide
confluence_id: 2818645
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818645
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818645
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-in-an-ide/configure-idea-to-use-the-sdk
new_url: /server/framework/atlassian-sdk/configure-idea-to-use-the-sdk
platform: server
product: atlassian-sdk
subcategory: learning
title: Configure IDEA to use the SDK
---
# Configure IDEA to use the SDK

Setting up IDEA for plugin development is a breeze. Simply create a plugin project using the `atlas-create-*-plugin` command (for example, [atlas-create-confluence-plugin](/server/framework/atlassian-sdk/atlas-create-confluence-plugin)) and then load the project's POM file into IntelliJ. IntelliJ's Maven integration will generate the appropriate project files for you.

While it's possible to run the Atlassian Plugin SDK commands from within IDEA as custom run commands, in practice, most developers simply use IDEA for code editing and debugging, and use a separate console to run the `atlas-run`, `atlas-debug`, or other Atlassian Plugin SDK command. After you've made project changes with the SDK, IDEA will detect the file changes on disk and prompt you to reimport the project.

After starting the Atlassian application, you can connect to it from IDEA for debugging on the default debug port 5005, as described in [Creating a Remote Debug Target](/server/framework/atlassian-sdk/creating-a-remote-debug-target). 

## Adding a plugin project to IDEA

To load the plugin project in IDEA:

1.  In IDEA, click **File** &gt; **Import Project**.
2.  Navigate to the root of your plugin project directory and select the `pom.xml` file. 
3.  In the wizard, configure project settings as desired.  
    For best results, you should set the project JDK to the Java home used by the SDK, such as `/usr/lib/jdk/jdk-1-6`. (To see what the SDK uses for its Java home, enter the `atlas-version` command and look for the Java home indicated in the output of the command.
4.  Click **Finish** when done.  
    Once IDEA loads your project, you're ready to go. 

<img src="/server/framework/atlassian-sdk/images/idea.jpg" width="650" />

## Increasing the amount of memory available to IDEA

You may find it beneficial to increase the default amount of memory allocated for IDEA. You can do this by modifying the VM options located in:

`<Install-dir>\bin\idea.exe.vmoptions`

`<Install-dir>\bin\idea.vmoptions`

`/Applications/IntelliJ\ IDEA\ 9.0.4.app/Contents/Info.plist`

For example, if you installed the application in it's default location on Windows you may see something like this:

    C:\Program Files\JetBrains\IntelliJ IDEA 9.0.4\bin\idea.exe.vmoptions

Here are sample settings:

``` bash
-Xms32m
-Xmx256m
-XX:MaxPermSize=128m
-ea
```

























































































































































































