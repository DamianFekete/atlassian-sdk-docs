---
aliases:
- /server/framework/atlassian-sdk/-localm2pluginsettings-13632950.html
- /server/framework/atlassian-sdk/-localm2pluginsettings-13632950.md
category: devguide
confluence_id: 13632950
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=13632950
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=13632950
date: '2017-12-08'
legacy_title: _LocalM2PluginSettings
platform: server
product: atlassian-sdk
subcategory: other
title: _LocalM2PluginSettings
---
# \_LocalM2PluginSettings

If you have an existing local `settings.xml` file, you may encounter problems resolving dependencies required by the SDK commands. To prevent these problems, add the following `<pluginRepository>` block to your local `settings.xml` profile:

``` xml
<pluginRepository>
    <id>atlassian-plugin-sdk</id>
    <url>file://${env.ATLAS_HOME}/repository</url>
     <releases>
        <enabled>true</enabled>
        <checksumPolicy>warn</checksumPolicy>
      </releases>
      <snapshots>
         <enabled>false</enabled>
      </snapshots>
 </pluginRepository>
```


































































































































































