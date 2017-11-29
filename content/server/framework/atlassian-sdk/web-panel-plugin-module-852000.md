---
title: Web Panel Plugin Module 852000
aliases:
    - /server/framework/atlassian-sdk/web-panel-plugin-module-852000.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852000
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852000
confluence_id: 852000
platform:
product:
category:
subcategory:
---
# Web Panel plugin module

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p><a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852001">Atlassian Plugin Framework 2.5</a>, Confluence 2.5, Bamboo 3.0, JIRA 4.4 and later.</p></td>
</tr>
</tbody>
</table>

 

 

## Purpose of this Module Type

Web Panel plugin modules allow plugins to define panels, or sections, on an HTML page. A panel is a set of HTML that will be inserted into a page.

## Configuration

The root element for the Web Panel plugin module is `web-panel`. It allows the following attributes and child elements for configuration:

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
<td><p>The class which implements this plugin module and which is responsible for providing the web panel's HTML.</p>
<p>In most cases you will not need to provide a custom class to generate the content,</p>
<p>as you can simply point to a static HTML file or a (Velocity) template.</p>
<p>See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>.</p>
<p>If you omit this attribute, you MUST provide a resource element and vice versa,</p>
<p>to ensure there is always exactly one source for the web panel's content.</p></td>
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
<td><p>The human-readable name of the plugin module.</p>
<p>Used only in the plugin's administrative user interface.</p></td>
</tr>
<tr class="even">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
<tr class="odd">
<td><p>weight</p>
<p> </p></td>
<td><p>Determines the order in which web panels appear.</p>
<p>Web panels are displayed top to bottom or left to right in order of ascending weight.</p>
<p>The 'lightest' weight is displayed first, the 'heaviest' weights sink to the bottom.</p>
<p>The weights for most applications' system sections start from 100, and the weights for the links generally start from 10.</p>
<p>The weight is incremented by 10 for each in sequence so that there is ample space to insert your own panels.</p>
<p><strong>Default:</strong> 1000.</p></td>
</tr>
<tr class="even">
<td>location</td>
<td><p>The location in the host application where the web panel must be rendered.</p>
<p>Note that every host application declares its own set of web panel plugin points.</p>
<p>Currently a web panel can only be associated with a single location.</p></td>
</tr>
</tbody>
</table>

**\*key and location attributes are required.**

#### Elements

The tables summarises the elements. The sections below contain further information.

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
<td><p><a href="#condition">condition</a></p></td>
<td><p>Defines a condition that must be satisfied for the web panel to be displayed.</p>
<p>If you want to 'invert' a condition, add an attribute 'invert=&quot;true&quot;' to it.</p>
<p>The web item will then be displayed if the condition returns false (not true).</p></td>
</tr>
<tr class="even">
<td><p><a href="#condition">conditions</a></p>
<p> </p></td>
<td><p>Defines the logical operator type to evaluate its condition elements. By default 'AND' will be used.</p>
<p><strong>Default:</strong> AND.</p></td>
</tr>
<tr class="odd">
<td><p><a href="#context-provider">context-provider</a></p></td>
<td><p>Allows dynamic addition to the Velocity context available for various web panel elements (in XML descriptors only).</p>
<p>Currently only one context-provider can be specified per web panel.</p></td>
</tr>
<tr class="even">
<td><p><a href="#label">label</a></p></td>
<td>Is the i18n key that will be used to look up the textual representation of the link.</td>
</tr>
<tr class="odd">
<td><p><a href="#param">param</a></p></td>
<td><p>Parameters for the plugin module. Use the 'key' attribute to declare the parameter key, then specify the value in either the 'value' attribute or the element body. This element may be repeated. An example is the configuration link described in <a href="https://developer.atlassian.com/display/DOCS/Adding+a+Configuration+UI+for+your+Plugin">Adding a Configuration UI for your Plugin</a>.</p>
<p>This is handy if you want to use additional custom values from the UI.</p></td>
</tr>
<tr class="even">
<td><p>description</p></td>
<td><p>The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body.</p>
<p>I.e. the description of the web panel.</p></td>
</tr>
<tr class="odd">
<td><p><a href="#resource">resource</a></p>
<p> </p></td>
<td><p>A resource element is used to provide a web panel with content.</p>
<p>It can be used in a way similar to <a href="https://developer.atlassian.com/display/DOCS/Adding+Resources+to+your+Project">normal resources</a>,</p>
<p>using the resource's location attribute to point to a static HTML file or (Velocity) template file that is provided by the plugin's JAR file.</p>
<p>To differentiate between static HTML and Velocity templates that need to be rendered, always specify the <code>type</code> attribute.</p>
<p>See the examples further down on this page.</p>
<p>It is also possible to embed the contents (both static HTML or velocity) directly in the <code>atlassian-plugin.xml</code> file</p>
<p>by encoding it in the resource element's body and then omitting the <code>location</code> attribute.</p>
<p>Note that if you omit the resource element you MUST provide the module descriptor's <code>class</code> attribute, and vice versa,</p>
<p>to ensure there is always exactly one source for the web panel's content.</p></td>
</tr>
</tbody>
</table>

**\*label element is required.**

 

#### Condition and Conditions Elements

Conditions can be added to the [web section](https://developer.atlassian.com/display/DOCS/Web+Section+Plugin+Module), [web item](https://developer.atlassian.com/display/DOCS/Web+Item+Plugin+Module) and [web panel](https://developer.atlassian.com/display/DOCS/Web+Panel+Plugin+Module) modules, to display them only when **all** the given conditions are true.

Condition elements must contain a class attribute with the fully-qualified name of a Java class. The referenced class:

-   must implement `com.atlassian.plugin.web.Condition`, and
-   will be auto-wired by Spring before any condition checks are performed.

Condition elements can take optional parameters. These parameters will be passed in to the condition's `init()` method as a map of string key/value pairs after autowiring, but before any condition checks are performed. For example:

``` xml
<condition class="com.atlassian.jira.plugin.webfragment.conditions.JiraGlobalPermissionCondition">
    <param name="permission">admin</param>
</condition>
```

NOTE: In versions before JIRA 3.7, this class is called `com.atlassian.jira.plugin.web.conditions.JiraGlobalPermissionCondition`

To invert a condition, add the attribute 'invert="true"' to the condition element. This is useful where you want to show the section if a certain condition is *not* satisfied.  
Conditions elements are composed of a collection of condition/conditions elements and a type attribute. The type attribute defines what logical operator is used to evaluate its collection of condition elements. The type can be one of **AND** or **OR**.

For example: The following condition is true if the current user is a system administrator OR a project administrator:

``` xml
<conditions type="OR">
    <condition class="com.atlassian.jira.plugin.webfragment.conditions.JiraGlobalPermissionCondition">
        <param name="permission">admin</param>
    </condition>
    <condition class="com.atlassian.jira.plugin.webfragment.conditions.UserHasVisibleProjectsCondition">
        <param name="permission">project</param>
    </condition>
</conditions>
```

NOTE: In versions before JIRA 3.7, the second class is called `com.atlassian.jira.plugin.web.conditions.UserHasProjectsCondition`

#### Context-provider Element

|            |                                                                       |
|------------|-----------------------------------------------------------------------|
| Available: | Atlassian Plugins 2.5, Confluence 2.5, Bamboo 3.0, JIRA 4.2 and later |

The `context-provider` element must contain a class attribute with the fully-qualified name of a Java class. The referenced class:The context-provider element adds to the Velocity context available to the [web section](https://developer.atlassian.com/display/DOCS/Web+Section+Plugin+Module) and [web item](https://developer.atlassian.com/display/DOCS/Web+Item+Plugin+Module) modules. You can add what you need to the context, to build more flexible section and item elements. Currently only one context-provider can be specified per module. Additional context-providers are ignored.

-   must implement `com.atlassian.plugin.web.ContextProvider`, and
-   will be auto-wired by Spring before any additions to the Velocity context.

For example, the following context-provider will add `historyWindowHeight` and `filtersWindowHeight` to the context.

In the following example, `HeightContextProvider` extends `AbstractJiraContextProvider`, which is only available in JIRA and happens to implement `ContextProvider`. The `AbstractJiraContextProvider` conveniently extracts the `User` and `JiraHelper` from the context map, which you would otherwise have to do manually.

``` java
public class HeightContextProvider extends AbstractJiraContextProvider
{
    private final ApplicationProperties applicationProperties;

    public HeightContextProvider(ApplicationProperties applicationProperties)
    {
        this.applicationProperties = applicationProperties;
    }

    public Map getContextMap(User user, JiraHelper jiraHelper)
    {
        int historyIssues = 0;
        if (jiraHelper != null && jiraHelper.getRequest() != null)
        {
            UserHistory history = (UserHistory) jiraHelper.getRequest().getSession().getAttribute(SessionKeys.USER_ISSUE_HISTORY);
            if (history != null)
            {
                historyIssues = history.getIssues().size();
            }
        }
        int logoHeight = TextUtils.parseInt(applicationProperties.getDefaultBackedString(APKeys.JIRA_LF_LOGO_HEIGHT));
        String historyHeight = String.valueOf(80 + logoHeight + (25 * historyIssues));
        String filterHeight = String.valueOf(205 + logoHeight);
        return EasyMap.build("historyWindowHeight", historyHeight,
                             "filtersWindowHeight", filterHeight);
    }
}
```

The above `HeightContextProvider` can be used by nesting the following element in a web item module.

``` xml
<context-provider class="com.atlassian.jira.plugin.web.contextproviders.HeightContextProvider" />
```

The newly added context entries `historyWindowHeight` and `filtersWindowHeight` can be used in the XML module descriptors just like normal velocity context variables, by prefixing them with the dollar symbol ($):

``` xml
<!-- pass the value of historyWindowHeight as a parameter called windowHeight (see param element above for its usage) -->
<param name="windowHeight">$historyWindowHeight</param>

<!-- set the link's label to print the value of filtersWindowHeight -->
<label>filter window height is: $filtersWindowHeight</label>
```

#### Label Elements

Label elements may contain optional parameters, as shown below:

``` xml
<label key="common.concepts.create.new.issue">
    <param name="param0">$helper.project.name</param>
</label>
```

-   The parameters allow you to insert values into the label using Java's <a href="http://java.sun.com/j2se/1.4.2/docs/api/java/text/MessageFormat.html" class="external-link">MessageFormat</a> syntax.
-   Parameter names must start with `param` and will be mapped in *alphabetical order* to the substitutions in the format string. I.e. param0 is {0}, param1 is {1}, param2 is {2}, etc.
-   Parameter values are rendered using Velocity, allowing you to include dynamic content.

#### Param Elements

Param elements represent a map of key/value pairs, where each entry corresponds to the param elements attribute: `name` and `value` respectively.

``` xml
<param name="key" value="value" />
```

The value can be retrieved from within the Velocity view with the following code, where $item is a `WebItemModuleDescriptor`:

``` xml
$item.webParams.get("key") <!-- retrieve the value -->
$item.webParams.getRenderedParam("key", $user, $helper) <!-- retrieve the Velocity rendered value -->
```

If the `value` attribute is not specified, the value will be set to the body of the element. I.e. the following two param elements are equivalent:

``` xml
<param name="isPopupLink" value="true" />
<param name="isPopupLink">true</param>
```

#### Resource Element

Unless the module descriptor's `class` attribute is specified, a web panel will contain a single resource child element that contains the contents of the web panel. This can be plain HTML, or a (Velocity) template to provide dynamic content.

A web panel's resource element can either contain its contents embedded in the resource element itself, as part of the `atlassian-plugin.xml` file, or it can link to a file on the classpath when the `location` attribute is used.

A resource element's `type` attribute identifies the format of the panel's content (currently "**static**" and "**velocity**" are provided by Atlassian Plugin Framework 2.5.0 and atlassian-template-renderer 2.5.0 respectively) which allows the plugin framework to use the appropriate <a href="https://studio.atlassian.com/source/browse/PLUG/trunk/atlassian-plugins-webfragment/src/main/java/com/atlassian/plugin/web/renderer/WebPanelRenderer.java?r=56664" class="external-link">com.atlassian.plugin.web.renderer.WebPanelRenderer</a>.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Type</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><strong>static</strong></p></td>
<td><p>Used to indicate that the web panel's contents must not be processed, but included in the page as is.</p></td>
</tr>
<tr class="even">
<td><p><strong>velocity</strong></p></td>
<td><p>Used to indicate that the web panel contains <a href="http://velocity.apache.org" class="external-link">Velocity markup</a> that needs to be parsed.</p></td>
</tr>
</tbody>
</table>

The template rendering system is extensible. You can add custom renderers by creating plugins. For more information on this, check out the [Web Panel Renderer Plugin Module](https://developer.atlassian.com/display/DOCS/Web+Panel+Renderer+Plugin+Module).

## Web Panel Examples

NOTE: The values of the `location` attributes in the examples below are not real. They are just illustrative of the kind of location that Confluence, Bamboo and FishEye make available.

A web panel that contains static, embedded HTML:

``` xml
       <web-panel key="myPanel" location="atl.confluence.comments">
           <resource name="view" type="static"><![CDATA[<b>Hello World!</b>]]></resource>
       </web-panel>
```

A web panel that contains an embedded Velocity template:

``` xml
       <web-panel key="myPanel" location="atl.bamboo.buildplan">
           <resource name="view" type="velocity"><![CDATA[#set($name = 'foo')My name is $name]]></resource>
       </web-panel>
```

A web panel containing a Velocity template that is on the classpath (part of the plugin's JAR file):

``` xml
       <web-panel key="myPanel" location="atl.fisheye.annotatedfile">
           <resource name="view" type="velocity" location="templates/pie.vm"/>
       </web-panel>
```

As mentioned previously, it is also possible to provide your own custom class that is responsible for producing the panel's HTML, by using the descriptor's class attribute (which makes the resource element redundant):

``` xml
       <web-panel key="myPanel" location="atl.crucible.dashboard" class="com.example.FooWebPanel">
```

Note that `com.example.FooWebPanel` MUST implement <a href="https://studio.atlassian.com/source/browse/PLUG/trunk/atlassian-plugins-webfragment/src/main/java/com/atlassian/plugin/web/model/WebPanel.java?r=56850" class="external-link">WebPanel</a>.

## Application-Specific Locations

Each host application declares its own set of locations where the web panel can be rendered. Please refer to the documentation for each application:

-   Confluence: [Web Panel Plugin Module](https://developer.atlassian.com/display/CONFDEV/Web+Panel+Plugin+Module)
-   JIRA: [Web Panel Plugin Module](https://developer.atlassian.com/display/JIRADEV/Web+Panel+Plugin+Module)

##### RELATED TOPICS

[Web Panel Renderer Plugin Module](/server/framework/atlassian-sdk/web-panel-renderer-plugin-module-852106.html)  
[Plugin Modules](/server/framework/atlassian-sdk/plugin-modules-852136.html)

























