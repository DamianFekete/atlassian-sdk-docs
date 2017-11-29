---
title: Content for Template Context Items Plugin Module 852140
aliases:
    - /server/framework/atlassian-sdk/-content-for-template-context-items-plugin-module-852140.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852140
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852140
confluence_id: 852140
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Template Context Items Plugin Module

## Purpose of this Module Type

This module type allows you to put arbitrary context items into the context of any <a href="/pages/createpage.action?spaceKey=ATR&amp;title=Using+the+Atlassian+Template+Renderer" class="createlink">Using the Atlassian Template Renderer</a>. This is useful to ensure plugin developers don't have to repeatedly create the same context each time they need to render content.

This module type is similar to the Confluence velocity-context-item module type. However, it is more powerful in the following ways:

-   It can be used with any template rendering technology, not just velocity
-   It allows items to be scoped in the context of the plugin that declares it, or to be in the global context of all plugins
-   It allows referencing of arbitrary components, not just classes. This means you don't need to create wrapper classes if you want to put a general component (such as the SAL I18nResolver) in your context. It also means you can use Spring prototype beans if you want to use some per context stateful bean

## Configuration

The root element for the Template Context Items plugin module is `template-context-item`. It allows the following attributes for configuration:

#### Attributes

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name*</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>context-key</p></td>
<td><p>The key with which the context item is referenced from templates, e.g. <code>$i18n</code> in the example below.</p></td>
</tr>
<tr class="even">
<td><p>component-ref </p></td>
<td><p>A reference to a component in the plugin's application context.</p>
<p>To reference OSGi services or host components, import the component using <code>component-import</code>.</p>
<p>The component will be looked up on each use, so prototype spring beans will be newly instantiated each time.</p></td>
</tr>
<tr class="odd">
<td><p>class</p></td>
<td><p>The class that should be instantiated and put into the context. This will be a singleton.</p>
<p><strong>Note:</strong> either this or <code>component-ref</code>, but not both, is required.</p></td>
</tr>
<tr class="even">
<td><p>global</p></td>
<td><p>True if the context item should be available to contexts for all plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
</tbody>
</table>

**\*context-key attribute is required.**

## Example

``` javascript
<template-context-item key="i18nResolveContextItem" component-ref="i18nResolver"
    context-key="i18n" global="true" name="I18nResolver Context Item"/>
```

## Notes

### Rendering templates for other plugins

When rendering templates for other plugins, you need to ensure your plugin gets the template renderer for the other plugins bundle. There are many ways to do this, and all involve getting a hold of the plugins `BundleContext`. With the bundle context, you can lookup the `TemplateRenderer` service, however, in most cases you won't want to do this directly, as you may encounter problems if the template renderer has not been enabled yet, or is restarted. It will usually be more appropriate to use a `ServiceTracker`, and access the template renderer through that.

The following are the two best ways of getting a hold of the plugins `BundleContext`, which will apply depending on your situation:

#### When you have a reference to the plugin's `Plugin` object

This will be the case if you have defined a dynamic module type, from which you can access the plugins `Plugin` object. In this case, you can access the `BundleContext` like so:

``` javascript
BundleContext ctx = ((OsgiPlugin) plugin).getBundle().getBundleContext();
```

#### When you expose a service that is imported by the plugin

In this case, you should expose an OSGi `ServiceFactory` for your service. These work in the same way to Springs `FactoryBean`'s. Here's an example:

``` javascript
public class MyServiceServiceFactory implements ServiceFactory
{
    public Object getService(Bundle bundle, ServiceRegistration registration)
    {
        return new MyService(bundle.getBundleContext());
    }
    ...
}
```

#### Using a `ServiceTracker`

Once you have a `BundleContext`, you need to create `ServiceTracker` that tracks the `TemplateRenderer` service in the plugins `BundleContext`:

``` javascript
private final ServiceTracker templateRendererServiceTracker;
public MyService(BundleContext bundleContext)
{
    templateRendererServiceTracker = new ServiceTracker(bundleContext, TemplateRenderer.class.getName(), null);
    templateRendererServiceTracker.open();
}
```

Now you can use the service using the `getService()`. The important thing that you need to worry about is handling if the service isn't available. Sometimes it may be appropriate to do no action, at other times, you may want to throw an exception:

``` javascript
TemplateRenderer renderer = (TemplateRenderer) templateRendererServiceTracker.getService();
if (renderer == null)
{
    throw new RuntimeException("TemplateRenderer service not available");
}
// Now use the renderer
```

Finally, it's important that you close the `ServiceTracker` once you're finished using it. There are a number of reasons why this might happen:

-   Your plugin might be brought down
-   The plugin using you might be brought down
-   The plugin using you might decide to unimport your service

Closing the service tracker should be done in your plugin module type descriptors disable method, or your `ServiceFactory`'s unget method. For example:

``` javascript
public void ungetService(Bundle bundle, ServiceRegistration registration, Object service)
{
    ((MyService) service).closeTemplateRendererServiceTracker();
}
```

In `MyService` you would then have a corresponding method that would call the `close()` method on the service tracker.

























