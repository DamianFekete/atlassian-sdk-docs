---
aliases:
- /server/framework/atlassian-sdk/accessing-classes-from-another-plugin-852151.html
- /server/framework/atlassian-sdk/accessing-classes-from-another-plugin-852151.md
category: devguide
confluence_id: 852151
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852151
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852151
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/plugin-framework-faq/accessing-classes-from-another-plugin
new_url: /server/framework/atlassian-sdk/accessing-classes-from-another-plugin
platform: server
product: atlassian-sdk
subcategory: other
title: Accessing classes from another plugin
---
# Accessing classes from another plugin

If you are building a [dynamic plugin](/server/framework/atlassian-sdk/dynamic-plugin), you can bundle libraries inside your plugin. Place your dependent JARs in the `META-INF/lib` directory (folder) inside the plugin JAR. Any dependency that you specify in your POM will be included in the plugin's `META-INF/lib` directory.

Below is the standard structure of such a JAR, showing the content of plugin's root directory:  
![](/server/framework/atlassian-sdk/images/pluginjarstructure4.png)  
  
And here's the content of the `META-INF/lib` directory:  
![](/server/framework/atlassian-sdk/images/pluginjarstructure3.png)  
  
In the above diagrams:

-   The plugin root directory is `Crowd SAML Plugin`.
-   The plugin descriptor `atlassian-plugin.xml` is at the root level.
-   The classes are located under the `com/atlassian/crowd/plugin/...` directory.
-   The `META-INF/lib` directory contains the dependent JARs.

##### RELATED TOPICS

<a href="/pages/createpage.action?spaceKey=PLUGINFRAMEWORK&amp;title=Troubleshooting+a+LinkageError" class="createlink">Troubleshooting a LinkageError</a>







































