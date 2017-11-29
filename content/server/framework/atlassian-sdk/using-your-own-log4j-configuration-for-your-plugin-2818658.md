---
title: Using Your Own Log4J Configuration for Your Plugin 2818658
aliases:
    - /server/framework/atlassian-sdk/using-your-own-log4j-configuration-for-your-plugin-2818658.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818658
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818658
confluence_id: 2818658
platform:
product:
category:
subcategory:
---
# Documentation : Using your own log4j configuration for your plugin

The <a href="https://maven.atlassian.com/public/com/atlassian/amps/atlassian-plugin-sdk" class="external-link">Atlassian Plugin SDK</a> makes it easy to override the application's `log4j.properties` file, so that you can do custom logging for your plugin.

1.  Create your `log4j.properties` file. A simple way to do this is to copy the application's `log4j.properties` file and change it to suit your needs.
2.  Place the `log4j.properties` file somewhere in your source tree, for example in `src/aps/log4j.properties` ('aps' means the Atlassian Plugin SDK).
3.  Configure your `pom.xml` like this:

    ``` javascript
    <plugin>
      <groupId>com.atlassian.maven.plugins</groupId>
      <artifactId>maven-***-plugin</artifactId> <!-- *** is the name of the application (product) you're using -->
      <version>3.0.4</version>
      <extensions>true</extensions>
      <configuration>
        <productVersion>${product.version}</productVersion>
        <log4jProperties>src/aps/log4j.properties</log4jProperties>
      </configuration>
    </plugin>
    ```

Now you can run your application via `atlas-run` or `atlas-debug`.

{{% note %}}

A plugin specific log4j.properties file does not get picked up using this method once you deploy your plugin to another stand alone server. It only works using `atlas-run` or `atlas-debug`

{{% /note %}}

























