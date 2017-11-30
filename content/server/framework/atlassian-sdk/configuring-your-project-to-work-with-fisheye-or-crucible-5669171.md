---
title: Configuring Your Project to Work with Fisheye Or Crucible 5669171
aliases:
    - /server/framework/atlassian-sdk/configuring-your-project-to-work-with-fisheye-or-crucible-5669171.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669171
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669171
confluence_id: 5669171
platform:
product:
category:
subcategory:
---
# Documentation : Configuring your project to work with FishEye or Crucible

Configuring your project to work with FishEye/Crucible is as simple as configuring the `maven-fecru-plugin` that comes with the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

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

where `amps.version` is the version of the Atlassian Plugin SDK you are using (greater than or equal to 3.4), and `ao.version` the version of the Active Objects plugin you're using (greater than or equal to 0.5.10). `fecru.version` is the version of FishEye/Crucible you are targeting (greater than or equal to 2.7.0-20110906235809).

FishEye/Crucible version 2.7.0 bundles ActiveObjects and is fully supported





















































































































































































































































