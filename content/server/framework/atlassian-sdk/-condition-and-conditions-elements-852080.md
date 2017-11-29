---
title: Condition and Conditions Elements 852080
aliases:
    - /server/framework/atlassian-sdk/-condition-and-conditions-elements-852080.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852080
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852080
confluence_id: 852080
platform:
product:
category:
subcategory:
---
# Documentation : \_Condition and Conditions Elements

Conditions can be added to the [web section](/server/framework/atlassian-sdk/web-section-plugin-module-852133.html), [web item](/server/framework/atlassian-sdk/web-item-plugin-module-852014.html) and [web panel](/server/framework/atlassian-sdk/web-panel-plugin-module-852000.html) modules, to display them only when **all** the given conditions are true.

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

























