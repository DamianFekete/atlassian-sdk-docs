---
aliases:
- /server/framework/atlassian-sdk/852046.html
- /server/framework/atlassian-sdk/852046.md
category: devguide
confluence_id: 852046
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852046
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852046
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/converting-from-version-1-to-version-2-osgi-plugins
new_url: /server/framework/atlassian-sdk/converting-from-version-1-to-version-2-osgi-plugins
platform: server
product: atlassian-sdk
subcategory: learning
title: Converting from Version 1 to Version 2 (OSGi) Plugins
---
# Converting from Version 1 to Version 2 (OSGi) Plugins

This page contains guidelines on migrating an existing version 1 plugin to the Atlassian Plugin Framework 2. Version 2 and later of the plugin framework is based on <a href="http://en.wikipedia.org/wiki/OSGi" class="external-link">OSGi</a> and Spring Dynamic Modules. The plugin framework has all the advantages of OSGi, plus it will be included into all Atlassian applications. This means that writing plugins for different applications will be more consistent.

Plugins that were written for the old framework will continue to work, but to leverage the new functionality you will need to convert your plugin to the new framework. This page describes how to migrate an existing plugin to the new plugin framework.

 

## Prerequisites

First upgrade the host application to a version which supports version 2 of the plugin framework. For example, upgrade to Confluence 2.10 or later, or JIRA 4.0 or later. See the [Plugin Framework Version Matrix](/server/framework/atlassian-sdk/plugin-framework-version-matrix).

## Summary of How to Convert your Plugin

Summary of the steps required to convert your plugin:

1.  Add the `plugins-version="2"` attribute in `atlassian-plugin.xml`:

    ``` xml
    <atlassian-plugin name="plugin name" key="plugin key" enabled="true" plugins-version="2">
    ```

2.  Check that packages used by your plugin are available to OSGi plugins. 
3.  Check that components used by your plugin are available to OSGi plugins. See [OSGi, Spring and the Plugin Framework](/server/framework/atlassian-sdk/852146.html) for more information.

The plugin framework handles all the OSGi requirements, such as bundle instructions, manifest, etc. See [Going from Plugin to OSGi Bundle](/server/framework/atlassian-sdk/going-from-plugin-to-osgi-bundle). For more complex plugins, you may find it useful to do more complex configuration, such as supplying complete Spring configuration files.

## Details of How to Convert your Plugin

### 1. Set your plugin 'plugins-version' flag to version 2

As described in the [documentation](/server/framework/atlassian-sdk/atlassian-platform-common-components) there are two types of plugins in the Atlassian Plugin Framework 2:

> -   **Version 1** -- These may be static (deployed in `WEB-INF/lib`) or dynamic (via the web UI, only in Confluence) and should work the same as they did in version 1 of the Atlassian Plugin Framework. The capabilities and features available to version 1 plugins vary significantly across products.
> -   **Version 2** -- These plugins are dynamically deployed on an internal <a href="http://osgi.org" class="external-link">OSGi</a> container to provide a consistent set of features and behaviours, regardless of the application the plugin is running on. Version 2 plugins have to be specifically declared as such, using the `plugins-version="2"` attribute in `atlassian-plugin.xml`.

So the first step of migration is to make your plugin a *Version 2* plugin by setting `plugins-version="2"` attribute in `atlassian-plugin.xml`:

``` xml
<atlassian-plugin name="plugin name" key="plugin key" enabled="true" plugins-version="2">
```

For the remainder of this document, please consider the following terms synonymous (they mean the same thing): *Version 2 plugin* and *OSGi plugin*.

### 2. Check that packages used by your plugin are available to OSGi plugins

OSGi plugins - plugins with 'plugins-version' set to 2 - are subject to certain restrictions. In particular, an OSGi plugin can access only those external classes that the host application (or other plugins) explicitly exposes. This means that you can no longer assume that all classes on the application's classpath will be accessible to your plugin.

Refer to the list of packages that your host application exposes, and ensure that all classes used by your plugin are covered by this list. Inside the application, this list is configured as a parameter to the `packageScanningConfiguration` component in the `pluginServiceContext.xml` file.

-   [List of packages that Confluence exposes](https://developer.atlassian.com/display/CONFDEV/Packages+available+to+OSGi+plugins)
-   [Using the OSGi Browser](/server/framework/atlassian-sdk/using-the-osgi-browser) to determine the packages and components exposed by an application.

It is very important to ensure that plugin code does not depend on packages that are not exposed, as the problem will only manifest itself during runtime.

#### 2.1 Rely on automatic package imports

With the plugin framework, the required packages are imported transparently for OSGi plugins. You do not need to do anything to have required packages imported, but it may help to understand how this works.

Normally, an <a href="http://en.wikipedia.org/wiki/OSGi" class="external-link">OSGi</a> bundle needs to explicitly import all packages it needs. To work around this requirement, the plugin framework generates the list of required packages by scanning the class files inside your plugin and determining which packages they use. Once this list of packages is determined, the plugin system generates an OSGi manifest and inserts it into your plugin prior to loading it into the OSGi container. For more information, refer to [OSGi Basics](/server/framework/atlassian-sdk/852146.html) and [how OSGI bundles are generated](/server/framework/atlassian-sdk/going-from-plugin-to-osgi-bundle).

#### 2.2 Customise package imports and exports with a bundle manifest

If you want to have a full control over what packages are imported by your plugin, you can package the plugin as an OSGi bundle. To do this, you need to specify all necessary entries in a manifest file inside your plugin JAR file. Using the <a href="http://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html" class="external-link">Bundle Plugin for Maven</a> makes the process of generating a valid OSGi manifest much simpler.

You might also want to configure a bundle manifest yourself if you want expose a set of packages as being exported from your plugin.

See [Managing Dependencies](/server/framework/atlassian-sdk/managing-dependencies).

### 3. Check that components used by your plugin are available to OSGi plugins

The other important restriction for OSGi plugins is that they are only allowed to access those Spring components that are explicitly exposed by the host application or by other plugins.

-   In Confluence, you can find the list of all components that are available to OSGi plugins under `http://<baseURL>/admin/pluginexports.action`. In this list, each Spring component is listed against the interfaces that it provides. In OSGi, every component must specify the interfaces it provides.
-   [Using the OSGi Browser](/server/framework/atlassian-sdk/using-the-osgi-browser) to determine the packages and components exposed by an application.

As with the exposed packages, the list of exposed components attempts to cover all the host application functionality but not to expose all the internals of the application. If your plugin uses the beans that are not exposed you should be able to find an exposed bean that provides the same functionality. As with the packages, this list is intentionally limited to try to improve plugin compatibility across releases of the host application.

It is very important to ensure that plugin code does not depend on beans that are not exposed, as the problem will only manifest itself during runtime. The easiest way to ensure that there are no dependencies on beans which are not exposed is to use constructor injection. Using constructor injection will ensure that the plugin fails during the loading if any of the dependencies are not satisfied.

#### 3.1 Specify qualifiers on ambiguous Spring dependencies

In some cases, the host application exposes more than one bean under the same interface. When this happens, <a href="http://www.springframework.org" class="external-link">Spring</a> can't determine exactly which bean to use to satisfy a dependency on that interface. For example, there may be two exposed beans that implement the PluginController interface. Spring will fail to inject the right dependency unless you provide a <a href="http://www.springframework.org" class="external-link">Spring</a> *@Qualifier* annotation.

The most common example is in Confluence:

``` java
// Confluence has two beans that implement PluginController, so we add a qualifier to specify which one we want
public void setPluginController(@Qualifier("pluginController") PluginController pluginController)
{
this.pluginController = pluginController;
}
```

#### 3.2 Expose your plugin components to other plugins

In order to make a component in your plugin available to other plugins you can simply add the `public="true"` attribute to the component in your plugin descriptor file. You will need to specify one or more interfaces under which this bean will be exposed.

``` xml
<component key="pluginScheduler" class="com.atlassian.sal.core.scheduling.TimerPluginScheduler" public="true" > 
<interface>com.atlassian.sal.api.scheduling.PluginScheduler</interface> 
</component>
```

#### 3.3 Import components exposed by other plugins

Components that are exposed by other plugins are treated a little differently to beans that are exposed by the host application. Your plugin needs to specifically import components which come from other plugins. To do this, include a `<component-import>` tag inside your `atlassian-plugin.xml` file.

``` xml
<component-import key="loc" interface="com.atlassian.sal.api.license.LicenseHandler" />
```

You will also need to ensure that the component [class is imported](#class-is-imported), which [usually happens transparently](#usually-happens-transparently).

### 4. Advanced configuration with Spring configuration files

The new plugin framework provides the ability to create plugin components using complete Spring configuration files. If you provide Spring Dynamic Modules (Spring DM) configuration files in `META-INF/spring/`, these will be loaded into your plugin OSGi bundle by the Spring DM loader. Using this option for configuration provides you with a lot of flexibility about how your plugin components are created and managed.

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns:beans="http://www.springframework.org/schema/beans"
  xmlns:osgi="http://www.springframework.org/schema/osgi"
  xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
  xsi:schemaLocation="
    http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
    http://www.springframework.org/schema/osgi http://www.springframework.org/schema/osgi/spring-osgi.xsd"
  default-autowire="autodetect">

  <beans:bean id="repositoryManager" class="com.atlassian.plugin.repository.logic.ConfluenceRepositoryManager"/>
  ...
</beans:beans>
```

To include a Spring configuration file, ensure it is included in the `META-INF/spring/` directory inside your plugin JAR file. All files matching `*.xml` inside this directory will be loaded as Spring configuration files when your plugin is loaded. For more details on Spring configuration, see the <a href="http://www.springframework.org" class="external-link">Spring documentation</a>.

## Notes

-   Confluence API limitations - See the [Confluence developer documentation: Converting a Plugin to Plugin Framework 2](https://developer.atlassian.com/display/CONFDEV/Converting+a+Plugin+to+Plugin+Framework+2).

## Useful External Guides

-   Video of a presentation from Atlassian Summit 2010, by John Kodumal of Atlassian: <a href="https://www.youtube.com/watch?v=uT9eMc5w0nQ" class="external-link">YouTube: Plugins 2.0 &amp; OSGi Gotchas</a>.

    > Migrating to Plugins 2.0 is easier than you think, especially when you know what to expect. We'll arm you with the info you need to move to Plugins 2.0.

##### RELATED TOPICS

[Managing Dependencies](/server/framework/atlassian-sdk/managing-dependencies)  
[OSGi, Spring and the Plugin Framework](/server/framework/atlassian-sdk/852146.html)  
[Common Coding Tasks](/server/framework/atlassian-sdk/common-coding-tasks)  
[Confluence Developer Documentation: Converting a Plugin to Plugin Framework 2](https://developer.atlassian.com/display/CONFDEV/Converting+a+Plugin+to+Plugin+Framework+2)

























































































