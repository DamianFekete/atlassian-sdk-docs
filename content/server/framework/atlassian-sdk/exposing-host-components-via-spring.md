---
aliases:
- /server/framework/atlassian-sdk/exposing-host-components-via-spring-852023.html
- /server/framework/atlassian-sdk/exposing-host-components-via-spring-852023.md
category: devguide
confluence_id: 852023
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852023
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852023
date: '2017-12-08'
guides: tutorials
legacy_title: Exposing Host Components via Spring
platform: server
product: atlassian-sdk
subcategory: learning
title: Exposing host components via Spring
---
# Exposing host components via Spring

Atlassian Plugins comes with a Spring module that can be used to expose existing Spring beans to plugins either via XML or annotations.

{{% note %}}

Beans that are exposed as host components should be classes that implement one or more interfaces, which will be used solely for bean access. Under the covers, host components are exposed as OSGi services from the system bundle, and as such, they are exposed and matched as interfaces.

{{% /note %}}

#### Consuming host components

Before we get into exposing host components, it is worth discussing how to consume them. In a nutshell: simply use them in the constructions of your modules and components, and you'll get the instances injected.

The long answer is host components are exposed as OSGi services from the system bundle. If your plugin is a plain jar, during installation, the plugin framework will put it through a transformation pipeline to convert it to an OSGi bundle. As part of this, the framework generates any necessary Spring XML configuration files, one of which contains references to host components. The framework tries to scan your bytecode to see if you refer to the class of any host component, and if so, automatically generates a component-import, or more accurately, an OSGi service reference, to the host component service. With the host component now in the Spring bean factory, it is available for automatic injection by other Spring beans and module classes.

## Annotation-based HostComponentProvider

If using the annotation support in Spring 2.5 or later, you may wish to use annotations to mark spring beans that should be exposed to plugins as host components.

Assuming your Spring configuration is already configured to scan the classloader for classes with the @Component annotation, you can follow the following steps:

1.  Copy the atlassian-plugins-spring jar into your application. It contains a class called `SpringHostComponentProviderFactoryBean`, which has the `@Component` annotation. This FactoryBean will create an instance of `HostComponentProvider`.
2.  Consume the `HostComponentProvider` in your class that instantiates the plugin framework, passing the `HostComponentProvider` to the `PluginsConfigurationBuilder`.
3.  Annotate any Spring components that you'd like to expose to plugins with the @AvailableToPlugins annotation. By default, this will expose the bean under all interfaces it discovers, but you can customise the specific interface by passing in the interface class as the default annotation value.

## XML-based HostComponentProvider

If you are already defining your beans in XML, it may be more natural to also mark them as available to plugins via XML. Assuming you are using Spring 2.0 or later, with XML namespace support, you can follow these steps:

1.  Copy the atlassian-plugins-spring jar into your application. It contains a `META-INF/spring.handlers` file, which defines the XML namespace to use.
2.  Add the XML namespace to all applicable Spring XML configuration files. For example:

    ``` xml
    <beans xmlns="http://www.springframework.org/schema/beans"
           xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
           xmlns:plugin="http://atlassian.com/schema/spring/plugin"
           xsi:schemaLocation="
              http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.5.xsd
              http://atlassian.com/schema/spring/plugin http://atlassian.com/schema/spring/plugin.xsd">

        . . . 
    </beans>
    ```

3.  Use the new namespace in your XML, marking the desired beans as available to plugins with the "available" attribute. For example:

    ``` xml
    <bean name="foo2" class="com.example.MyServiceImpl" plugin:available="true"/> 
    ```

    You can also customise the interfaces under which the bean is exposed via the "interface" sub-element:

    ``` xml
    <bean name="fooCustomInterfaces" class="com.example.MyServiceImpl" plugin:available="true">
       <plugin:interface>com.example.MyService</plugin:interface>
       <plugin:interface>com.example.SomeCapability</plugin:interface>
    </bean>
    ```













































































































































































































































































































