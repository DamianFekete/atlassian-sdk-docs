---
aliases:
- /server/framework/atlassian-sdk/-module-definition-example-5669180.html
- /server/framework/atlassian-sdk/-module-definition-example-5669180.md
category: devguide
confluence_id: 5669180
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669180
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669180
date: '2017-12-11'
legacy_title: _Module definition example
platform: server
product: atlassian-sdk
subcategory: other
title: _Module definition example
---
# \_Module definition example

**Module definition example**

``` xml
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
  <plugin-info>
    <description>A basic Active Objects module test</description>
    <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
    <version>1.0</version>
  </plugin-info>

  <ao key="ao-module">
    <description>The AO module for this plugin.</description>
    <entity>com.myapp.MyEntity</entity>
    <upgradeTask>com.myapp.upgrades.v1.Version1UpgradeTask</upgradeTask>
  </ao>
</atlassian-plugin>
```
















