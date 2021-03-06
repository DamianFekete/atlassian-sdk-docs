---
aliases:
- /server/framework/atlassian-sdk/supporting-websudo-in-your-plugin-2818401.html
- /server/framework/atlassian-sdk/supporting-websudo-in-your-plugin-2818401.md
category: devguide
confluence_id: 2818401
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818401
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818401
date: '2017-12-08'
legacy_title: Supporting WebSudo in your Plugin
platform: server
product: atlassian-sdk
subcategory: faq
title: Supporting WebSudo in your plugin
---
# Supporting WebSudo in your plugin

Support for ﻿Secure Administrator Sessions, called 'WebSudo', was added in Confluence 3.3 (see <a href="#documentation" class="unresolved">documentation</a>) and JIRA 4.3 (see <a href="#documentation" class="unresolved">documentation</a>). When an administrator who is logged into Confluence or JIRA attempts to access an administration function, they are prompted to log in again.

All the Atlassian applications will support WebSudo sessions at some point. As of [SAL 2.2](https://developer.atlassian.com/pages/viewpage.action?pageId=5242917) and <a href="/server/framework/atlassian-sdk/rest-plugin-2-2-release-notes" class="createlink">REST 2.2</a> it is possible to enforce WebSudo from within a plugin if the host application supports it.

[More...](/server/framework/atlassian-sdk/adding-websudo-support-to-your-plugin)
