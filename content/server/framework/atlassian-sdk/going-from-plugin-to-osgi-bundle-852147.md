---
aliases:
- /server/framework/atlassian-sdk/going-from-plugin-to-osgi-bundle-852147.html
- /server/framework/atlassian-sdk/going-from-plugin-to-osgi-bundle-852147.md
category: devguide
confluence_id: 852147
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852147
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852147
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/plugin-framework/behind-the-scenes-in-the-plugin-framework/going-from-plugin-to-osgi-bundle
new_url: /server/framework/atlassian-sdk/going-from-plugin-to-osgi-bundle
platform: server
product: atlassian-sdk
subcategory: learning
title: Going from Plugin to OSGi bundle
---
# Going from Plugin to OSGi bundle

The plugin framework supports multiple types of plugins ranging from built-in plugins that are little more than an XML file to fully-fledged OSGi-based plugins.

For version 2 plugins that are deployed into the internal OSGi container, as a plugin author you can ignore all the OSGi trappings and just provide a JAR containing the `atlassian-plugin.xml` descriptor file.

The Atlassian Plugin Framework 2 tries to hide the complexity of OSGi as much as possible, especially for simple plugins that do not have dependencies on other plugins. However, since version 2 plugins will be deployed on OSGi, they need to be transformed into an OSGi bundle that the OSGi container understands. The Atlassian Plugin Framework has a built-in way of transforming plugin JARs into fully-fledged OSGi bundles.

INFO: If you are familiar with OSGi and want to provide an OSGi bundle directly in order to leverage all its features, you are free to do so.

## Converting a Plugin into an OSGi Bundle

The following diagram describes the process by which a plugin JAR is dynamically loaded and, at the end of the process flow, transformed into an OSGi bundle.

![](/server/framework/atlassian-sdk/images/pluginosgiworkflow-50pc.png)

##### RELATED TOPICS

\[[Managing Dependencies](/server/framework/atlassian-sdk/managing-dependencies)\]  
[Automatic Generation of Spring Configuration](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Automatic+Generation+of+Spring+Configuration)  
[Plugin Framework](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Plugin+Framework)

































































































































































































