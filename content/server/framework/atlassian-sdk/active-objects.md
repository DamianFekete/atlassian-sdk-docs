---
aliases:
- /server/framework/atlassian-sdk/active-objects-5669125.html
- /server/framework/atlassian-sdk/active-objects-5669125.md
category: devguide
confluence_id: 5669125
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669125
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669125
date: '2017-12-08'
guides: guides
legacy_title: Active Objects
platform: server
product: atlassian-sdk
subcategory: learning
title: Active Objects
---
# Active Objects

Active Objects is a new ORM (object relational mapping) layer into Atlassian products. Active Objects is implemented as a plugin into Atlassian applications. It enables easier, faster, and more scalable data access and storage than the existing Bandana and PluginSettings APIs.

The goal of the Active Objects plugin is to provide a **plugin data storage component** that plugins can and should use to persist their private data. Active Objects satisfies these requirements:

<table>
<colgroup>
<col style="width: 30%" />
<col style="width: 70%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Real database</p></td>
<td><p>Instead of using a key/value store to mimic a relational database, Active Objects provides plugin developers with access to a real database.</p></td>
</tr>
<tr class="even">
<td><p>Database independence</p></td>
<td><p>Active Objects abstracts all database implementation details. The specific underlying database implementation that Active Objects provides should not have any effect on the plugin's implementation, as each product supports multiple databases.</p></td>
</tr>
<tr class="odd">
<td><p>ORM interface</p></td>
<td><p>The ORM interface bundled with Active Objects allows plugin developers to avoid many common issues and tedious boilerplate code involved in issuing queries, creating schemas and performing migrations between schema versions.</p></td>
</tr>
<tr class="even">
<td><p>Sandboxing</p></td>
<td><p>A plugin can access only the data that belongs to it, not data belonging to other plugins or to the host products.</p></td>
</tr>
<tr class="odd">
<td><p>Backup/restore</p></td>
<td><p>The product's existing database backup/restore (or export/import) mechanisms take care of backing up the plugin data. <em>Note:</em> Backup/restore is fully integrated with JIRA 5.0, but is not yet integrated with all products. Beware of this detail when developing an Active Objects plugin or using another plugin that uses Active Objects.</p></td>
</tr>
</tbody>
</table>

## Getting Started

-   [Installing Active Objects](/server/framework/atlassian-sdk/installing-active-objects)
-   [AO 0.18.x Upgrade Guide](/server/framework/atlassian-sdk/ao-0-18-x-upgrade-guide)
-   [Getting Started with Active Objects](/server/framework/atlassian-sdk/getting-started-with-active-objects)
-   [Developing your plugin with Active Objects](/server/framework/atlassian-sdk/developing-your-plugin-with-active-objects)
-   [AO 1.0.0 Upgrade Guide](/server/framework/atlassian-sdk/ao-1-0-0-upgrade-guide)
-   [AO 1.1.0 Upgrade Guide](/server/framework/atlassian-sdk/ao-1-1-0-upgrade-guide)
-   [AO 1.2.0 Upgrade Guide](/server/framework/atlassian-sdk/ao-1-2-0-upgrade-guide)
-   [Handling AO Upgrade Tasks](/server/framework/atlassian-sdk/handling-ao-upgrade-tasks)

## Feedback

Please log any issues and requests in our <a href="https://ecosystem.atlassian.net/browse/AO" class="external-link">issue tracker</a>.
