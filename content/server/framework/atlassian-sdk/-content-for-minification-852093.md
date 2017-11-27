---
title: Content for Minification 852093
aliases:
    - /server/framework/atlassian-sdk/-content-for-minification-852093.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852093
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852093
confluence_id: 852093
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Minification

The aim of minification is to remove all unnecessary characters (such as white space) without affecting the functionality.

## How Minification Works

For a given resource, the plugin framework will serve the minified file (`*-min.xxx` or `*.min.xxx`) if present, otherwise it will serve the non-minified file.

For example, take a look at this declaration:

``` javascript
<web-resource key="avataror">
  <dependency>jira.webresources:jira-global</dependency>
  <resource type="download" name="avataror.js" location="/includes/js/avataror.js">
    <param name="source" value="webContextStatic"/>
  </resource>
  <resource type="download" name="avataror.css" location="/styles/avataror.css">
    <param name="source" value="webContextStatic"/>
  </resource>
</web-resource>
```

When the resource named `avataror.js` is requested, the system will check for a file called `avataror-min.js` or `avataror.min.js`. If either of these files exists, it will be served. Otherwise, the plugin framework it will fall back to the old behaviour of streaming the named location file.

## Compressing Files in your Build

There is a Maven 2 plugin that will compress files in your build.

``` javascript
<plugin>
  <groupId>net.sf.alchim</groupId>
  <artifactId>yuicompressor-maven-plugin</artifactId>
  <executions>
    <execution>
      <goals>
        <goal>compress</goal>
      </goals>
    </execution>
  </executions>
  <configuration>
  <!-- Everything on one line -->
    <linebreakpos>-1</linebreakpos>
    <!-- Don't really care about warning messages. They're fairly useless -->
    <jswarn>false</jswarn>
    <excludes>
      <exclude>**/*.xml</exclude>
      <exclude>**/*-min*</exclude>
    </excludes>
  </configuration>
</plugin>
```

## Disabling Minification

You can turn off minification support in your development environments, so that you serve up only non-minified files for debugging purposes:

``` javascript
-Datlassian.webresource.disable.minification=true
```

Minification is automatically disabled in Atlassian developer mode.
















































































































































































































































































































