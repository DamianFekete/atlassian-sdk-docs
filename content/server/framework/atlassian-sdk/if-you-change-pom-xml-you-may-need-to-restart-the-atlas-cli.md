---
aliases:
- /server/framework/atlassian-sdk/2818364.html
- /server/framework/atlassian-sdk/2818364.md
category: devguide
confluence_id: 2818364
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818364
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818364
date: '2017-12-08'
legacy_title: If you change pom.xml you may need to restart the atlas-cli
platform: server
product: atlassian-sdk
subcategory: faq
title: If you change pom.xml you may need to restart the atlas-cli
---
# If you change pom.xml you may need to restart the atlas-cli

If you are using `atlas-cli` and `pi` for a fast development cycle of your plugin and you get compilation errors about "Unable to run mojo" and no Java line number in your plugin source code, it may be that you changed the dependencies in `pom.xml` but didn't restart `atlas-cli`.
