---
aliases:
- /server/framework/atlassian-sdk/-plugin-module-matrix-851990.html
- /server/framework/atlassian-sdk/-plugin-module-matrix-851990.md
category: devguide
confluence_id: 851990
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851990
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851990
date: '2017-12-08'
legacy_title: _Plugin Module Matrix
platform: server
product: atlassian-sdk
subcategory: other
title: _Plugin Module Matrix
---
# \_Plugin Module Matrix

The matrix below lists the Atlassian applications and shows which plugin module types each application supports, assuming that the application supports version 2 of the Plugin Framework. The applications are listed horizontally across the top and the plugin module types are listed vertically on the left. The vertical list also includes miscellaneous other items of interest.

-   Version numbers next to the YES word show the **earliest release** of the application which supports the relevant module type.
-   Version numbers in brackets show a future release expected to support the relevant module type.

{{% note %}}

Not all plugin types are shown

The matrix below applies only to applications which support the Plugin Framework 2.0 and later. Also, it shows only the module types which are part of the common Plugin Framework 2.x, not those which are unique to a particular application.

{{% /note %}}

<table style="width:100%;">
<colgroup>
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
<col style="width: 14%" />
</colgroup>
<thead>
<tr class="header">
<th><p> </p></th>
<th><p>Plugin Reference Implementation</p></th>
<th><p>Confluence</p></th>
<th><p>JIRA</p></th>
<th><p>FishEye/Crucible</p></th>
<th><p>Crowd</p></th>
<th><p>Bamboo</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Component Import Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.6</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Component Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
1.6</p></td>
<td><p>YES<br />
1.5</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Module Type Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.6</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Servlet Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
1.6</p></td>
<td><p>YES<br />
1.5</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Servlet Filter Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.6</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Servlet Listener Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.6</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Servlet Parameter Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.6</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Web Resource Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
1.6</p></td>
<td><p>YES<br />
1.6</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Web Item Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.5</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Web Section Plugin Module</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.5</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>UI Toolbox decorators</p></td>
<td><p>YES</p></td>
<td><p>YES<br />
2.10</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.6</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Dynamic plugin support</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p> </p></td>
<td><p>YES<br />
2.0</p></td>
<td><p>YES<br />
1.6</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

Other useful version matrices:

-   [Shared Access Layer (SAL)](/server/framework/atlassian-sdk/sal-version-matrix)
-   <a href="http://confluence.atlassian.com/display/APPLINKS/Application+Links+Version+Matrix" class="external-link">Application Links (AppLinks)</a>
