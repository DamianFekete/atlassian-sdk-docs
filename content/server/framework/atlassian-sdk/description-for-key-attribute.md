---
aliases:
- /server/framework/atlassian-sdk/-description-for-key-attribute-852067.html
- /server/framework/atlassian-sdk/-description-for-key-attribute-852067.md
category: devguide
confluence_id: 852067
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852067
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852067
date: '2017-12-11'
legacy_title: _Description for key attribute
platform: server
product: atlassian-sdk
subcategory: other
title: _Description for key attribute
---
# \_Description for key attribute

The unique identifier of the plugin module. You refer to this key to use the resource from other contexts in your plugin, such as from the plugin Java code or JavaScript resources.

 

    <component-import key="appProps" interface="com.atlassian.sal.api.ApplicationProperties"/>

 

In the example, `appProps` is the key for this particular module declaration, for `component-import`, in this case.

































