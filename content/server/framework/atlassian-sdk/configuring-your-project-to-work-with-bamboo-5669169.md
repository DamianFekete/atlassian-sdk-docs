---
title: Configuring Your Project to Work with Bamboo 5669169
aliases:
    - /server/framework/atlassian-sdk/configuring-your-project-to-work-with-bamboo-5669169.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669169
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669169
confluence_id: 5669169
platform:
product:
category:
subcategory:
---
# Documentation : Configuring your project to work with Bamboo

Configuring your project to work with JIRA is as simple as configuring the `maven-bamboo-plugin` that comes with the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

``` xml
<plugin>
  <groupId>com.atlassian.maven.plugins</groupId>
  <artifactId>maven-bamboo-plugin</artifactId>
  <version>${amps.version}</version>
  <extensions>true</extensions>
  <configuration>
    <pluginArtifacts>
      <pluginArtifact>
        <groupId>com.atlassian.activeobjects</groupId>
        <artifactId>activeobjects-plugin</artifactId>
        <version>${ao.version}</version>
      </pluginArtifact>
      <pluginArtifact>
        <groupId>com.atlassian.activeobjects</groupId>
        <artifactId>activeobjects-bamboo-spi</artifactId>
        <version>${ao.version}</version>
      </pluginArtifact>
    </pluginArtifacts>
    <productVersion>${bamboo.version}</productVersion>
  </configuration>
</plugin>
```

where `amps.version` is the version of the Atlassian Plugin SDK you're using, and `ao.version` the version of the Active Objects plugin you're using. `bamboo.version` is the version of Confluence you want to use.


















































































































































































































































































































