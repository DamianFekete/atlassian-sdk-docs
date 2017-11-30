---
title: Configuring Your Project to Work with the Refapp 5669163
aliases:
    - /server/framework/atlassian-sdk/configuring-your-project-to-work-with-the-refapp-5669163.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669163
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669163
confluence_id: 5669163
platform:
product:
category:
subcategory:
---
# Documentation : Configuring your project to work with the Refapp

Configuring your project to work with the Refapp is as simple as configuring the `maven-refapp-plugin` that comes with the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project). In your `pom.xml` edit your plugin according to the following:

``` xml
<plugin>
  <groupId>com.atlassian.maven.plugins</groupId>
  <artifactId>maven-refapp-plugin</artifactId>
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
        <artifactId>activeobjects-refapp-spi</artifactId>
        <version>${refappspi.version}</version>
      </pluginArtifact>
    </pluginArtifacts>
    <productVersion>${refapp.version}</productVersion>
  </configuration>
</plugin>
```

where `amps.version`, `refapp.version`, `ao.version` and `refappspi.version` are the versions you want to use.


















































































































































































































































































































