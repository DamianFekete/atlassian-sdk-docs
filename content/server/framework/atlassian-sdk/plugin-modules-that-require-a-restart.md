---
aliases:
- /server/framework/atlassian-sdk/plugin-modules-that-require-a-restart-852017.html
- /server/framework/atlassian-sdk/plugin-modules-that-require-a-restart-852017.md
category: devguide
confluence_id: 852017
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852017
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852017
date: '2017-12-08'
legacy_title: Plugin Modules that Require a Restart
platform: server
product: atlassian-sdk
subcategory: faq
title: Plugin modules that require a restart
---
# Plugin modules that require a restart

Plugin modules can be marked with an `@RequiresRestart` annotation which means the plugin will not be reloaded until the application server is restarted. See [Plugins that Cannot be Reloaded with FastDev or pi](/server/framework/atlassian-sdk/plugins-that-cannot-be-reloaded-with-fastdev-or-pi).
