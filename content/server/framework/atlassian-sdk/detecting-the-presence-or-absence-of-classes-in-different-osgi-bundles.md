---
aliases:
- /server/framework/atlassian-sdk/detecting-the-presence-or-absence-of-classes-in-different-osgi-bundles-2818636.html
- /server/framework/atlassian-sdk/detecting-the-presence-or-absence-of-classes-in-different-osgi-bundles-2818636.md
category: devguide
confluence_id: 2818636
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818636
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818636
date: '2017-12-08'
legacy_title: Detecting the Presence or Absence of Classes in Different OSGI Bundles
platform: server
product: atlassian-sdk
subcategory: faq
title: Detecting the presence or absence of classes in different OSGI bundles
---
# Detecting the presence or absence of classes in different OSGI bundles

{{% warning %}}

Problems have been found with this approach and it is not recommended. We are currently working on a better solution.

{{% /warning %}}{{% note %}}

This page is about 'Plugins 2' plugins, i.e. plugins written for version 2 of the Atlassian Plugin Framework. The procedure below will not work with plugins written against version 1 of the plugin framework.

{{% /note %}}

Occasionally you will need to write a plugin that behaves differently depending on the presence or absence of another plugin. An example where we at Atlassian confront this problem is with the [AppLinks](https://developer.atlassian.com/display/APPLINKS) plugin: if the AppLinks plugin is available, we want to use it to auto-detect known servers and connect to them automatically, but we still want our plugin to behave normally if AppLinks is not present.

There are a few ways to detect whether a specific plugin is present in your host application or not. On this page, we will show you how to add a **listener** to track when the availability of that plugin changes.

To start with, there is a bit of housekeeping. Add a dependency on spring-extender in your `pom.xml`:

``` xml
<dependency>
  <groupId>org.springframework.osgi</groupId>
  <artifactId>spring-osgi-extender</artifactId>
  <version>1.2.0</version>
  <scope>provided</scope> <!-- Provided by application -->
</dependency>
```

Add a DynamicImport-Package element to the plugin-info element in `atlassian-plugin.xml`:

``` xml
<plugin-info>
...
  <bundle-instructions>
    ...
    <DynamicImport-Package>com.example.plugin.package*;version="1.2.3",com.example.another.plugins.package*;version="3.1.4"</DynamicImport-Package>
    <!-- packages are separated by commas (,) and package information is separated by semicolons (;) -->
  </bundle-instructions>
</plugin-info>
```

Wire up the class you will use, in `atlassan-plugin.xml`:

``` xml
<component key="exampleKey" name="Example Name" class="com.example.somepackage.ExampleClass">
  <interface>com.example.somepackage.ExampleInterface</interface>
</component>
    
```

Now to the meat of it all. The class should implement BundleContextAware and DisposableBean as follows:

**ExampleClass.java**

``` java
package com.example.somepackage;

import org.springframework.osgi.context.BundleContextAware;
import org.springframework.beans.factory.DisposableBean;

public class ExampleClass implements ExampleInterface, BundleContextAware, DisposableBean
{
        private ServiceTracker tracker = null;
    private boolean exampleIsPresent = false;
    public boolean isExamplePresent() { return exampleIsPresent; }

    /**
     * Set the {@link BundleContext} that this bean runs in. Normally this can
     * be used to initialize an object.
     * 
     * @param bundleContext the <code>BundleContext</code> object to be used
     * by this object
     */
    public void setBundleContext(final BundleContext bundleContext) // comes from BundleContextAware
    {
        ServiceTracker tracker = new ServiceTracker(bundleContext, "com.example.plugin.package.ExampleDependency", new ServiceTrackerCustomizer(){

            public Object addingService(ServiceReference serviceReference)
            {
                final ExampleDependency exampleDependency = (ExampleDependency) bundleContext.getService(serviceReference);
                exampleIsPresent = true;
                return exampleDependency;
                
            }

            public void modifiedService(ServiceReference serviceReference, Object o)
            {
                /* Do nothing for this simple case */
            }

            public void removedService(ServiceReference serviceReference, Object o)
            {
                exampleIsPresent = false;
            }
        });
        
        // Start the tracker. 
        tracker.open();
        this.tracker = tracker;
    }

    /**
     * Invoked by a BeanFactory on destruction of a singleton.
     *
     * @throws Exception in case of shutdown errors.
     *                   Exceptions will get logged but not rethrown to allow
     *                   other beans to release their resources too.
     */
    public void destroy() throws Exception // comes from DisposableBean
    {
        // stick your cleanup code here
        tracker.close();
    }

}
```

**ExampleInterface.java**

``` java
package com.example.somepackage;

public interface ExampleInterface{}
```

Just query the method **isExamplePresent** to find out if the example dependency is available, and execute different code based on the result.

##### RELATED TOPICS

[Advanced Plugin Development FAQ](/server/framework/atlassian-sdk/advanced-plugin-development-faq)  
[Set up the Atlassian Plugin SDK and Build a Project](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project)







































































































































































































































































































































































































































