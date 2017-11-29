---
title: Adding the Maven Dependency 5669173
aliases:
    - /server/framework/atlassian-sdk/adding-the-maven-dependency-5669173.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669173
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669173
confluence_id: 5669173
platform:
product:
category:
subcategory:
---
# Adding the maven dependency

You only need to add one dependency to your plugin's `pom.xml` to enable Active Objects:

``` xml
<dependency>
  <groupId>com.atlassian.activeobjects</groupId>
  <artifactId>activeobjects-plugin</artifactId>
  <version>${ao.version}</version>
  <scope>provided</scope>
</dependency>
```

where `ao.version` is the version of Active Objects you're using.  Find a list of all the versions <a href="https://packages.atlassian.com/maven/repository/public/com/atlassian/activeobjects/activeobjects-plugin/" class="external-link">here</a>.

























