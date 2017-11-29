---
title: Note About Maven Bundled with Sdk 2818464
aliases:
    - /server/framework/atlassian-sdk/-note-about-maven-bundled-with-sdk-2818464.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818464
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818464
confluence_id: 2818464
platform:
product:
category:
subcategory:
---
# Documentation : \_Note about Maven Bundled with SDK

When running Maven commands against your project, make sure that you use the version of Maven bundled with the Atlassian Plugin SDK. This is important if you have a local version of Maven installed, as well as the Atlassian Plugin SDK. The simplest way is to use the [`atlas-mvn`](/server/framework/atlassian-sdk/atlas-mvn-2818341.html) wrapper command instead of `mvn`. Another way is to [put the bundled Maven on your path](/server/framework/atlassian-sdk/verifying-your-maven-settings-2818643.html).

























