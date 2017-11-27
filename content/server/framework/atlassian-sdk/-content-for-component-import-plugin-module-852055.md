---
title: Content for Component Import Plugin Module 852055
aliases:
    - /server/framework/atlassian-sdk/-content-for-component-import-plugin-module-852055.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852055
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852055
confluence_id: 852055
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Component Import Plugin Module

## Purpose of this Module Type

Component Import plugin modules allow you to access Java components shared by other plugins, even if the component is upgraded at runtime.

## Configuration

The root element for the Component Import plugin module is `component-import`. It allows the following attributes and child elements for configuration:

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
<td><p>interface</p></td>
<td><p>The Java interface of the component to import.</p>
<p>This attribute is only required if the <code>interface</code> elements are not used.</p></td>
</tr>
<tr class="even">
<td>key</td>
<td><p>The unique identifier of the plugin module. You refer to this key to use the resource from other contexts in your plugin, such as from the plugin Java code or JavaScript resources.</p>
<p> </p>
<pre><code>&lt;component-import key=&quot;appProps&quot; interface=&quot;com.atlassian.sal.api.ApplicationProperties&quot;/&gt;</code></pre>
<p> </p>
<p>In the example, <code>appProps</code> is the key for this particular module declaration, for <code>component-import</code>, in this case.</p>
 
<p>That is, the identifier of the component to import.</p></td>
</tr>
<tr class="odd">
<td><p>filter</p>
<p> </p></td>
<td><p>The LDAP filter to use to match public components (OSGi services).</p>
<p>The format of the filter must be a valid LDAP filter. (Plugin Framework 2.3 and later.)</p></td>
</tr>
</tbody>
</table>

**\*interface and key attributes are required.**

#### Elements

-   interface - the Java interface under which the component to retrieve is registered. This element can appear zero or more times, but is required if the `interface` attribute is not used. **Required.**

## Example

Here is an example `atlassian-plugin.xml` file containing a single component import:

``` xml
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic component import module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <component-import key="helloWorldService">
        <interface>com.myapp.HelloWorldService</interface>
    </component-import>
</atlassian-plugin>
```

It consumes a component made available via a different plugin:

``` xml
<atlassian-plugin name="Hello World Provider" key="example.plugin.helloworld.provider" plugins-version="2">
    <plugin-info>
        <description>A basic component module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <component key="helloWorldService" class="com.myapp.internal.MyHelloWorldService" public="true">
        <interface>com.myapp.HelloWorldService</interface>
    </component>
</atlassian-plugin>
```

Here is an example of matching via an LDAP filter. Since a component import is really just matching an OSGi service, you can optionally specify an LDAP filter to match the specific service. Here is an example that matches a dictionary service that provides a `language` attribute that equals `English`:

``` xml
<component-import key="dictionaryService" interface="com.myapp.DictionaryService"
                  filter="(language=English)" />
```

## Notes

Some information to be aware of when developing or configuring a Component Import plugin module:

-   Component imports, at installation time, are used to generate the `atlassian-plugins-spring.xml` Spring Framework configuration file, transforming Component Import plugin modules into OSGi service references using Spring Dynamic Modules.
-   The imported component will have its bean name set to the component import key, which may be important if using 'by name' dependency injection.
-   If you wish to have more control over how imported services are discovered and made available to your plugin, you can create your own Spring configuration file containing Spring Dynamic Modules elements, stored in `META-INF/spring` in your plugin jar. This is recommended if you are needing to import multiple services that implement an interface, for example.
-   You can use component imports to customise the bean name of host components, particularly useful if you plan to use 'by name' dependency injection.

















































































































































































































































































































