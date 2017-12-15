---
aliases:
- /server/framework/atlassian-sdk/-content-for-web-item-plugin-module-852066.html
- /server/framework/atlassian-sdk/-content-for-web-item-plugin-module-852066.md
category: devguide
confluence_id: 852066
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852066
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852066
date: '2017-12-08'
legacy_title: _Content for Web Item Plugin Module
platform: server
product: atlassian-sdk
subcategory: other
title: _Content for Web Item Plugin Module
---
# \_Content for Web Item Plugin Module

## Purpose of this Module Type

Web Item plugin modules allow plugins to define new links in application menus.

## Configuration

The root element for the Web Item plugin module is `web-item`. It allows the following attributes and child elements for configuration:

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
<td><p>The class which implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>.</p></td>
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
<p>Used only in the plugin's administrative user interface.</p></td>
</tr>
<tr class="even">
<td>section</td>
<td><p>Location into which this web item should be placed.</p>
<p>For non-sectioned locations, this is just the location key.</p>
<p>For sectioned locations it is the location key, followed by a slash ('/'),</p>
<p> and the name of the web section in which it should appear.</p></td>
</tr>
<tr class="odd">
<td><p>system</p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
<tr class="even">
<td><p>weight</p>
<p> </p></td>
<td><p>Determines the order in which web items appear.</p>
<p>Items are displayed top to bottom or left to right in order of ascending weight.</p>
<p>The 'lightest' weight is displayed first, the 'heaviest' weights sink to the bottom.</p>
<p>The weights for most applications' system sections start from 100,</p>
<p>and the weights for the links generally start from 10.</p>
<p>The weight is incremented by 10 for each in sequence so that there is ample space to insert your own sections and links.</p>
<p><strong>Default:</strong> 1000.</p></td>
</tr>
</tbody>
</table>

**\*key and section attributes are required.**

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
<td><p><a href="#condition-and-conditions-elements">condition</a></p></td>
<td><p>Defines a condition that must be satisfied for the web panel to be displayed.</p>
<p>If you want to 'invert' a condition, add an attribute 'invert=&quot;true&quot;' to it.</p>
<p>The web item will then be displayed if the condition returns false (not true).</p></td>
</tr>
<tr class="even">
<td><p><a href="#condition-and-conditions-elements">conditions</a></p>
<p> </p></td>
<td><p>Defines the logical operator type to evaluate its condition elements. By default 'AND' will be used.</p>
<p><strong>Default:</strong> AND.</p></td>
</tr>
<tr class="odd">
<td><p><a href="#context-provider-element">context-provider</a></p></td>
<td><p>Allows dynamic addition to the Velocity context available for various web panel elements (in XML descriptors only).</p>
<p>Currently only one context-provider can be specified per web panel.</p></td>
</tr>
<tr class="even">
<td>description</td>
<td><p>The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body. </p>
<p>I.e. the description of the web item.</p></td>
</tr>
<tr class="odd">
<td><a href="#icon-elements">icon</a></td>
<td><p>Defines an icon to display with or as the link.</p>
<p> <strong>Note:</strong> In some cases the icon element is required.</p>
<p>Try adding it if your web section is not displaying properly.</p></td>
</tr>
<tr class="even">
<td><p><a href="#label-elements">label</a></p></td>
<td>Is the i18n key that will be used to look up the textual representation of the link.</td>
</tr>
<tr class="odd">
<td><a href="#link-elements">link</a></td>
<td><p>Defines where the web item should link to.</p>
<p>The contents of the link element will be rendered using Velocity, allowing you to put dynamic content in links.</p>
<p>For more complex examples of links, see <a href="#link-elements">below</a>.</p></td>
</tr>
<tr class="even">
<td><p><a href="#param-elements">param</a></p></td>
<td><p>Parameters for the plugin module. Use the 'key' attribute to declare the parameter key, then specify the value in either the 'value' attribute or the element body. This element may be repeated. An example is the configuration link described in <a href="https://developer.atlassian.com/display/DOCS/Adding+a+Configuration+UI+for+your+Plugin">Adding a Configuration UI for your Plugin</a>.</p>
<p>This is handy if you want to use additional custom values from the UI.</p></td>
</tr>
<tr class="odd">
<td><p>description</p></td>
<td><p>The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body.</p>
<p>I.e. the description of the web panel.</p></td>
</tr>
<tr class="even">
<td><p><a href="#resource">resource</a></p>
<p> </p></td>
<td><p>A resource for this plugin module. This element may be repeated. A 'resource' is a non-Java file that a plugin may need in order to operate. Refer to <a href="https://developer.atlassian.com/display/DOCS/Adding+Resources+to+your+Project">Adding Resources to your Project</a> for details on defining a resource.</p></td>
</tr>
<tr class="odd">
<td>styleClass</td>
<td><p>Defines an additional CSS class that will added to this web item when it is rendered on the page.</p>
<p>Note that this value may be ignored in some situations.</p></td>
</tr>
<tr class="even">
<td><a href="#tooltip-elements">tooltip</a></td>
<td>Is the i18n key that will be used to look up the textual mouse-over text of the link.</td>
</tr>
</tbody>
</table>

**\*label and link elements are required.**

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

#### Tooltip Elements

Tooltip elements have the same attributes and parameters as the label elements. See [above](#label-elements).

#### Link Elements

Link elements may contain additional information:

``` xml
<link linkId="create_link" absolute="false">/secure/CreateIssue!default.jspa</link>
```

-   The `linkId` is **optional**, and provides an XML id for the link being generated.
-   The `absolute` is **optional** and defaults to false unless the link starts with `http://` or `https://`

The body of the link element is its URL. The URL is rendered with Velocity, so you can include dynamic information in the link. For example, in Confluence, the following link would include the page ID:

``` xml
<link linkId="view-attachments-link">/pages/viewpageattachments.action?pageId=$page.id</link>
```

#### Icon Elements

Icon elements have a `height` and a `width` attribute. The location of the icon is specified within a [link](#link-elements) element:

``` xml
<icon height="16" width="16">
    <link>/images/icons/print.gif</link>
</icon>
```

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

## Example

### Single web item in the admin section

Here is an example `atlassian-plugin.xml` file containing a single web item:

``` xml
<atlassian-plugin name="Hello World Plugin" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic web item module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <web-item key="google_home" name="Google Home" section="system.admin/example1" weight="10">
        <description key="item.google.home.desc">Simple link to google.com.</description>
        <label key="item.google.home.label" />
        <link linkId="google_home">http://google.com</link>
    </web-item>
</atlassian-plugin>
```

## Add a web item to the application header bar

Here is an example `atlassian-plugin.xml` file containing how to add your link to the application header.

![](/server/framework/atlassian-sdk/images/screen-shot-2013-06-11-at-2.57.27-pm.png)

``` xml
<atlassian-plugin name="Hello World Plugin" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic web item module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <web-item key="google_home" name="Google Home" section="system.header/left" weight="60">
        <description key="item.google.home.desc">Simple link to google.com.</description>
        <label key="item.google.home.label" />
        <link linkId="google_home">http://google.com</link>
    </web-item>
</atlassian-plugin>
```
