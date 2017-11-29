---
aliases:
- /server/framework/atlassian-sdk/troubleshooting-speakeasy-2818156.html
- /server/framework/atlassian-sdk/troubleshooting-speakeasy-2818156.md
category: devguide
confluence_id: 2818156
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818156
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818156
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/speakeasy/troubleshooting-speakeasy
new_url: /server/framework/atlassian-sdk/troubleshooting-speakeasy
platform: server
product: atlassian-sdk
subcategory: learning
title: Troubleshooting Speakeasy
---
# Troubleshooting Speakeasy

The following are problems that may occur with Speakeasy and their solution:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p><strong>Problem</strong></p></th>
<th><p><strong>Solution</strong></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>User can't access the Speakeasy page due to a rogue extension</p></td>
<td><p>Have the user visit<br />
</p>
<div class="panel preformatted" style="border-width: 1px;">
<div class="preformattedContent panelContent">
<pre><code>http://THE_SERVER_URL/plugins/servlet/speakeasy/unsubscribe</code></pre>
</div>
</div>
<p><br />
to be removed from all Speakeasy extension access lists</p></td>
</tr>
<tr class="even">
<td><p>User is having UI issues that may be due to a Speakeasy extension</p></td>
<td><p>If the user knows the probable extension, they can visit the Speakeasy page in their user profile and disable it. Otherwise, they can use the unsubscribe URL listed above to automatically unsubscribe from all Speakeasy extensions</p></td>
</tr>
<tr class="odd">
<td><p>Speakeasy has a bug and one of the extensions is polluting the UI for everyone</p></td>
<td><p>First, try to disable the Speakeasy extension by disabling its plugin in the UPM. If that doesn't work, you can disable Speakeasy itself also in the UPM. When you re-enable Speakeasy, all user extension subscriptions will be preserved.</p></td>
</tr>
<tr class="even">
<td><p>After upgrading Speakeasy, some extensions are missing</p></td>
<td><p>The plugin system has a bug that prevents Speakeasy from being upgraded by simply installing the new version. You have to explicitly uninstall the previous Speakeasy plugin then install the upgraded jar.</p></td>
</tr>
</tbody>
</table>










































































































