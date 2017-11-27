---
aliases:
- /server/framework/atlassian-sdk/maven-runs-out-of-memory-2818367.html
- /server/framework/atlassian-sdk/maven-runs-out-of-memory-2818367.md
category: devguide
confluence_id: 2818367
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818367
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818367
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/atlassian-plugin-sdk-faq/maven-runs-out-of-memory
new_url: /server/framework/atlassian-sdk/maven-runs-out-of-memory
platform: server
product: atlassian-sdk
subcategory: other
title: Maven runs out of memory
---
# Maven runs out of memory

You may need to allocate more memory to Maven in order to complete your build. You can do so by setting an environment variable called `MAVEN_OPTS`. For example:

``` javascript
export MAVEN_OPTS=-Xmx512m
```













































