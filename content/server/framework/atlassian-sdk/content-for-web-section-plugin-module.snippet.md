---
aliases:
- /server/framework/atlassian-sdk/-content-for-web-section-plugin-module-852114.html
- /server/framework/atlassian-sdk/-content-for-web-section-plugin-module-852114.md
category: devguide
confluence_id: 852114
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852114
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852114
date: '2017-12-08'
legacy_title: _Content for Web Section Plugin Module
platform: server
product: atlassian-sdk
subcategory: other
title: _Content for Web Section Plugin Module
---
# \_Content for Web Section Plugin Module

## Purpose of this Module Type

Web Section plugin modules allow plugins to define new sections in application menus. Each section can contain one or more links. To insert the links themselves, see the [Web Item Plugin Module](/server/framework/atlassian-sdk/web-item-plugin-module).

## Configuration

The root element for the Web Section plugin module is `web-section` It allows the following attributes and child elements for configuration:

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
<td>The class which implements this plugin module. The class you need to provide depends on the module type. For example, Confluence theme, layout and colour-scheme modules can use classes already provided in Confluence. So you can write a theme-plugin without any Java code. But for macro and listener modules you need to write your own implementing class and include it in your plugin. See the plugin framework guide to <a href="https://developer.atlassian.com/display/DOCS/Creating+Plugin+Module+Instances">creating plugin module instances</a>.</td>
</tr>
<tr class="even">
<td><p>state</p></td>
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
<td><p>The human-readable name of the plugin module. Only used in the plugin's administrative user interface.</p></td>
</tr>
<tr class="even">
<td><p>location</p></td>
<td><p>The <a href="https://developer.atlassian.com/display/JIRADEV/Web+Fragments#WebFragments-Locations">location</a> into which this web item should be placed.</p></td>
</tr>
<tr class="odd">
<td><p>system</p>
<p> </p></td>
<td><p>Indicates whether this plugin module is a system plugin module (value='true') or not (value='false'). Only available for non-OSGi plugins.</p>
<p><strong>Default:</strong> false.</p></td>
</tr>
<tr class="even">
<td><p>weight</p></td>
<td><h6 id="id-_ContentforWebSectionPluginModule-weightattrWeightattribute">Weight attribute</h6>
<p>Determines the order in which web items appear. Items are displayed top to bottom or left to right in order of ascending weight. The 'lightest' weight is displayed first, the 'heaviest' weights sink to the bottom. The weights for most applications' system sections start from 100, and the weights for their links generally start from 10. The weight is incremented by 10 for each in sequence so that there is ample space to insert your own sections and links.</p></td>
</tr>
</tbody>
</table>

**\*key, location, weight attributes are required.**

#### Elements

The table summarises the elements. The sections below contain further information.

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
<td><p>condition</p></td>
<td><p>Defines a condition that must be satisfied for the web item to be displayed. If you want to 'invert' a condition, add an attribute 'invert=&quot;true&quot;' to it. The web item will then be displayed if the condition returns false (not true). More below (<a href="http://developer.atlassian.com#conditionElements" class="external-link">Condition and Conditions elements</a>).</p></td>
</tr>
<tr class="even">
<td><p>conditions</p></td>
<td><p>Defines the logical operator type used to evaluate the condition elements. By default 'AND' will be used. More below (<a href="https://developer.atlassian.com/http:/#conditionElements">Condition and Conditions elements</a>).</p>
<p><strong>Default:</strong> AND.</p></td>
</tr>
<tr class="odd">
<td><p>context-provider</p></td>
<td><p>Allows dynamic addition to the Velocity context available for various web item elements (in XML descriptors only). Currently only one context-provider can be specified per web item and section. More below (<a href="#context-provider">Context-provider</a>)</p></td>
</tr>
<tr class="even">
<td><p>description</p></td>
<td><p>The description of the plugin module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body. Use this element to describe the section.</p></td>
</tr>
<tr class="odd">
<td><p>label</p></td>
<td><p>Is the i18n key that will be used to look up the textual representation of the link. More below (<a href="#label">Label</a>).</p></td>
</tr>
<tr class="even">
<td><p>param</p></td>
<td><p>Parameters for the plugin module. Use the 'key' attribute to declare the parameter key, then specify the value in either the 'value' attribute or the element body. This element may be repeated. An example is the configuration link described in <a href="https://developer.atlassian.com/display/DOCS/Adding+a+Configuration+UI+for+your+Plugin">Adding a Configuration UI for your Plugin</a>. Defines a key/value pair available from the web item. This is handy if you want to use additional custom values from the UI. More below (<a href="#param">Param</a>).</p></td>
</tr>
<tr class="odd">
<td><p>resource</p></td>
<td>A resource for this plugin module. This element may be repeated. A 'resource' is a non-Java file that a plugin may need in order to operate. Refer to <a href="https://developer.atlassian.com/display/DOCS/Adding+Resources+to+your+Project">Adding Resources to your Project</a> for details on defining a resource.</td>
</tr>
<tr class="even">
<td><p>tooltip</p></td>
<td><p>Is the i18n key that will be used to look up the textual mouse-over text of the link. More below (<a href="#tooltip">Tooltip</a>).</p></td>
</tr>
</tbody>
</table>

**\*label element is required.**

####  Label 

Label elements may contain optional parameters, as shown below:

``` xml
<label key="common.concepts.create.new.issue">
    <param name="param0">$helper.project.name</param>
</label>
```

-   The parameters allow you to insert values into the label using Java's <a href="http://java.sun.com/j2se/1.4.2/docs/api/java/text/MessageFormat.html" class="external-link">MessageFormat</a> syntax.
-   Parameter names must start with `param` and will be mapped in *alphabetical order* to the substitutions in the format string. I.e. param0 is {0}, param1 is {1}, param2 is {2}, etc.
-   Parameter values are rendered using Velocity, allowing you to include dynamic content.

#### Tooltip 

Tooltip elements have the same attributes and parameters as the label elements. See [above](#label).

#### Param

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

#### Context-provider

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

#### Condition and Conditions elements

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

Here is an example `atlassian-plugin.xml` file containing a single web section, using a condition that will be available in JIRA:

``` xml
<atlassian-plugin name="Hello World Plugin" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic web section module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <web-section key="usersgroups" name="Users and Groups Section" location="system.admin" weight="110">
        <label key="admin.menu.usersandgroups.users.and.groups" />
        <condition class="com.atlassian.jira.plugin.webfragment.conditions.UserIsAdminCondition" />
    </web-section>
</atlassian-plugin>
```

NOTE: In versions before JIRA 3.7, this class is called `com.atlassian.jira.plugin.web.conditions.UserIsAdminCondition`
