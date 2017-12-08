---
aliases:
- /server/framework/atlassian-sdk/maven-runs-out-of-memory-2818367.html
- /server/framework/atlassian-sdk/maven-runs-out-of-memory-2818367.md
category: devguide
confluence_id: 2818367
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818367
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818367
date: '2017-12-08'
legacy_title: Maven Runs Out of Memory
platform: server
product: atlassian-sdk
subcategory: faq
title: Maven runs out of memory
---
# Maven runs out of memory

You may need to allocate more memory to Maven in order to complete your build. You can do so by setting an environment variable called `MAVEN_OPTS`. For example:

``` bash
export MAVEN_OPTS=-Xmx512m
```


























































































