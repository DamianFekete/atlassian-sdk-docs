---
aliases:
- /server/framework/atlassian-sdk/quick-start-guide-to-embedding-851992.html
- /server/framework/atlassian-sdk/quick-start-guide-to-embedding-851992.md
category: devguide
confluence_id: 851992
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851992
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851992
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/plugin-framework/embedding-the-plugin-framework/quick-start-guide-to-embedding
new_url: /server/framework/atlassian-sdk/quick-start-guide-to-embedding
platform: server
product: atlassian-sdk
subcategory: learning
title: Quick start guide to embedding
---
# Quick start guide to embedding

If you want to get the plugin framework into your application with little fuss, this is the guide for you.

Before you start, ensure your application requires recent versions of Java 5 or Java 6.

## Step 1: Add the Framework and Dependency JARs to your Webapp

If you already use Maven 2, the easiest way to add the Atlassian Plugins JAR files to your build is to add this dependency:

``` xml
<dependency>
  <groupId>com.atlassian.plugins</groupId>
  <artifactId>atlassian-plugins-main</artifactId>
  <version>RELEASE</version>
</dependency>
```

In your dependency declaration, replace RELEASE with the latest version.

Alternatively, you can add the individual JAR files, paying attention to their dependencies as defined in their pom.xml. At a minimum, you will want these jars:

-   atlassian-plugins-core-VERSION.jar
-   atlassian-plugins-main-VERSION.jar

You can find them in the Maven repository: <a href="http://maven.atlassian.com/public/com/atlassian/plugins" class="uri external-link">http://maven.atlassian.com/public/com/atlassian/plugins</a>

## Step 2: Start the Plugin Framework during Application Initialisation

The primary class to configure and use to manage the plugin framework is `com.atlassian.plugin.main.AtlassianPlugins`. This is an example of how to construct and start an instance of it:

``` java
// Determine which packages to expose to plugins
PackageScannerConfiguration scannerConfig = new DefaultPackageScannerConfiguration();
scannerConfig.setServletContext(servletContext);
scannerConfig.getPackageIncludes().add("com.example*");

// Determine which module descriptors, or extension points, to expose.
// This 'on-start' module is used throughout this guide as an example only
DefaultModuleDescriptorFactory modules = new DefaultModuleDescriptorFactory(new DefaultHostContainer());
modules.addModuleDescriptor("on-start", OnStartModuleDescriptor.class);

// Determine which service objects to expose to plugins
HostComponentProvider host = new HostComponentProvider() {
    public void provide(ComponentRegistrar reg)
    {
        reg.register(MyServiceInterface.class).forInstance(
            myServiceInstance);
    }
};

// Construct the configuration
PluginsConfiguration config = new PluginsConfigurationBuilder()
        .pluginDirectory(new File("plugins"))
        .packageScannerConfiguration(scannerConfig)
        .hotDeployPollingFrequency(2, TimeUnit.SECONDS)
        .hostComponentProvider(host)
        .moduleDescriptorFactory(modules)
        .build();

// Start the plugin framework
AtlassianPlugins plugins = new AtlassianPlugins(config);
plugins.start();
```

`MyServiceInterface` and `myServiceInstance` could be any interface and implementation, respectively, that you want to share with plugins. The only requirement is any object instances you share must have an interface.

## Step 3: Add a New Module Descriptor

Plugin modules are the extension points your application exposes to plugins. The module descriptors are how a plugin tells the framework that it implements one of those extension points.

Here is a simple module descriptor that allows a plugin to define code that will be ran on startup:

``` java
public class OnStartModuleDescriptor extends AbstractModuleDescriptor<Runnable>
{
    public Runnable getModule()
    {
        return ((AutowireCapablePlugin)getPlugin()).autowire(getModuleClass());
    }
}
```

Next, your application needs to use this extension point. In our example, we would need to add this code to at the end of our application intialisation code:

``` java
for (Runnable runnable :  plugins.getPluginAccessor().getEnabledModulesByClass(Runnable.class))
{
    runnable.run();
}
```

## Step 4: Write a Simple Test Plugin

Finally, we need to write a simple plugin to ensure everything is working correctly. A plugin generally is composed of Java code and a single `atlassian-plugin.xml` descriptor file sitting at the root of the jar. Since it is a jar, ensure that it has a valid manifest.

To test the 'on-start' plugin module type described in this guide, let's write a 'himom-plugin' that will print "Hi Mom!" on startup. This plugin will consist of a Runnable class that does the work and a plugin descriptor for configuration:

#### HiMomRunnable.java

``` java
public class HiMomRunnable implements Runnable
{
    public void run()
    {
        System.out.println("Hi Mom!");
    }
}
```

#### atlassian-plugin.xml

``` java
<atlassian-plugin key="himom-plugin" name="Hi Mom" plugins-version="2">
    <plugin-info>
        <version>1.0.0</version>
    </plugin-info>
    <on-start key="himom"
            class="com.example.himom.HiMomRunnable" />
</atlassian-plugin>
```

To deploy this plugin, we can drop it into the "plugins" directory we configured in step 2 and the plugin framework should find it within 2 seconds and install the plugin automatically.


























































































































































































































































