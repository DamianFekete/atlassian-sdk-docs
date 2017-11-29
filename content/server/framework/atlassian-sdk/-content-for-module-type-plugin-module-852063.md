---
title: Content for Module Type Plugin Module 852063
aliases:
    - /server/framework/atlassian-sdk/-content-for-module-type-plugin-module-852063.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852063
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852063
confluence_id: 852063
platform:
product:
category:
subcategory:
---
# Documentation : \_Content for Module Type Plugin Module

## Purpose of this Module Type

Module Type plugin modules allow you to dynamically add new plugin module types to the plugin framework, generally building on other plugin modules. For example, a plugin developer could create a `<dictionary>` plugin module that is used to feed a dictionary service used by still other plugins.

## Configuration

The root element for the Module Type plugin module is `module-type`. It allows the following attributes and child elements for configuration:

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
<td><p>class</p></td>
<td><p>The ModuleDescriptor class to instantiate when a new plugin module of this type is found.</p>
<p>See the plugin framework guide to <a href="/server/framework/atlassian-sdk/creating-plugin-module-instances-851984.html">creating plugin module instances</a>.</p></td>
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
<td><p>The unique identifier of the plugin module. You refer to this key to use the resource from other contexts in your plugin, such as from the plugin Java code or JavaScript resources.</p>
<p> </p>
<pre><code>&lt;component-import key=&quot;appProps&quot; interface=&quot;com.atlassian.sal.api.ApplicationProperties&quot;/&gt;</code></pre>
<p> </p>
<p>In the example, <code>appProps</code> is the key for this particular module declaration, for <code>component-import</code>, in this case.</p>
 
<p>I.e. the identifier of the module type. This value will be used as the XML element name to match.</p></td>
</tr>
<tr class="odd">
<td><p>name</p></td>
<td><p>The human-readable name of the plugin module.</p></td>
</tr>
<tr class="even">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
</tbody>
</table>

**\*key attribute is required.**

#### Elements

-   description - The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body.

## Example

Here is an example `atlassian-plugin.xml` file containing a plugin module type:

``` xml
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A dictionary module type test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <module-type key="dictionary" class="example.plugin.DictionaryModuleDescriptor" />
</atlassian-plugin>
```

Our dictionary module descriptor allows plugins to provide dictionaries that get definitions of technical terms and phrases in various languages. We have a `Dictionary` interface that looks like this:

``` java
public interface Dictionary
{
    String getDefinition(String text);
}
```

The Java code for `DictionaryModuleDescriptor` could look like this:

``` java
public class DictionaryModuleDescriptor extends AbstractModuleDescriptor<Dictionary>
{
    private String language;

    @Override
    public DictionaryModuleDescriptor(ModuleFactory moduleFactory)
    {
        super(moduleFactory);
    }

    @Override
    public void init(Plugin plugin, Element element) throws PluginParseException
    {
        super.init(plugin, element);
        language = element.attributeValue("lang");
    }

    public Dictionary getModule()
    {
         return moduleFactory.createModule(moduleClassName, this);
    }

    public String getLanguage()
    {
        return language;
    }
}
```

This will add the new module type 'dictionary' to the plugin framework, allowing other plugins to use the new module type. Here is a plugin that uses the new 'dictionary' module type:

``` xml
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>An english dictionary</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <dictionary key="myEnglishDictionary" lang="english" class="example.plugin.english.MyDictionary" />
</atlassian-plugin>
```

Accessing modules of your dynamic module type can be done using `com.atlassian.plugin.PluginAccessor`.

``` java
// To get all the enabled modules of this module descriptor
List<DictionaryModuleDescriptor> dictionaryModuleDescriptors =
        pluginAccessor.getEnabledModuleDescriptorsByClass(DictionaryModuleDescriptor.class);
// Now we'll use each one to get a map of languages to translations of the word "OSGi"
Map<String, String> results = new HashMap<String, String>();
for (DictionaryModuleDescriptor dictionaryModuleDescriptor : dictionaryModuleDescriptors)
{
    results.put(dictionaryModuleDescriptor.getLanguage(),
            dictionaryModuleDescriptor.getModule().getDefinition("OSGi"));
}
```

Note that it is not advisable to cache the results of calls to `com.atlassian.plugin.PluginAccessor`'s methods, since the return values can change at any time as a result of plugins being installed, uninstalled, enabled, or disabled.

## Notes

Some information to be aware of when developing or configuring a Module Type plugin module:

-   Not all dynamic module types will need to use the `class` attribute on the modules that implement them. For example, if the above dictionary example just used a resource file to translate terms, and not an interface that plugins had to implement, plugins using the dictionary module type might look like this:

    ``` xml
    <dictionary key="myEnglishDictionary" lang="english" resource="example/plugin/english/myDictionary.properties" />
    ```

-   The plugin that defines a new module type cannot use the module type in the Plugin Framework 2.1, but can in 2.2 or later.
-   If you want to have control over the construction of the ModuleDescriptor, you can skip the 'module-type' module and make public a component registered against the ModuleDescriptorFactory interface:

    ``` xml
    <component key="dictionaryFactory" class="example.plugin.DictionaryModuleDescriptorFactory" public="true">
      <interface>com.atlassian.plugin.ModuleDescriptorFactory</interface>
    </component>
    ```

    Ensure your `ModuleDescriptorFactory` implements `com.atlassian.plugin.osgi.external.ListableModuleDescriptorFactory`.

-   By specifying the `application` attribute in your module type element, you can ensure that a plugin only uses that module type when it is running in a specific application. For example, with the following snippet, the dictionary module type is only used when the plugin is loaded in JIRA:

    ``` java
    <dictionary key="myEnglishDictionary" lang="english" class="example.plugin.english.MyDictionary" application="jira" />
    ```

    The supported values for `application` are the **Product Keys** listed in the [Atlassian Plugin SDK documentation](/server/framework/atlassian-sdk/working-with-the-sdk-2818723.html#supported-atlassian-applicationsand-default-ports).

























