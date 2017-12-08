---
aliases:
- /server/framework/atlassian-sdk/configuring-your-project-5669161.html
- /server/framework/atlassian-sdk/configuring-your-project-5669161.md
category: devguide
confluence_id: 5669161
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669161
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669161
date: '2017-12-08'
guides: guides
legacy_title: Configuring your project
platform: server
product: atlassian-sdk
subcategory: learning
title: Configuring your project
---
# Configuring your project

## Configuring your project to work with Bamboo

Configuring your project to work with JIRA is as simple as configuring the `maven-bamboo-plugin` that comes with the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

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

where `amps.version` is the version of the Atlassian Plugin SDK you're using, and `ao.version` the version of the Active Objects plugin you're using. `bamboo.version` is the version of Confluence you want to use.

## Configuring your project to work with Confluence

Configuring your project to work with Confluence is as simple as configuring the `maven-confluence-plugin` that comes with the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project)

``` xml
<plugin>
  <groupId>com.atlassian.maven.plugins</groupId>
  <artifactId>maven-confluence-plugin</artifactId>
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
        <artifactId>activeobjects-confluence-spi</artifactId>
        <version>${ao.version}</version>
      </pluginArtifact>
    </pluginArtifacts>
    <productVersion>${confluence.version}</productVersion>
  </configuration>
</plugin>
```

where `amps.version` is the version of the Atlassian Plugin SDK you're using, and `ao.version` the version of the Active Objects plugin you're using. `confluence.version` is the version of Confluence you want to use.

## Configuring your project to work with FishEye or Crucible

Configuring your project to work with FishEye/Crucible is as simple as configuring the `maven-fecru-plugin` that comes with the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

``` xml
<plugin>
  <groupId>com.atlassian.maven.plugins</groupId>
  <artifactId>maven-fecru-plugin</artifactId>
  <version>3.4</version>
  <extensions>true</extensions>
  <configuration>
    <productVersion>${fecru.version}</productVersion>
  </configuration>
</plugin>
```

where `amps.version` is the version of the Atlassian Plugin SDK you are using (greater than or equal to 3.4), and `ao.version` the version of the Active Objects plugin you're using (greater than or equal to 0.5.10). `fecru.version` is the version of FishEye/Crucible you are targeting (greater than or equal to 2.7.0-20110906235809).

FishEye/Crucible version 2.7.0 bundles ActiveObjects and is fully supported

## Configuring your project to work with JIRA

Configuring your project to work with JIRA is as simple as configuring the `maven-jira-plugin` that comes with the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project)

``` xml
<plugin>
  <groupId>com.atlassian.maven.plugins</groupId>
  <artifactId>maven-jira-plugin</artifactId>
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
        <artifactId>activeobjects-jira43-spi</artifactId>
        <version>${ao.version}</version>
      </pluginArtifact>
    </pluginArtifacts>
    <productVersion>${jira.version}</productVersion>
  </configuration>
</plugin>
```

where `amps.version` is the version of the Atlassian Plugin SDK you're using, and `ao.version` the version of the Active Objects plugin you're using. `jira.version` is the version of JIRA you want to use.

## Configuring your project to work with the Refapp

Configuring your project to work with the Refapp is as simple as configuring the `maven-refapp-plugin` that comes with the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project). In your `pom.xml` edit your plugin according to the following:

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

where `amps.version`, `refapp.version`, `ao.version` and `refappspi.version` are the versions you want to use.

























































































































































































































































