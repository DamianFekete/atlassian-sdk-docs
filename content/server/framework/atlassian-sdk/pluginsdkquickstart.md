---
aliases:
- /server/framework/atlassian-sdk/-pluginsdkquickstart-5669863.html
- /server/framework/atlassian-sdk/-pluginsdkquickstart-5669863.md
category: devguide
confluence_id: 5669863
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669863
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669863
date: '2017-12-11'
legacy_title: _PluginSDKQuickStart
platform: server
product: atlassian-sdk
subcategory: other
title: _PluginSDKQuickStart
---
# \_PluginSDKQuickStart

1.  Download and install the latest <a href="http://java.sun.com/" class="external-link">JDK</a>.
2.  Download and install the <a href="https://maven.atlassian.com/public/com/atlassian/amps/atlassian-plugin-sdk" class="external-link">Atlassian Plugin SDK</a>.
3.  Create a plugin skeleton using `atlas-create-APPLICATION-plugin`. For example, `atlas-create-confluence-plugin`.
4.  Type `atlas-run` to run your plugin's host application with the plugin skeleton installed.
5.  To dynamically install your plugin in the host application, use the Atlassian CLI (command line interface). In a new terminal window, run `atlas-cli` then `pi`. ("pi" stands for "plugin install".)
6.  Open the project in your IDE and start coding.
7.  Make sure that your plugin is secure. See this <a href="http://confluence.atlassian.com/display/ATL/Securing+your+Plugin" class="external-link">AtlasCamp 2010 presentation</a>.
8.  As you make changes, type `pi` again to load your latest code.
9.  Write [unit and functional tests](https://developer.atlassian.com/pages/viewpage.action?pageId=2818653).
10. When you're ready, [release your plugin](/server/framework/atlassian-sdk/packaging-and-releasing-your-plugin).

The brief instructions above are covered in more detail in [installing the Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

































































































