---
aliases:
- /server/framework/atlassian-sdk/852146.html
- /server/framework/atlassian-sdk/852146.md
category: devguide
confluence_id: 852146
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852146
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852146
date: '2017-12-08'
guides: guides
legacy_title: OSGi, Spring and the Plugin Framework
platform: server
product: atlassian-sdk
subcategory: learning
title: OSGi, Spring and the Plugin framework
---
# OSGi, Spring and the Plugin framework

<a href="http://www.osgi.org/" class="external-link">OSGi</a> is a dynamic module system for Java.

## OSGi Terminology

-   **Bundle** -- A bundle is a JAR file with special OSGi entries in its manifest and containing classes, resources, and other JARs.
-   **Lifecycle** -- A lifecycle is the sequence of states a [bundle](https://developer.atlassian.com/pages/viewpage.action?pageId=852005) goes through: uninstalled, installed, resolved, starting, stopping, active.
-   **Service** -- A service is an object instance exposed under the one or more interfaces that it implements and a map of properties.

Take a look at the <a href="/server/framework/atlassian-sdk/plugin-framework-glossary" class="createlink">glossary</a> for more terms and definitions.

## Overview of OSGi in the Plugin Framework

#### OSGi Features

-   Service registry
-   Lifecycle model
-   Bundle dependency system
-   Optional security layer (not currently used, but may be used in the future e.g. to define trusted plugins)

#### What Benefits do the Above Features Give Us?

-   You can upgrade bundles at runtime.
-   Bundles can depend on other bundles at a service, package, or JAR level. At a very simple level, you can define that plugin A requires plugin B
-   Bundles can hide packages from other bundles. For example, you might make your API package public but hide other packages. This reduces the complexity of dependencies, making it easier for you to change your plugin and know that you will not break other plugins on upgrade.
-   Bundles can expose packages by version.

#### Service Registry

A service registry is a map of one or more interfaces bound to object instances, with a set of properties attached to it.

-   Key -- A string representation of the interface name. One or more interfaces that this service is implementing.
-   Instance
-   Properties

Example of a service registration:

``` xml
Key: "com.foo.MyInterface"
Instance: com.foo.MyService
Properties:
name => foo
someProperty => someValue
```

#### Lifecycle

A lifecycle is the sequence of states a [bundle](https://developer.atlassian.com/pages/viewpage.action?pageId=852005) goes through: uninstalled, installed, resolved, starting, stopping, active.

Most stages in the bundle lifecycle are familiar to plugin developers. OSGi adds the **resolved** step. This indicates that the OSGi system has connected up all the dependencies at a class level and made sure they are all resolved.

#### Bundle Manifest

When you create an OSGi bundle, the manifest is where you declare information such as a bundle symbolic name (i.e. the plugin key) and the bundle version (i.e. the plugin version), etc.

You can import a package, and even declare that you need a specific version of the package. This is a nice way to declare your dependencies. For example, if your plugin uses Velocity, you can say you require Velocity 1.5 or greater.

You can export packages, i.e. make them available to other plugins and/or applications.

You can also define a class path for where you are putting your dependent JARs. Either you can continue putting all your dependent JARs into the default `META-INF/lib` folder inside the JAR, or you can choose your own custom location.

Example of a bundle manifest:

``` xml
Manifest-Version: 1.0
Bundle-ManifestVersion: 2
Bundle-SymbolicName: org.foo.Example
Bundle-Version: 1.0
Import-Package: org.bar;version="1.3.0"
Export-Package: org.foo.api
Bundle-ClassPath: .,META-INF/lib/foo.jar
```

More: [Managing Dependencies](/server/framework/atlassian-sdk/managing-dependencies).

#### Spring Dynamic Modules

The <a href="http://docs.spring.io/osgi/docs/current/reference/html/" class="external-link">Spring Dynamic Modules</a> library (Spring DM) enables developers to build plugins with a consistent dependency injection across Atlassian applications.

Spring DM takes the service model of OSGi and simplifies it into Spring terms, making the dynamics of OSGi services a bit easier to work with. This is especially useful for developers who are already familiar with Spring.

Spring DM gives every plugin its own bean factory. You can:

-   Declare internal beans, e.g. beans used by the plugin but not available publicly.
-   Expose beans, using a bit of XML, as OSGi services so that other plugins can consume them.
-   Declare a bean in your bean factory which is simply a proxy to another service provided by another bundle. You declare the interface in your constructor and get it injected, but Spring handles how that instance of that interface is wired to an actual service in OSGi.

For more information, see the <a href="http://docs.spring.io/osgi/docs/current/reference/html/" class="external-link">Spring DM documentation</a>.

#### Using Services

``` xml
<osgi:service id="fooService"
  ref="foo"
  interface="com.myapp.Foo"/>
```

#### Declaring a Bean as an OSGi Service

``` xml
<!-- bunch of XML namespace stuff skipped -->
<beans>
<bean name="foo" class="com.myapp.FooImpl"/>
<osgi:service id="fooService" ref="foo"
  interface="com.myapp.Foo"/>
</beans>
```

#### Declaring an OSGi Service as a Bean

``` xml
<!-- bunch of XML namespace stuff skipped -->
<beans>
<osgi:reference id="foo"
  interface="com.myapp.Foo"/>
</beans>
```

#### Making Plugins Depend on Each Other

Plugins can generate their own OSGi headers and use:

``` xml
Require-Bundle: org.otherPlugin;bundleversion="[3.2.0,4.0.0)"

Import-Package: org.otherPlugin.api;version="[3.2.0,4.0.0)"
```

#### Defining Extension Points for Plugins

-   Plugin A contains the `org.Foo` interface and defines a service reference:

    ``` xml
    <component-import key="foo" interface="org.Foo" />
    ```

-   Plugin B exposes its implementation:

    ``` xml
    <component key="foo" public="true"
    class="org.bar.FooImpl" interface="org.foo.Foo" />
    ```

##### RELATED TOPICS

[Managing Dependencies](/server/framework/atlassian-sdk/managing-dependencies)  
[Using the OSGi Browser](/server/framework/atlassian-sdk/using-the-osgi-browser)  
[Writing Atlassian Plugins](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Writing+Atlassian+Plugins)
