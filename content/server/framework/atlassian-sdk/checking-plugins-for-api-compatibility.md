---
aliases:
- /server/framework/atlassian-sdk/checking-plugins-for-api-compatibility-6291602.html
- /server/framework/atlassian-sdk/checking-plugins-for-api-compatibility-6291602.md
category: devguide
confluence_id: 6291602
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=6291602
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=6291602
date: '2017-12-08'
guides: guides
legacy_title: Checking Plugins for API Compatibility
platform: server
product: atlassian-sdk
subcategory: learning
title: Checking Plugins for API Compatibility
---
# Checking Plugins for API Compatibility

{{% warning %}}

The Atlassian Plugin Checkup tool has been retired from service, you can read more about [Checkup's retirement](https://developer.atlassian.com/blog/2015/02/retiring-checkup/).

{{% /warning %}}

 

The <a href="http://checkup.atlassian.com/" class="external-link">Atlassian Plugin Checkup</a> lets you test your plugin's compatibility with different versions of our products. It helps you identify API changes between versions of a product. 

## Running the Atlassian Plugin Checkup

To use the Atlassian Plugin Checkup tool:

1.  Go to <a href="http://checkup.atlassian.com" class="external-link">http://checkup.atlassian.com.</a>
2.  Upload the JAR file that contains the plugin you want to check. You can load the JAR from a network location, by URL, or directly from your file system.
3.  Choose an Atlassian product and version.
4.  Run the report for the version.
5.  Fix your plugin to clear any warnings given by the checkup report.

## Reading the Checkup Report

The checkup tool produces an online report showing a list of methods, parameters and other components that the plugin references in the Atlassian product. The report indicates the components that are:

-   Unavailable in the given version of the given product.
-   Deprecated.
-   Part of an internal interface.
-   Part of the stable, public API.

Below is a more detailed description of each of the categories, including guidelines on what you can do to fix the problem.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Category</p></th>
<th><p>Description</p></th>
<th><p>What to Do</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Unavailable</p></td>
<td><p>The plugin refers to components that do not exist in the given version of the given Atlassian product.</p></td>
<td><p>Change the plugin so that it does not refer to these methods, parameters or other components. Check the product's <a href="https://developer.atlassian.com/static/">reference documentation</a> to see the available interfaces, and read through the product release notes and developer release notes for previous releases to see when the component was removed and what the recommended replacement is.</p></td>
</tr>
<tr class="even">
<td><p>Deprecated</p></td>
<td><p>The plugin refers to components that have been deprecated, and will likely be removed in the next major version of the Atlassian product.</p></td>
<td><p>Check the product's <a href="https://developer.atlassian.com/static/">reference documentation</a> to see when and why the component was deprecated, and what the recommended replacement is. Read through the recent product release notes and developer release notes for more information on the changes. Update the plugin as soon as possible.</p></td>
</tr>
<tr class="odd">
<td><p>Private</p></td>
<td><p>The plugin refers to an internal class, interface or other component that is not part of the stable, public API. The referenced component may change in a future version of the Atlassian product. This may break your plugin.<br />
<em>Note:</em> Currently only JIRA 5.0 is able to distinguish between internal components and public APIs. For all the other products, and for earlier versions of JIRA, all the available components will appear on this tab.</p></td>
<td><p>If you are not using JIRA 5.0, there is no need to take any action.<br />
If you are using JIRA 5.0, you should change the plugin to use the public APIs where possible. See <a href="https://developer.atlassian.com/display/JIRADEV/Preparing+for+JIRA+5.0">Preparing for JIRA 5.0</a>.</p></td>
</tr>
<tr class="even">
<td><p>Valid</p></td>
<td><p>These references made by your plugin are public, and are guaranteed not to change before the next major version of the Atlassian product.<br />
<em>Note:</em> This tab will be empty for all products except JIRA 5.0. If you are not using JIRA 5.0, it's OK if there are no components listed here. If you are using JIRA 5.0, there should be a lot of information on this tab.</p></td>
<td><p>All good. No action required.</p></td>
</tr>
</tbody>
</table>

### More Resources for Finding What Has Changed

If you cannot resolve an API compatibility problem, try searching <a href="https://answers.atlassian.com" class="external-link">Atlassian Answers</a>. If no one has asked the question yet, add the question, giving it <a href="https://answers.atlassian.com/browse_tags/" class="external-link">appropriate tags</a>.

## Coming Back to View the Report Again

The report remains available until someone generates it again for the same plugin and product version. You can bookmark the URL to view the report later.

## References Checked by the Atlassian Plugin Checkup

The checkup tool checks all references made by the plugin to the following components:

-   Method calls
-   Method parameters
-   Types in method parameters and return types
-   Interface and class implementations and extensions
-   Annotations
-   Fields

















































































































































































































































































































