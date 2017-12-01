---
aliases:
- /server/framework/atlassian-sdk/access-components-statically-852012.html
- /server/framework/atlassian-sdk/access-components-statically-852012.md
category: devguide
confluence_id: 852012
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852012
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852012
legacy_url: https://developer.atlassian.com/docs/faq/plugin-framework-faq/access-components-statically
new_url: /server/framework/atlassian-sdk/access-components-statically
platform: server
product: atlassian-sdk
subcategory: faq
title: Access components statically
---
# Access components statically

Any class defined in a module descriptor will be created and autowired automatically by Spring, optionally injecting host components, imported components, and components defined in your plugin. However, there are several cases, such as Confluence Jobs, where your object cannot be created via Spring and therefore, you need to find another way to access a component.

{{% note %}}

This should only be tried as a last resort. Make sure you aren't just working around a poorly designed circular dependency or avoiding passing components to objects instantiated from components.

{{% /note %}}

The solution is to create a component that is injected with everything you need that then exposes those beans as static methods. For example, you could define this component in your `atlassian-plugin.xml`:

``` xml
<component key="staticAccessor" class="com.example.myplugin.StaticAccessor />
```

Then code `StaticAccessor` as follows:

``` java
public class StaticAccessor {
 
    private static SpaceManager spaceManager;
    private static PluginSettingsFactory pluginSettingsFactory;
    private static MyComponent myComponent;

    public StaticAccessor(SpaceManager spaceManager, PluginSettingsFactory pluginSettingsFactory, MyComponent myComponent) {
        StaticAccessor.spaceManager = spaceManager;
        StaticAccessor.pluginSettingsFactory = pluginSettingsFactory;
        StaticAccessor.myComponent = myComponent;
    }

    public static SpaceManager getSpaceManager() {
        return spaceManager;
    }

    public static PluginSettingsFactory getPluginSettingsFactory() {
        return pluginSettingsFactory;
    }

    public static MyComponent getMyComponent() {
        return myComponent;
    }
}
```

In this example, SpaceManager is a Confluence host component, PluginSettingsFactory is an imported component from SAL, and MyComponent is a component defined in your plugin.

Finally, in your class that can't be injected, you can now easily access the components you need statically from StaticAccessor.

This technique contains several patterns that are generally very bad, but acceptable here:

1.  Static variables will be null if accessed before the object is constructed. However, as long as you don't try to call StaticAccessor from a constructor, the variables will be guaranteed to be assigned before access.
2.  Static state is generally thought of to be type of global variable, however since the class is loaded as part of an OSGi bundle, you can think of it scoped to the bundle's lifecycle - when the plugin is uninstalled, the state goes away. However, be aware that even if the plugin is disabled, the ClassLoader for that bundle, which contains a direct reference on the StaticAccessor class and therefore, its static variables, will still be around. Since this technique only advocates storing static references to defined components, this shouldn't be a problem.





















































































