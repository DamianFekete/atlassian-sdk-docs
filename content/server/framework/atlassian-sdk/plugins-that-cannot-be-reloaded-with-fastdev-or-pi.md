---
aliases:
- /server/framework/atlassian-sdk/plugins-that-cannot-be-reloaded-with-fastdev-or-pi-2818391.html
- /server/framework/atlassian-sdk/plugins-that-cannot-be-reloaded-with-fastdev-or-pi-2818391.md
category: devguide
confluence_id: 2818391
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818391
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818391
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/advanced-plugin-development-faq/plugins-that-cannot-be-reloaded-with-fastdev-or-pi
new_url: /server/framework/atlassian-sdk/plugins-that-cannot-be-reloaded-with-fastdev-or-pi
platform: server
product: atlassian-sdk
subcategory: other
title: Plugins that cannot be reloaded with FastDev or pi
---
# Plugins that cannot be reloaded with FastDev or pi

{{% warning %}}

FastDev and atlas-cli have been deprecated. Please use [Automatic Plugin Reinstallation with QuickReload](https://developer.atlassian.com/docs/developer-tools/automatic-plugin-reinstallation-with-quickreload) instead.

{{% /warning %}}

 

During development it is useful to use FastDev or the maven-cli `pi` command to reload a plugin in an actively running application, to provide rapid testing of changes. See [Reloading a Plugin after Changes](/server/framework/atlassian-sdk/reloading-a-plugin-after-changes-2818373.html).

However, plugin modules can be marked with a `@RequiresRestart` annotation which means the plugin will not be reloaded until the application server is restarted. This means that the `pi` command does not work for these plugins.

Below is a list of plugin modules indicating if they require a restart or not.

## JIRA

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Module Type</p></th>
<th><p>Can be reloaded</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Component</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>ComponentImport</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="odd">
<td><p>ComponentTabPanel</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>CustomFieldSearcher</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>CustomFieldType</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>Gadget</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="odd">
<td><p>IssueOperation</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>IssueTabPanel</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>JQLFunction</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>ModuleType</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="odd">
<td><p>Portlet</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>ProjectTabPanel</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>Report</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>Resource</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="odd">
<td><p>REST</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="even">
<td><p>RPC-SOAP</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>RPC-XMLRPC</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>SearchRequestView</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>ServletContextListener</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="even">
<td><p>ServletContextParameter</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="odd">
<td><p>ServletFilter</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="even">
<td><p>Servlet</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="odd">
<td><p>UserFormat</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>VersionTabPanel</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>WebItem</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="even">
<td><p>WebResource</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="odd">
<td><p>WebSection</p></td>
<td><p><strong>Yes</strong></p></td>
</tr>
<tr class="even">
<td><p>Webwork</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>WorkflowCondition</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>WorkflowFunction</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>WorkflowValidator</p></td>
<td><p><strong>No</strong></p></td>
</tr>
</tbody>
</table>

## Confluence

**All modules except Component will be reloaded**

## Bamboo

Everything not listed here can be reloaded.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Module Type</p></th>
<th><p>Can be reloaded</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Component</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>BuildAgentRequirementFilter</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>CapabilityConfiguratorModule</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>CustomIndexReaderModule</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>CustomPostBuildIndexModule</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>CustomPreBuildQueuedActionModule</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>LegacyBuilderToTaskConverter</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>NotificationTypeModule</p></td>
<td><p><strong>Yes</strong> Bamboo &gt;=4.1</p></td>
</tr>
<tr class="odd">
<td><p>PlanDeletionInterceptorActionModule</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>RepositoryModule</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="odd">
<td><p>SpringComponentModule</p></td>
<td><p><strong>No</strong></p></td>
</tr>
<tr class="even">
<td><p>TriggerReasonModule</p></td>
<td><p><strong>No</strong></p></td>
</tr>
</tbody>
</table>

## Fisheye/Crucible

*Information to be completed*. Component will not be reloaded.

## Other information

-   See <a href="http://jira.atlassian.com/browse/JRA-19242" class="uri external-link">http://jira.atlassian.com/browse/JRA-19242</a>















































































