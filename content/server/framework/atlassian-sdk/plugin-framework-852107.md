---
aliases:
- /server/framework/atlassian-sdk/plugin-framework-852107.html
- /server/framework/atlassian-sdk/plugin-framework-852107.md
category: devguide
confluence_id: 852107
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852107
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852107
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/plugin-framework
new_url: /server/framework/atlassian-sdk/plugin-framework
platform: server
product: atlassian-sdk
subcategory: learning
title: Plugin Framework
---
# Plugin Framework

## Getting Started

Get started by [setting up your Atlassian plugin development environment](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

With Atlassian's plugin development platform, you can create plugins that extend the functionality of Atlassian applications such as <a href="http://www.atlassian.com/software/jira/" class="external-link">JIRA</a>, <a href="http://www.atlassian.com/software/confluence/" class="external-link">Confluence</a> and <a href="http://www.atlassian.com" class="external-link">others</a>.

The platform consists of a plugin framework and set of components that provide useful tools to plugin developers. To see how the pieces fit together, take a look at the [overview of the platform](/server/framework/atlassian-sdk/atlassian-platform-common-components). To get started writing plugins, download and set up the Atlassian Plugin SDK. Then follow the plugin development guidelines for your specific application, as listed [below](#below).

If you need detailed information about the plugin framework itself, read the details [below](#below).

## Plugin Framework in Detail

### Atlassian Plugin Framework

The plugin framework supports several types of plugins, including OSGi-based plugins. <a href="http://www.osgi.org/" class="external-link">OSGi</a> is a dynamic module system for Java that the framework uses to enable plugins to depend on each other and more easily share services. Because the plugin framework supports multiple versions of plugins simultaneously, legacy plugins or those built into the application can exist side-by-side with newer dynamic plugins that leverage the plugin-sharing benefits of OSGi.

### Plugin Descriptor

See how to [define your plugin via an XML file](/server/framework/atlassian-sdk/configuring-the-plugin-descriptor), the 'plugin descriptor'.

### OSGi, Spring and the Plugin Framework\*

Read the in-depth information about [how we use OSGi](/server/framework/atlassian-sdk/852146.html) in the Atlassian Plugin Framework.

\*Embedding the Plugin Framework  
Find out how to [transform your web application](/server/framework/atlassian-sdk/embedding-the-plugin-framework) into a platform that can be extended at runtime via plugins.

 

## Resources

[Atlassian Platform Common Components](/server/framework/atlassian-sdk/atlassian-platform-common-components)

[Application Version Matrix](/server/framework/atlassian-sdk/plugin-framework-version-matrix)

<a href="http://docs.atlassian.com/" class="external-link">Javadoc</a>

<a href="http://plugins.atlassian.com/" class="external-link">Plugin Exchange</a>

<a href="https://bitbucket.org/atlassian/atlassian-plugins" class="external-link">Source code</a>

<a href="http://maven.atlassian.com/public/com/atlassian/plugins/" class="external-link">Binaries</a>

### Help

[Plugin Framework FAQ](/server/framework/atlassian-sdk/plugin-framework-faq-852039.html)

<a href="https://answers.atlassian.com/" class="external-link">Answers from the community</a>

<a href="https://studio.atlassian.com/browse/PLUG" class="external-link">Feature requests and bug reports</a>

<a href="http://my.atlassian.com/" class="external-link">Mailing lists at my.atlassian.com</a>

 

## Plugin Modules

#### [Plugin Module Index](/server/framework/atlassian-sdk/plugin-module-index)

#### [Component Import Plugin Module](/server/framework/atlassian-sdk/component-import-plugin-module)

#### [Component Plugin Module](/server/framework/atlassian-sdk/component-plugin-module)

#### [Module Type Plugin Module](/server/framework/atlassian-sdk/module-type-plugin-module)

#### [Servlet Context Listener Plugin Module](/server/framework/atlassian-sdk/servlet-context-listener-plugin-module)

#### [Servlet Context Parameter Plugin Module](/server/framework/atlassian-sdk/servlet-context-parameter-plugin-module)

#### [Servlet Filter Plugin Module](/server/framework/atlassian-sdk/servlet-filter-plugin-module)

#### [Servlet Plugin Module](/server/framework/atlassian-sdk/servlet-plugin-module)

#### [Template Context Item Plugin Module](/server/framework/atlassian-sdk/template-context-item-plugin-module)

#### [Web Item Plugin Module](/server/framework/atlassian-sdk/web-item-plugin-module)

#### [Web Panel Plugin Module](/server/framework/atlassian-sdk/web-panel-plugin-module)

#### [Web Panel Renderer Plugin Module](/server/framework/atlassian-sdk/web-panel-renderer-plugin-module)

#### [Web Resource Plugin Module](/server/framework/atlassian-sdk/web-resource-plugin-module)

#### [Web Resource Transformer Plugin Module](/server/framework/atlassian-sdk/web-resource-transformer-plugin-module)

#### [Web Section Plugin Module](/server/framework/atlassian-sdk/web-section-plugin-module)





































































































































































































