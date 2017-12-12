---
aliases:
- /server/framework/atlassian-sdk/component-plugin-module-852118.html
- /server/framework/atlassian-sdk/component-plugin-module-852118.md
category: reference
confluence_id: 852118
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852118
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852118
date: '2017-12-08'
legacy_title: Component Plugin Module
platform: server
product: atlassian-sdk
subcategory: modules
title: Component plugin module
---
# Component plugin module

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p>Atlassian Plugin Framework 2.0 and later.<br />
<em>Note</em>: The Component plugin module described below is available only for OSGi-based plugins using version 2 of the Plugin Framework.<br />
<br />
In version 1 plugins, this plugin module will differ significantly from the information on this page. In version 1 dynamic plugins or those deployed in <code>WEB-INF/lib</code>, this plugin module will be interpreted differently based on the application to which the plugin is deployed because it installs the component in the application's object container. For example, JIRA uses Pico and Confluence uses Spring. So the object's lifecycle and dependency injection process will vary.<br />
<br />
For version 2 plugins, as described below, the internal Spring framework is used regardless of the host application. Creation, dependency injection and sharing between plugins are consistent.</p></td>
</tr>
</tbody>
</table>

 

 

## Purpose of this Module Type

Component plugin modules enable you to share Java components between other modules in your plugin and optionally with other plugins in the application. You can use it to make any type of class instance available to other plugins or modules. It's in effect a Spring bean declaration (with greatly simplified syntax, since only autowiring is supported) plus an OSGi export.

The typical uses of a component are:

-   To define a singleton class that's used internally by your plugin, which the framework instantiates for you and passes to your other classes via autowiring; or
-   To expose an API to other plugin modules.

## Configuration

The root element for the Component plugin module is `component`. It allows the following attributes and child elements for configuration:

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
<td>alias</td>
<td><p>The alias to use for the component when registering it in the internal bean factory.</p>
<p><strong>Default:</strong> the plugin key.</p></td>
</tr>
<tr class="even">
<td><p>class</p></td>
<td><p>The class which implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>. </p>
<p>The Java class of the component. This does not need to extend or implement any class or interface. </p></td>
</tr>
<tr class="odd">
<td>key</td>
<td><p> The unique identifier of the plugin module. You refer to this key to use the resource from other contexts in your plugin, such as from the plugin Java code or JavaScript resources.</p>
<p> </p>
<pre><code>&lt;component-import key=&quot;appProps&quot; interface=&quot;com.atlassian.sal.api.ApplicationProperties&quot;/&gt;</code></pre>
<p> </p>
<p>In the example, <code>appProps</code> is the key for this particular module declaration, for <code>component-import</code>, in this case.</p>
 
<p>I.e. the identifier of the component.</p></td>
</tr>
<tr class="even">
<td><p>state</p>
<p> </p></td>
<td><p>Indicate whether the plugin module should be disabled by default (value='disabled') or enabled by default (value='enabled').</p>
<p><strong>Default:</strong> enabled.</p></td>
</tr>
<tr class="odd">
<td><p>i18n-name-key</p></td>
<td>The localisation key for the human-readable name of the plugin module.</td>
</tr>
<tr class="even">
<td><p>key</p></td>
<td>The unique identifier of the plugin module. You refer to this key to use the resource from other contexts in your plugin, such as from the plugin Java code or JavaScript resources.
<p> </p>
<pre><code>&lt;component-import key=&quot;appProps&quot; interface=&quot;com.atlassian.sal.api.ApplicationProperties&quot;/&gt;</code></pre>
<p> </p>
<p>In the example, <code>appProps</code> is the key for this particular module declaration, for <code>component-import</code>, in this case.</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module. </p>
<p>I.e. the human-readable name of the component.</p>
<p><strong>Default:</strong> the plugin key.</p></td>
</tr>
<tr class="even">
<td>public</td>
<td><p>Indicates whether this component should be made available to other plugins via the <a href="https://developer.atlassian.com/display/DOCS/Component+Import+Plugin+Module">Component Import Plugin Module</a> or not.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
<tr class="odd">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
</tbody>
</table>

**\*key attribute is required.**

#### Elements

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
<td>interface</td>
<td><p>The Java interface under which this component should be registered.</p>
<p>This element can appear zero or more times.</p></td>
</tr>
<tr class="even">
<td><p>description</p></td>
<td><p> The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body.</p></td>
</tr>
<tr class="odd">
<td>service-properties</td>
<td><p>Map of simple properties to associate with a public component (Plugin Framework 2.3 and later).</p>
<p>Child elements are named <code>entry</code> and have <code>key</code> and <code>value</code> attributes.</p>
<p>Service properties are intended to serve as filterable values in the component-import declarations that use this component.</p>
<p>This allows you to define various flavors of a public component, and import them based on the value of these flavors.</p>
<p>For example, when importing a component named <code>dictionaryService</code> with a <code>language</code> service property,</p>
<p>the <code>component-import</code> statement can select the component flavor with <code>language</code> property <code>English</code> as follows:</p>
<p><code>&lt;component-import key=&quot;dictionaryService&quot; interface=&quot;com.myapp.DictionaryService&quot; filter=&quot;(language=English)&quot; /&gt;</code></p></td>
</tr>
</tbody>
</table>

##  Example

Here is an example `atlassian-plugin.xml` file containing a single public component:

``` xml
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic component module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <component key="helloWorldService" class="com.myapp.DefaultHelloWorldService">
        <description>Provides hello world services.</description>
        <interface>com.myapp.HelloWorldService</interface>
    </component>
</atlassian-plugin>
```

Here is an example public component with several service properties:

``` xml
<component key="dictionaryService" class="com.myapp.DefaultDictionaryService" interface="com.myapp.DictionaryService">
    <description>Provides a dictionary service.</description>
    <service-properties>
        <entry key="language" value="English" />
    </service-properties>
</component>
```

## Notes

Some information to be aware of when developing or configuring a Component plugin module:

-   Components, at installation time, are used to generate the `atlassian-plugins-spring.xml` Spring Framework configuration file, transforming Component plugin modules into Spring bean definitions. The generated file is stored in a temporary plugin jar and installed into the framework. The plugin author should very rarely need to override this file.
-   The injection model for components first looks at the constructor with the largest number of arguments and tries to call it, looking up parameters by type in the plugin's bean factory. If only a no-arg constructor is found, it is called then Spring tries to autowire the bean by looking at the types used by setter methods. If you wish to have more control over how your components are created and configured, you can create your own Spring configuration file, stored in `META-INF/spring` in your plugin jar.
-   If the `public` attribute is set to 'true', the component will be turned into an OSGi service under the covers, using Spring Dynamic Modules to manage its lifecycle.
-   This module type in non-OSGi (version 1) plugins supported the StateAware interface in some products to allow a component to react to when it is enabled or disabled. To achieve the same effect, you can use the two Spring lifecycle interfaces: <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/beans/factory/InitializingBean.html" class="external-link">InitializingBean</a> and <a href="http://static.springframework.org/spring/docs/2.5.x/api/org/springframework/beans/factory/DisposableBean.html" class="external-link">DisposableBean</a>. The init() and destroy() methods on these interfaces will be called when the module is enabled or disabled, exactly like StateAware. Making this change to a component in an existing plugin will be backwards compatible in all but JIRA. That is, a component module in a legacy plugin which implements InitializingBean will have its init() method called when it is enabled, exactly the same as such a component in an OSGi plugin.
-   Components for non-OSGi (version 1) plugins behave very differently to components for OSGi plugins. For version 1 plugins, components are loaded into the application's object container, be it PicoContainer for JIRA or Spring for all other products that support components. For OSGi plugins, components are turned into beans for the Spring bean factory for that specific plugin. This provides more separation for plugins, but means you cannot do things like override JIRA components in OSGi plugins, as you can for static plugins.

##### RELATED TOPICS

[Plugin Modules](/server/framework/atlassian-sdk/plugin-modules)



































































































































































































