---
aliases:
- /server/framework/atlassian-sdk/-version-compatibility-852030.html
- /server/framework/atlassian-sdk/-version-compatibility-852030.md
category: devguide
confluence_id: 852030
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852030
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852030
date: '2017-12-08'
legacy_title: _Version Compatibility
platform: server
product: atlassian-sdk
subcategory: other
title: _Version Compatibility
---
# \_Version Compatibility

Almost every Atlassian application has a version of the Atlassian Plugin Framework. However, they may not all have the same version. If you are developing a plugin, you need to know what your version is capable of, and how it will interact with other versions.

{{% note %}}

The Atlassian Plugin Framework 2 is available in all current Atlassian applications, but may not be available in some older versions.

 

{{% /note %}}

The table below matches the application versions with Plugin Framework versions:

-   Version numbers without brackets show the **earliest** release of the application which supports the relevant framework version.
-   Version numbers in brackets show a future application release expected to support the relevant framework version.

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 12%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Plugin Framework</p></th>
<th><p>Bamboo</p></th>
<th><p>Confluence</p></th>
<th><p>Crowd</p></th>
<th><p>Crucible</p></th>
<th><p>FishEye</p></th>
<th><p>JIRA</p></th>
<th><p>Bitbucket Server<br />
(formerly Stash) </p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>2.0</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%201.5%20Release%20Notes" class="external-link">Crowd 1.5</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%201.6%20Release%20Notes" class="external-link">Crucible 1.6</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%201.6%20Release%20Notes" class="external-link">FishEye 1.6</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>2.1</p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/CONF210/Confluence%202.10%20Release%20Notes" class="external-link">Confluence 2.10</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%201.6%20Release%20Notes" class="external-link">Crowd 1.6</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>2.2</p></td>
<td><p><a href="http://confluence.atlassian.com/display/BAMBOO/Bamboo%202.3%20Release%20Notes" class="external-link">Bamboo 2.3</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.0%20Release%20Notes" class="external-link">Confluence 3.0</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.0%20Release%20Notes" class="external-link">Crowd 2.0</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.0%20Release%20Notes" class="external-link">Crucible 2.0</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%202.0%20Release%20Notes" class="external-link">FishEye 2.0</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>2.3</p></td>
<td><p><a href="http://confluence.atlassian.com/display/BAMBOO/Bamboo%202.4%20Release%20Notes" class="external-link">Bamboo 2.4</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.1%20Release%20Notes" class="external-link">Crucible 2.1</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%202.1%20Release%20Notes" class="external-link">FishEye 2.1</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA040/JIRA%204.0%20Release%20Notes" class="external-link">JIRA 4.0</a></p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>2.4</p></td>
<td><p><a href="http://confluence.atlassian.com/display/BAMBOO/Bamboo%202.5%20Release%20Notes" class="external-link">Bamboo 2.5</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.1%20Release%20Notes" class="external-link">Confluence 3.1</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.1%20Release%20Notes" class="external-link">Crowd 2.1</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.2%20Release%20Notes" class="external-link">Crucible 2.2</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%202.2%20Release%20Notes" class="external-link">FishEye 2.2</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA041/JIRA%204.1%20Release%20Notes" class="external-link">JIRA 4.1</a></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>2.5</p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.3%20Release%20Notes" class="external-link">Confluence 3.3</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA042/JIRA%204.2%20Release%20Notes" class="external-link">JIRA 4.2</a></p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>2.6</p></td>
<td><p><a href="http://confluence.atlassian.com/display/BAMBOO/Bamboo%202.7%20Release%20Notes" class="external-link">Bamboo 2.7</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.4%20Release%20Notes" class="external-link">Confluence 3.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.2.2%20Release%20Notes" class="external-link">Crowd 2.2</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.4%20Release%20Notes" class="external-link">Crucible 2.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%202.4%20Release%20Notes" class="external-link">FishEye 2.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA043/JIRA%204.3%20Release%20Notes" class="external-link">JIRA 4.3</a></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>2.7</p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.5%20Release%20Notes" class="external-link">Confluence 3.5</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>2.8</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.3.1%20Release%20Notes" class="external-link">Crowd 2.3</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.4%20Release%20Notes" class="external-link">JIRA 4.4</a></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>2.9</p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%204.0%20Release%20Notes" class="external-link">Confluence 4.0</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>2.10</p></td>
<td><p>(Bamboo 3.4)</p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%204.1%20Release%20Notes" class="external-link">Confluence 4.1</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA+5.0+Release+Notes" class="external-link">JIRA 5.0</a></p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>2.11</p></td>
<td><p>Bamboo 4.0</p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%204.2%20Release%20Notes" class="external-link">Confluence 4.2</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>2.12</p></td>
<td><p>Bamboo 4.1</p></td>
<td><p><a href="https://confluence.atlassian.com/display/DOC/Confluence+4.3+Release+Notes" class="external-link">Confluence 4.3</a></p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.7%20Release%20Notes" class="external-link">Crucible 2.7</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%202.7%20Release%20Notes" class="external-link">FishEye 2.7</a></p></td>
<td><p> </p></td>
<td><p><a href="https://confluence.atlassian.com/display/STASH/Stash+1.0+release+notes" class="external-link">Stash 1.0</a></p></td>
</tr>
<tr class="even">
<td><p>2.13</p></td>
<td><p> </p></td>
<td><p><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.0+Release+Notes" class="external-link">Confluence 5.0</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA+5.1+Release+Notes" class="external-link">JIRA 5.1</a></p></td>
<td><p>(Stash 2.1)</p></td>
</tr>
<tr class="odd">
<td>3.0</td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.2+Release+Notes" class="external-link">Confluence 5.2</a></td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/JIRA/JIRA+6.0+Release+Notes" class="external-link">JIRA 6.0</a></td>
<td> </td>
</tr>
<tr class="even">
<td>3.1</td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td>3.2</td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.6+Release+Notes" class="external-link">Confluence 5.6</a></td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/JIRA/JIRA+6.3+Release+Notes" class="external-link">JIRA 6.3</a></td>
<td> </td>
</tr>
<tr class="even">
<td>3.3</td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.8+Release+Notes" class="external-link">Confluence 5.8</a></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td>4.0</td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.9+Release+Notes" class="external-link">Confluence 5.9</a></td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/JIRASOFTWARE/JIRA+Software+7.0.x+release+notes" class="external-link">JIRA 7.0</a></td>
<td> </td>
</tr>
<tr class="even">
<td>4.1</td>
<td> </td>
<td><p><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.10+Release+Notes" class="external-link">Confluence 5.10 </a><br />
<a href="https://confluence.atlassian.com/display/DOC/Confluence+6.0+Release+Notes" class="external-link">Confluence 6.0</a> </p></td>
<td> </td>
<td> </td>
<td> </td>
<td>(JIRA 7.1)</td>
<td> </td>
</tr>
<tr class="odd">
<td>4.4</td>
<td> </td>
<td><p>Confluence 6.1<br />
Confluence 6.2<br />
Confluence 6.3<br />
Confluence 6.4<br />
Confluence 6.5<br />
</p></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
</tr>
</tbody>
</table>
