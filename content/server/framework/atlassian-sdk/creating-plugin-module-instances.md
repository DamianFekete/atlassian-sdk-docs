---
aliases:
- /server/framework/atlassian-sdk/creating-plugin-module-instances-851984.html
- /server/framework/atlassian-sdk/creating-plugin-module-instances-851984.md
category: devguide
confluence_id: 851984
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851984
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851984
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/creating-plugin-module-instances
new_url: /server/framework/atlassian-sdk/creating-plugin-module-instances
platform: server
product: atlassian-sdk
subcategory: learning
title: Creating plugin module instances
---
# Creating plugin module instances

 

## Overview

When specifying an implementation of a plugin module, you can specify the class name that the plugin framework should resolve, instantiate, and inject for you. Instances are created per usage (prototype-scope) and Spring injection will happen via <a href="http://static.springsource.org/spring/docs/2.5.6/reference/beans.html#beans-factory-autowire" class="external-link">autodetection autowire mode</a>, which tries constructor injection, falling back to setter injection by type.

In [Atlassian Plugin Framework 2.5](https://developer.atlassian.com/pages/viewpage.action?pageId=852001) and later, the instantiation of a plugin module has been improved to give you full control how your module classes will be created via a new optional prefix-based, pluggable PrefixModuleFactory interface. Out of the box, the framework ships with support for the `"bean:"` prefix that allows you to refer to a Spring bean by ID instead of specifying a classname in the module descriptor. This gives you complete control over the creation, scope, and injection of your plugin modules.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Everything from here down is available in</p></td>
<td><p><a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852001">Atlassian Plugin Framework 2.5</a> and later.</p></td>
</tr>
</tbody>
</table>

For example, if you wanted to instantiate a class, you could specify a servlet class via:

``` xml
<servlet key="myServlet" class="class:com.example.MyServlet" />
```

Since the "class" prefix is the default, you could also configure the Servlet via:

``` xml
<servlet key="myServlet" class="com.example.MyServlet" />
```

The following prefixes are supported:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Prefix</p></th>
<th><p>Description</p></th>
<th><p>Default</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>class</p></td>
<td><p>Instantiates the class via Spring using the autodetect autowire mode</p></td>
<td><p>true</p></td>
</tr>
<tr class="even">
<td><p>bean</p></td>
<td><p>Looks up the specified bean ID in the Spring context</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

## Using the "bean" Prefix

Before you can use the "bean" prefix, you must create a bean that lives in the Spring context. This bean can be specified via the `<component>` module type or in a custom Spring XML file living in `META-INF/spring`. When using Spring XML directly, you have full control over the creation, scope, and injection of the bean. Reasons you may want to use the "bean" prefix include:

-   Want to use constructor injection even if you have a default constructor.
-   Want to manually configure the beans to inject, including constants.
-   Want to share a module instance with components.
-   Want to customise the scope of the module instance. But be aware that the descriptor may cache the instance later.

### Examples

#### Making a module instance available to other components or plugin modules

In `atlassian-plugin.xml`:

``` xml
<component key="myServlet" class="com.example.MyServlet" />
<servlet key="myServlet" class="bean:myServlet" />
```

#### Using "byName" setter injection

In `META-INF/spring/myPlugin.xml`:

``` xml
<bean id="myServlet" class="com.example.MyServlet" autowire="byName"/>
```

In `atlassian-plugin.xml`:

``` xml
<servlet key="myServlet" class="bean:myServlet" />
```

## Creating a New Prefix

You can create your own prefix for further control over the creation of module instances. This technique can be used to do things like delegating the creation to a scripting engine or automatically wrapping all module instances in proxies.

### Example

Let's say we want to create a new prefix called "named", which instantiates all module instances via a single argument constructor that expects the name of the plugin.

#### Step 1. Create a PrefixModuleFactory instance

Our `NamedPrefixModuleFactory` loads the class then instantiates its constructor with the plugin key:

``` java
public class NamedPrefixModuleFactory implements PrefixModuleFactory
{
    public String getPrefix()
    {
        return "named";
    }

    public <T> T createModule(String name, ModuleDescriptor<T> moduleDescriptor) throws PluginParseException
    {
        try
        {
            Class clazz = getClass().getClassLoader().loadClass(name);
            return (T) clazz.getConstructor(String.class).newInstance(moduleDescriptor.getPluginKey());
        }
        catch (Exception e)
        {
            throw new RuntimeException("Obviously non-production code here...", e);
        }
    }
}
```

#### Step 2. Expose it as a component

Just by exposing the `NamedPrefixModuleFactory` as a component, or more specifically, as a bean in our `BeanFactory`, the plugin framework will pick it up and use it for plugin module prefix resolution:

``` xml
<component key="namedPrefix" class="com.example.NamedPrefixModuleFactory" />
```

#### Step 3. Use the new prefix

The prefix is now able to be used by plugin modules that expect objects like the servlet module type:

``` xml
<servlet key="myServlet" class="named:com.example.MyServlet" />
```

##### RELATED TOPICS

[Common Coding Tasks](/server/framework/atlassian-sdk/common-coding-tasks)  
[Plugin Modules](/server/framework/atlassian-sdk/plugin-modules)












































































































































































































































































































































































































































