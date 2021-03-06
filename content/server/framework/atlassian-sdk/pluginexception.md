---
aliases:
- /server/framework/atlassian-sdk/pluginexception-2818384.html
- /server/framework/atlassian-sdk/pluginexception-2818384.md
category: devguide
confluence_id: 2818384
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818384
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818384
date: '2017-12-08'
legacy_title: PluginException
platform: server
product: atlassian-sdk
subcategory: faq
title: PluginException
---
# PluginException

#### Symptom: "PluginException: Unable to instantiate class"

**Cause**: No Java class file referring to the class exists, so the automatic scanner for injection didn't know it needed to make the class importable

**Solution**: Explicitly add `<component-import>` elements or create a subclass with a delegating constructor

**Example**:

<a href="http://confluence.atlassian.com/display/DOCSPRINT/Plugin+Tutorial+-+Create+a+New+JIRA+Custom+Field+Type" class="external-link">Create a New JIRA Custom Field Type</a>

See also  <a href="https://ecosystem.atlassian.net/browse/PLUG-535?src=confmacro" class="jira-issue-key"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&avatarId=15303&avatarType=issuetype" class="icon" />PLUG-535</a> - Create explicit imports for host components Resolved
