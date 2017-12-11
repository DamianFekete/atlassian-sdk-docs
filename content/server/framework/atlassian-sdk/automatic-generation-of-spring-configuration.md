---
aliases:
- /server/framework/atlassian-sdk/automatic-generation-of-spring-configuration-852044.html
- /server/framework/atlassian-sdk/automatic-generation-of-spring-configuration-852044.md
category: devguide
confluence_id: 852044
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852044
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852044
date: '2017-12-11'
guides: guides
legacy_title: Automatic Generation of Spring Configuration
platform: server
product: atlassian-sdk
subcategory: learning
title: Automatic generation of Spring configuration
---
# Automatic generation of Spring configuration

The Atlassian Plugin Framework uses <a href="http://www.springframework.org/osgi" class="external-link">Spring</a> to implement many of its features for OSGi plugins by automatically generating Spring XML configuration files. This generation occurs as several steps in the [OSGi plugin -&gt; OSGi bundle transformation](/server/framework/atlassian-sdk/going-from-plugin-to-osgi-bundle) that happens at plugin installation. These steps are:

1.  Component Import transformation
2.  Component transformation
3.  Host component imports
4.  Module Type transformation

#### Component Import Transformation

The [Component Import](/server/framework/atlassian-sdk/component-import-plugin-module) module type allows a plugin to import a component exposed by another plugin or by the host application itself. These elements are converted into the Spring configuration file `META-INF/spring/atlassian-plugins-component-imports.xml` as Spring DM `<osgi:reference>` elements. See the <a href="http://static.springsource.org/osgi/docs/1.1.3/reference/html/service-registry.html#service-registry:refs" class="external-link">Spring DM documentation</a>.

In their place, a placeholder module descriptor is stored in the plugin framework so that the import will appear in the list of plugin modules. However, disabling it has no effect.

#### Component Transformation

The [Component](/server/framework/atlassian-sdk/component-plugin-module) module type allows a plugin to make an object available for dependency injection within the plugin, and with the 'public' flag, also expose that instance to other plugins, accessible via the Component Import module type. The transformation that occurs upon installation converts these elements into Spring `<beans:bean>` elements in a configuration file called `META-INF/spring/atlassian-plugins-components.xml`. If the 'public' flag is set to true, the bean instances are also exposed via the Spring DM `<osgi:service>` element. See the <a href="http://static.springsource.org/osgi/docs/1.1.3/reference/html/service-registry.html#service-registry:export" class="external-link">Spring DM documentation</a>.

Like the Component Import module type, in their place, a placeholder module descriptor is stored in the plugin framework so that the component will appear in the list of plugin modules. However, disabling it has no effect.

#### Host Component Imports

Upon plugin installation, the plugin framework will scan the classes in the plugin JAR for any references to host components. If any are detected, the framework will generate the Spring configuration file `META-INF/spring/atlassian-plugins-host-components.xml` to add a bean for each host component needed. Since host components are always available and do not change during runtime, the bean definitions are special purpose beans that import the host component services on startup. The Spring DM `<osgi:reference>` element is not used, because it adds a lot of overhead that is not necessary here. You can override the beans by using the `<component-import>` element to specify a different bean name, since if the plugin framework detects an import for a host component, it will not generate a bean reference.

This is an example of a generated host component reference named 'foo':

``` xml
<beans:bean id="foo" class="com.atlassian.plugin.osgi.bridge.external.HostComponentFactoryBean">
  <beans:property name="filter" value="(&amp;(bean-name=foo)(plugins-host=true))"/>
</beans:bean>
```

The 'bean-name' is provided to the plugin framework by the application on initialisation, and the 'plugins-host' property is used to further restrict the filter to just host components.

#### Module Type Transformation

The [Module Type](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Module+Type+Plugin+Module) module allows a plugin to define its own plugin module types that it and other plugins can use. At installation time, it generates a bit of Spring configuration in a file named `META-INF/spring/atlassian-plugins-module-types.xml` to expose the appropriate `com.atlassian.plugin.ModuleDescriptorFactory` instance.

Here is an example of a module type 'foo' that uses the `my.FooDescriptor` module descriptor instance:

Code in `atlassian-plugin.xml`:

``` xml
<module-type key="foo" class="my.FooDescriptor" />
```

Code in `META-INF/spring/atlassian-plugins-module-types.xml`:

``` xml
<beans:bean id="springHostContainer" class="com.atlassian.plugin.osgi.bridge.external.SpringHostContainer"/>
<beans:bean id="moduleType-foo" class="com.atlassian.plugin.osgi.external.SingleModuleDescriptorFactory">
  <beans:constructor-arg index="0" ref="springHostContainer"/>
  <beans:constructor-arg index="1">
    <beans:value>foo</beans:value>
  </beans:constructor-arg>
  <beans:constructor-arg index="2">
    <beans:value>my.FooDescriptor</beans:value>
  </beans:constructor-arg>
</beans:bean>
<osgi:service id="moduleType-foo_osgiService" ref="moduleType-foo" auto-export="interfaces"/>
```

The `SpringHostContainer` bean is only created once per plugin, providing the ability to instantiate module descriptor instances using the plugin's Spring container. This means the module descriptor class 'FooDescriptor' can support constructor dependency injection for host and plugin components.

##### RELATED TOPICS

[Going from Plugin to OSGi Bundle](/server/framework/atlassian-sdk/going-from-plugin-to-osgi-bundle)  
[Plugin Framework](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Plugin+Framework)























































































































































































































































































































































































