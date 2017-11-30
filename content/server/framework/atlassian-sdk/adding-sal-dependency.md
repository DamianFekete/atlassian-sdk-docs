---
aliases:
- /server/framework/atlassian-sdk/adding-sal-dependency-5242905.html
- /server/framework/atlassian-sdk/adding-sal-dependency-5242905.md
category: devguide
confluence_id: 5242905
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5242905
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5242905
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/shared-access-layer/adding-sal-dependency
new_url: /server/framework/atlassian-sdk/adding-sal-dependency
platform: server
product: atlassian-sdk
subcategory: learning
title: Adding SAL dependency
---
# Adding SAL dependency

Add this to the `dependencies` section of your pom.xml.

**POM Dependency**

``` xml
<dependency>
    <groupId>com.atlassian.sal</groupId>
    <artifactId>sal-api</artifactId>
    <version>2.0.17</version>
    <scope>provided</scope> <!-- Uses the application's SAL instead of bundling it into the plugin. -->
</dependency>
```

You can find which versions of particular apps and SAL work together in the [SAL Version Matrix](/server/framework/atlassian-sdk/sal-version-matrix).



























































































































































































































