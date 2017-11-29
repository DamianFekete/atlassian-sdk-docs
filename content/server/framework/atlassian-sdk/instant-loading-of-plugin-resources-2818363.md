---
title: Instant Loading Of Plugin Resources 2818363
aliases:
    - /server/framework/atlassian-sdk/instant-loading-of-plugin-resources-2818363.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818363
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818363
confluence_id: 2818363
platform:
product:
category:
subcategory:
---
# Documentation : Instant Loading of Plugin Resources

During development, one of the main things that can slow you down is reloading the plugin just to see the effect of a change to a static CSS or JavaScript file. To solve this problem during development, you can point the plugin framework at a directory containing your resource files and have the plugin framework load them first before looking in the plugin itself.

To enable this feature, set the system property `plugin.resource.directories` to a comma-delimited list of directories containing plugin resources. For example, to point the framework at your current project's resource directory when running an Atlassian application from Maven, you could set the `MAVEN_OPTS` variable:

``` javascript
export MAVEN_OPTS=-Dplugin.resource.directories=/home/myuser/dev/myplugin/src/main/resources
```

 

 

























