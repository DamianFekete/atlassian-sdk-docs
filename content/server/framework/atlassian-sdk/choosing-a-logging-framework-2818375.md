---
title: Choosing a Logging Framework 2818375
aliases:
    - /server/framework/atlassian-sdk/choosing-a-logging-framework-2818375.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818375
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818375
confluence_id: 2818375
platform:
product:
category:
subcategory:
---
# Documentation : Choosing a Logging Framework

Three logging frameworks are available to plugins:

-   Log4j 1.2.15
-   Commons Logging 1.1.1
-   SLF4J 1.5

We recommend Simple Logging Facade for Java (<a href="http://www.slf4j.org/" class="external-link">SLF4J</a>) as a the primary logging framework.

You should ensure that none of these libraries are bundled with your plugin (in `META-INF/lib`) as this will prevent the host application from logging any of your plugin's log messages.

You can check your plugin's dependencies by using <a href="http://maven.apache.org/plugins/maven-dependency-plugin/tree-mojo.html" class="external-link"><code>mvn dependency:tree</code></a> and then exclude any transitive dependencies in the `pom.xml`:

``` javascript
<exclusions>
   <exclusion>
     <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
  </exclusion>
  <exclusion>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-log4j12</artifactId>
  </exclusion>
</exclusions>
```
