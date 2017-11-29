---
title: How to Speed Up Plugin Startup 8947254
aliases:
    - /server/framework/atlassian-sdk/how-to-speed-up-plugin-startup-8947254.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8947254
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8947254
confluence_id: 8947254
platform:
product:
category:
subcategory:
---
# How to speed up plugin startup

While plugin startup speed may not be a big issue in production, it certainly is during development. The good news is there are a few tricks you can use to drastically improve your plugin startup performance:

{{% note %}}

These tips are aimed at improving the performance of OSGi, or version 2, plugins

{{% /note %}}

### Minimize bundled libraries

If using the SDK, whenever you add a non-provided Maven dependency, that dependency and all its dependencies will be added to your jar. This can cause your plugin to inadvertently bundle things like its own copy of Spring, logging jars, or even the product itself. Not only is this a big cause of plugin startup speed, but it can also fatally affect the operation of your plugin with strange exceptions such as LinkageError's.

To know what libraries are being bundled in your plugin, you can either pay attention to the Maven output, or if dealing with a plugin jar itself, list the contents of the plugin via:

``` java
jar -tf my-plugin.jar
```

Now, look for paths that begin with `META-INF/lib` as these will be the jars that the SDK embedded in your plugin for you. Ideally, you don't want to see any, but if you do, ensure they aren't already provided by the host application or a bundled plugin.

The reason this slows down plugin startup is there are several steps in the plugin startup process that involve scanning all the bytecode of your plugin. Therefore, the more code to scan, the longer it'll take. Also, one of the big bottlenecks during system startup is classloading, so the fewer classes to load, the faster it'll go, not to mention the fewer resources, including the restricted perm gen, it'll take.

### Generate the OSGi manifest at build time

As a convenience feature, the plugin system doesn't require you to generate a complex and verbose OSGi manifest before installing your plugin. However, this convenience comes at a significant cost to startup performance, as it means the plugin system needs to scan the bytecode of every class in the plugin in order to generate the manifest.

As of this writing, the default configuration of the SDK is such that it won't generate a manifest, but will likely change. In the meantime, you can configure the SDK to generate the manifest by providing a non-empty `instructions` element in the configuration. A common configuration would look like this:

``` xml
<instructions>
  <Export-Package />
</instructions>
```

This tells the SDK to generate a manifest, but don't export any packages, which happens to be the default. For advanced developers, you can explicitly define Import-Package entries to ensure your plugin can only be installed when certain packages and versions are available. See OSGi tutorials for more information.

### Bypass host component scanning

Again as a convenience for backward compatibility, the plugin system doesn't require you to import host components explicitly, allowing you to simply reference a host component such as Confluence's `SpaceManager` in the constructor of a bean and it will "magically" be imported and available to your plugin. As expected, this convenience comes at a cost as all bytecode in your plugin has to be scanned on plugin startup.

The output of the host component scanning is a file `META-INF/spring/atlassian-plugins-host-components.xml` that is stored in the transformed version of your plugin upon installation. To bypass the generation of this file (and all other generated Spring files, actually), you can provide your own instance of this file and the processing will be aborted.

First, go through your plugin code and find all referenced host components. These will be beans that come from the host application such as SpaceManager in Confluence or IssueService in JIRA. For each host component, add an explicit `component-import` in your `atlassian-plugin.xml` like this:

``` xml
<component-import key="spaceManager" interface="com.atlassian.confluence.spaces.SpaceManager" />
```

Next, store this XML document as `META-INF/spring/atlassian-plugins-host-components.xml` in your plugin:

``` xml
<?xml version="1.0" encoding="UTF-8"?>

<beans:beans 
        xmlns:beans="http://www.springframework.org/schema/beans" 
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
        xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.5.xsd" />
```

If using the SDK, place this file in `src/main/resources/META-INF/spring/atlassian-plugins-host-components.xml`.

When you install your plugin, if you see any errors about unresolved constructor arguments from Spring, you know you missed a host component component-import.

### Extract bundled libraries

A minor performance improvement you can make that mainly applies to large plugins is to extract bundled jars into your main plugin instead of including them in their original jar form. As mentioned previously, all non-provided Maven dependencies, and their transitive dependencies, will be stored in your jar under the `META-INF/lib` path prefix. On startup, this means that in order for the plugin system to load a class in these embedded jars, it first has to unzip your plugin, then unzip the embedded jar. You can bypass this second step by unzipping the embedded jars into your main jar.

To do this when using the SDK, add this configuration element to your plugin configuration:

``` xml
<extractDependencies>true</extractDependencies>
```

The disadvantage of this technique is it'll be harder to determine later what jars are bundled in your plugin as you'll be lacking the easily listing in `META-INF/lib`.

### Minimize processing in constructors or initialization code

During plugin startup, any long-running code in a constructor or init function will hold up the loading of dependent plugins, not to mention the plugin system as a whole. This includes code that initializes data sources, retrieves content from external hosts, or builds data-extensive caches.

The easiest way to resolve this issue is to simply move the processing to a new thread so that its execution doesn't block plugin startup. However, this may not work as you may need to access system resources that may or may not be available, call other plugin services, or ensure the initialization code has executed before the application is considered up.

To run code when the full application has started, but before it is publicly available, you can use SAL to notify you when the plugin system has started.

1.  Create a class that implements `com.atlassian.sal.api.lifecycle.LifecycleAware`. Put your initialization code in the `onStart()` method, to be called when the application has started, or the plugin is finished loading if the plugin was installed after application start.
2.  Expose your class as a public component:

    ``` xml
    <component key="myStartupCode" class="com.example.MyStartup" public="true"
                   interface="com.atlassian.sal.api.lifecycle.LifecycleAware" />
    ```

























