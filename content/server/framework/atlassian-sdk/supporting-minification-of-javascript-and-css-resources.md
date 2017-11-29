---
aliases:
- /server/framework/atlassian-sdk/supporting-minification-of-javascript-and-css-resources-852081.html
- /server/framework/atlassian-sdk/supporting-minification-of-javascript-and-css-resources-852081.md
category: devguide
confluence_id: 852081
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852081
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852081
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/supporting-minification-of-javascript-and-css-resources
new_url: /server/framework/atlassian-sdk/supporting-minification-of-javascript-and-css-resources
platform: server
product: atlassian-sdk
subcategory: learning
title: Supporting minification of JavaScript and CSS resources
---
# Supporting minification of JavaScript and CSS resources

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p>Atlassian Plugin Framework 2.3 and later.</p></td>
</tr>
</tbody>
</table>

 

The Atlassian Plugin Framework supports <a href="http://en.wikipedia.org/wiki/Minification_%28programming%29" class="external-link">minification</a> when serving JavaScript and CSS resources.

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








































































































