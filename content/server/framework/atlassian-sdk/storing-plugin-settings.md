---
aliases:
- /server/framework/atlassian-sdk/storing-plugin-settings-18251950.html
- /server/framework/atlassian-sdk/storing-plugin-settings-18251950.md
category: devguide
confluence_id: 18251950
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=18251950
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=18251950
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/storing-plugin-settings
new_url: /server/framework/atlassian-sdk/storing-plugin-settings
platform: server
product: atlassian-sdk
subcategory: learning
title: Storing plugin settings
---
# Storing plugin settings

Plugin settings are part of the Shared Access Layer (SAL) component of the Atlassian plugin framework. Plugin settings provide a cross-product mechanism for persisting values relied upon by plugins.

`PluginSettings` objects are created with a `PluginSettingsFactory`, like this:

``` java
PluginSettings pluginSettings = pluginSettingsFactory.createGlobalSettings(); 
```

The `PluginSettingsFactory` interface includes the `createGlobalSettings()` method, which returns a `PluginSettings` object, as shown in the example.

Behind the scenes, settings are stored in a product-specific way. In a Confluence plugin, the `pluginSettingsFactory` will be a `ConfluencePluginSettingsFactory` and `createGlobalSettings()` will return a `ConfluencePluginSettings` object.

The `ConfluencePluginSettings` object uses [Bandana](https://developer.atlassian.com/display/CONFDEV/Persistence+in+Confluence) internally to store the plugin settings. For a JIRA plugin, the `JiraPluginSettingsFactory` returns `JiraPluginSettings` objects that use <a href="https://confluence.atlassian.com/display/JIRA043/JIRA+Architectural+Overview#JIRAArchitecturalOverview-PropertySet" class="external-link">PropertySets</a> to store the settings.

Here is a diagram of SAL's plugin settings objects:

<img src="http://atlassian.wpengine.netdna-cdn.com/developer/gliffy_factory_pattern.jpg" alt="gliffy_factory_pattern.jpg" class="confluence-external-resource mt-image-none" width="598" height="317" />

The `PluginSettingsFactory` uses the <a href="http://en.wikipedia.org/wiki/Abstract_factory_pattern" class="external-link">abstract factory pattern</a>: it "provides an interface for creating families of related or dependent objects without specifying their concrete classes" (p. 87 in *Design Patterns* by Gamma et al).

The `PluginSettingsFactory` allows us to create specific `PluginSettings` objects for Confluence, JIRA, and other products depending on what type of `PluginSettingsFactory` (e.g. `ConfluencePluginSettingsFactory`) is in use, which depends on what product a plugin is for.

Plugin developers benefit from the use of the abstract factory pattern here in several ways. No matter what the target product for a plugin, one syntax can be used to interact with plugin settings. So it is not necessary for developers to learn and remember multiple, distinct settings storage syntax for different products. And a particular plugin could potentially have multiple target products without special handling, at least as far as plugin settings are concerned.

These are benefits often seen when using factories for object creation: users of the object are insulated from the specific objects used and their implementations, and maintenance changes only need to occur in one location rather than in each client.








































































































































































































