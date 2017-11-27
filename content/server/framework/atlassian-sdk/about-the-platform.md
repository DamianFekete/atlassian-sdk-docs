---
aliases:
- /server/framework/atlassian-sdk/about-the-platform-2818409.html
- /server/framework/atlassian-sdk/about-the-platform-2818409.md
category: devguide
confluence_id: 2818409
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818409
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818409
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/about-the-platform
new_url: /server/framework/atlassian-sdk/about-the-platform
platform: server
product: atlassian-sdk
subcategory: learning
title: About the Platform
---
# About the Platform

This page tells you which versions of the Atlassian Plugin Development Platform and its components are included in your host application.

 

## Matrix of Platform Versions and Component Versions

The matrix below shows the versions of each component in the Atlassian Plugin Development Platform, mapped to the versions of the platform itself.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Platform Version</p></th>
<th><p>Components</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Platform 2.8</p></td>
<td><p><a href="https://developer.atlassian.com/display/ARCHIVES/Plugin+Framework+2.6+Release+Notes">Plugin Framework 2.6</a><br />
<a href="https://developer.atlassian.com/display/ARCHIVES/Shared+Access+Layer+2.2+Release+Notes">SAL 2.2</a><br />
<a href="https://developer.atlassian.com/display/DOCS/REST+Plugin+2.2+Release+Notes">REST 2.2</a><br />
<a href="https://developer.atlassian.com/display/AUI/AUI+3.2+Release+Notes">AUI 3.2</a><br />
ATR 1.2<br />
UPM (N/A)<br />
Event (N/A)<br />
OAuth (N/A)<br />
Trusted Apps (N/A)<br />
AppLinks (N/A)<br />
Streams (N/A)</p></td>
</tr>
<tr class="even">
<td><p><a href="https://developer.atlassian.com/display/DOCS/Plugin+Development+Platform+2.9+Release+Notes">Platform 2.9</a></p></td>
<td><p><a href="https://developer.atlassian.com/display/ARCHIVES/Plugin+Framework+2.7+Release+Notes">Plugin Framework 2.7</a><br />
<a href="https://developer.atlassian.com/display/ARCHIVES/Shared+Access+Layer+2.4+Release+Notes">SAL 2.4</a><br />
REST 2.4<br />
<a href="https://developer.atlassian.com/display/AUI/AUI+3.4+Release+Notes">AUI 3.4</a><br />
ATR 1.2<br />
UPM 1.2<br />
Event 2.0<br />
OAuth 1.2<br />
Trusted Apps 2.3<br />
AppLinks 3.2<br />
Streams (N/A)</p></td>
</tr>
<tr class="odd">
<td><p><a href="https://developer.atlassian.com/display/DOCS/Plugin+Development+Platform+2.10+Release+Notes">Platform 2.10</a></p></td>
<td><p><a href="https://developer.atlassian.com/display/ARCHIVES/Plugin+Framework+2.7+Release+Notes">Plugin Framework 2.7</a><br />
<a href="https://developer.atlassian.com/display/ARCHIVES/Shared+Access+Layer+2.5+Release+Notes">SAL 2.5</a><br />
REST 2.4<br />
<a href="https://developer.atlassian.com/display/AUI/AUI+3.4+Release+Notes">AUI 3.4</a><br />
ATR 1.2<br />
UPM 1.3<br />
Event 2.1<br />
OAuth 1.2<br />
Trusted Apps 2.4<br />
AppLinks 3.4<br />
Streams (N/A)</p></td>
</tr>
<tr class="even">
<td><p><a href="https://developer.atlassian.com/display/DOCS/Plugin+Development+Platform+2.11+Release+Notes">Platform 2.11</a></p></td>
<td><p>Plugin Framework 2.8<br />
SAL 2.6<br />
REST 2.5<br />
<a href="https://developer.atlassian.com/display/AUI/AUI+3.4+Release+Notes">AUI 3.4</a><br />
ATR 1.3<br />
UPM 1.4<br />
Event 2.1<br />
OAuth 1.2<br />
Trusted Apps 2.5<br />
AppLinks 3.5<br />
Streams (N/A)</p></td>
</tr>
<tr class="odd">
<td><p>Platform 2.12</p></td>
<td><p>Plugin Framework 2.9<br />
SAL 2.6<br />
REST 2.5<br />
<a href="https://developer.atlassian.com/display/AUI/AUI+3.5+Release+Notes">AUI 3.5</a><br />
ATR 1.3<br />
UPM 1.5<br />
Event 2.1<br />
OAuth 1.2<br />
Trusted Apps 2.5<br />
AppLinks 3.5<br />
Streams (N/A)</p></td>
</tr>
<tr class="even">
<td><p>Platform 2.13</p></td>
<td><p>Plugin Framework 2.10<br />
SAL 2.7<br />
REST 2.5<br />
<a href="https://developer.atlassian.com/display/AUI/AUI+3.5+Release+Notes">AUI 3.5</a><br />
ATR 1.3<br />
UPM 1.5<br />
Event 2.1<br />
OAuth 1.3<br />
Trusted Apps 2.5<br />
AppLinks 3.6<br />
Streams 5.0</p></td>
</tr>
</tbody>
</table>

**Key:**

-   ATR = Atlassian Template Renderer
-   AUI = [Atlassian User Interface](https://developer.atlassian.com/display/AUI)
-   REST = [Rest Plugin Module](https://developer.atlassian.com/display/REST)
-   SAL = [Shared Access Layer](https://developer.atlassian.com/display/SAL)
-   UPM = [Universal Plugin Manager](https://developer.atlassian.com/display/UPM)
-   Event = Atlassian Event
-   Streams = [Activity Streams](https://developer.atlassian.com/display/STREAMS)
-   (N/A) = (This component was not part of the platform at this time.)

## Matrix of Application Versions and Component Versions

See which versions of the Atlassian applications use each component:

### Plugin Framework

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

### Shared Access Layer (SAL)

The matrix below shows the applications which include and support the Shared Access Layer. The applications are listed horizontally across the top and the SAL versions are listed vertically on the left.

-   Version numbers show the **earliest** release of the application which supports the relevant SAL version.
-   Version numbers in brackets show a future application release expected to support the relevant SAL version.

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
<th><p> </p></th>
<th><p>Bamboo</p></th>
<th><p>Confluence</p></th>
<th><p>Crowd</p></th>
<th><p>Crucible</p></th>
<th><p>FishEye</p></th>
<th><p>JIRA</p></th>
<th>Bitbucket Server<br />
(formerly Stash)</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>SAL 3.1.0</td>
<td> </td>
<td>Confluence 6.5<br />
Confluence 6.4<br />
Confluence 6.3<br />
Confluence 6.2<br />
Confluence 6.1</td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/AdminJIRAServer074/Administering+JIRA+Server+7.4+applications" class="external-link">JIRA 7.4 platform</a></td>
<td><p><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+5.5+release+notes" class="external-link">Bitbucket Server 5.5</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+5.4+release+notes" class="external-link"><br />
Bitbucket Server 5.4</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+5.3+release+notes" class="external-link"><br />
Bitbucket Server 5.</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+5.2+release+notes" class="external-link">3<br />
Bitbucket Server 5.2<br />
</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+5.1+release+notes" class="external-link">Bitbucket Server 5.1<br />
</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+5.0+release+notes" class="external-link">Bitbucket Server 5.0</a></p></td>
</tr>
<tr class="even">
<td>SAL 3.0.7</td>
<td><p><a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo+5.13+Release+Notes" class="external-link">Bamboo 5.13</a></p></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/AdminJIRAServer073" class="external-link">JIRA 7.3 platform</a></td>
<td> </td>
</tr>
<tr class="odd">
<td>SAL 3.0.6</td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence+6.0+Release+Notes" class="external-link">Confluence 6.0</a><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.10+Release+Notes" class="external-link"><br />
Confluence 5.10</a></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.14+release+notes" class="external-link">Bitbucket Server 4.14</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.13+release+notes" class="external-link"><br />
Bitbucket Server 4.13</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.12+release+notes" class="external-link"><br />
Bitbucket Server 4.12</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.11+release+notes" class="external-link"><br />
Bitbucket Server 4.11</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.10+release+notes" class="external-link"><br />
Bitbucket Server 4.10</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.9+release+notes" class="external-link"><br />
Bitbucket Server 4.9</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.8+release+notes" class="external-link"><br />
Bitbucket Server 4.8</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.7+release+notes" class="external-link"><br />
Bitbucket Server 4.7</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.6+release+notes" class="external-link"><br />
Bitbucket Server 4.6</a></td>
</tr>
<tr class="even">
<td>SAL 3.0.5</td>
<td><p><a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo+5.11+Release+Notes" class="external-link">Bamboo 5.11<br />
</a><a href="https://confluence.atlassian.com/display/BAMBOO0512/Bamboo+5.12+Release+Notes" class="external-link">Bamboo 5.12</a> </p></td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.9+Release+Notes" class="external-link">Confluence 5.9</a></td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible+4.1+release+notes" class="external-link">Crucible 4.1</a><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible+4.0+release+notes" class="external-link"><br />
Crucible 4.0</a></td>
<td><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye+4.1+release+notes" class="external-link">FishEye 4.1</a><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye+4.0+release+notes" class="external-link"><br />
FishEye 4.0</a></td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.5+release+notes" class="external-link">Bitbucket Server 4.5</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.4+release+notes" class="external-link"><br />
Bitbucket Server 4.4</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.3+release+notes" class="external-link"> <br />
Bitbucket Server 4.3</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.2+release+notes" class="external-link"> <br />
Bitbucket Server 4.2</a></td>
</tr>
<tr class="odd">
<td>SAL 3.0.3</td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td><p><a href="https://confluence.atlassian.com/jiracore/jira-core-7-1-x-release-notes-802161668.html" class="external-link">JIRA 7.1<br />
</a><a href="https://confluence.atlassian.com/jiracore/jira-core-7-0-x-release-notes-781386735.html" class="external-link">JIRA 7.0</a></p></td>
<td> </td>
</tr>
<tr class="even">
<td>SAL 3.0.1</td>
<td><a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo+5.10+Release+Notes" class="external-link">Bamboo 5.10</a></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
</tr>
<tr class="odd">
<td>SAL 2.13</td>
<td> </td>
<td><p><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.8+Release+Notes" class="external-link">Confluence 5.8</a><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.7+Release+Notes" class="external-link"><br />
Confluence 5.7</a></p></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.1+release+notes" class="external-link">Bitbucket Server 4.1</a><a href="https://confluence.atlassian.com/display/BitbucketServer/Bitbucket+Server+4.0+release+notes" class="external-link"><br />
Bitbucket Server 4.0</a><a href="https://confluence.atlassian.com/display/STASH/Stash+3.11+release+notes" class="external-link"><br />
Stash 3.11</a><a href="https://confluence.atlassian.com/display/STASH/Stash+3.10+release+notes" class="external-link"><br />
Stash 3.10</a><a href="https://confluence.atlassian.com/display/STASH/Stash+3.9+release+notes" class="external-link"><br />
Stash 3.9</a><a href="https://confluence.atlassian.com/display/STASH/Stash+3.8+release+notes" class="external-link"><br />
Stash 3.8</a> <a href="https://confluence.atlassian.com/display/STASH/Stash+3.7+release+notes" class="external-link"><br />
Stash 3.7</a> <a href="https://confluence.atlassian.com/display/STASH/Stash+3.6+release+notes" class="external-link"><br />
Stash 3.6</a> <a href="https://confluence.atlassian.com/display/STASH/Stash+3.5+release+notes" class="external-link"><br />
Stash 3.5</a></td>
</tr>
<tr class="even">
<td>SAL 2.12</td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence+5.6+Release+Notes" class="external-link">Confluence 5.6</a></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/STASH/Stash+3.4+release+notes" class="external-link">Stash 3.4</a> <a href="https://confluence.atlassian.com/display/STASH/Stash+3.3+release+notes" class="external-link"><br />
Stash 3.3</a> <a href="https://confluence.atlassian.com/display/STASH/Stash+3.2+release+notes" class="external-link"><br />
Stash 3.2</a></td>
</tr>
<tr class="odd">
<td>SAL 2.11</td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td><p><a href="https://confluence.atlassian.com/display/JIRA/JIRA+6.4+Release+Notes" class="external-link">JIRA 6.4</a></p></td>
<td><a href="https://confluence.atlassian.com/display/STASH/Stash+3.0+release+notes" class="external-link">Stash 3.0</a></td>
</tr>
<tr class="even">
<td>SAL 2.10</td>
<td><p><a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo+5.9+release+notes" class="external-link">Bamboo 5.9</a></p>
<p><a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo+5.8+release+notes" class="external-link">Bamboo 5.8</a> <a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo+5.7+release+notes" class="external-link"><br />
Bamboo 5.7</a> <a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo+5.6+release+notes" class="external-link"><br />
Bamboo 5.6</a> <a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo%205.1%20Release%20Notes" class="external-link"><br />
Bamboo 5.1</a></p></td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence%205.2%20Release%20Notes" class="external-link">Confluence 5.2</a></td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.10%20Release%20Notes" class="external-link">Crucible 3.10</a><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.9%20Release%20Notes" class="external-link"><br />
Crucible 3.9</a><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.8%20Release%20Notes" class="external-link"><br />
Crucible 3.8</a><br />
<a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.7%20Release%20Notes" class="external-link">Crucible 3.7</a> <a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.6%20Release%20Notes" class="external-link"><br />
Crucible 3.6</a> <a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.6%20Release%20Notes" class="external-link"><br />
</a><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.5%20Release%20Notes" class="external-link">Crucible 3.5</a> <a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.2%20Release%20Notes" class="external-link"><br />
Crucible 3.2</a></td>
<td><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%203.10%20Release%20Notes" class="external-link">FishEye 3.10</a><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%203.9%20Release%20Notes" class="external-link"><br />
FishEye 3.9</a><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%203.8%20Release%20Notes" class="external-link"><br />
FishEye 3.8</a><br />
<a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%203.7%20Release%20Notes" class="external-link">FishEye 3.7</a> <a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%203.6%20Release%20Notes" class="external-link"><br />
FishEye 3.6</a> <a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%203.5%20Release%20Notes" class="external-link"><br />
FishEye 3.5</a> <a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%203.2%20Release%20Notes" class="external-link"><br />
FishEye 3.2</a></td>
<td><p><a href="https://confluence.atlassian.com/display/JIRA064/JIRA+6.3+Release+Notes" class="external-link">JIRA 6.3</a></p>
<p><a href="https://confluence.atlassian.com/display/JIRA064/JIRA+6.2+Release+Notes" class="external-link">JIRA 6.2</a></p>
<p><a href="https://confluence.atlassian.com/display/JIRA/JIRA+6.1+Release+Notes" class="external-link">JIRA 6.1</a></p></td>
<td><a href="https://confluence.atlassian.com/display/STASH/Stash+2.9+release+notes" class="external-link">Stash 2.9</a></td>
</tr>
<tr class="odd">
<td><strong>SAL 2.9</strong></td>
<td><a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo%205.0%20Release%20Notes" class="external-link">Bamboo 5.0</a></td>
<td><a href="https://confluence.atlassian.com/display/DOC/Confluence%205.0%20Release%20Notes" class="external-link">Confluence 5.0</a></td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%203.0%20Release%20Notes" class="external-link">Crucible 3.0</a></td>
<td><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%203.0%20Release%20Notes" class="external-link">FishEye 3.0</a></td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/STASH/Stash+2.4+release+notes" class="external-link">Stash 2.4</a></td>
</tr>
<tr class="even">
<td><strong>SAL 2.8</strong></td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/JIRA/JIRA+6.0+Release+Notes" class="external-link">JIRA 6.0</a></td>
<td><a href="https://confluence.atlassian.com/display/STASH/Stash+2.1+release+notes" class="external-link">Stash 2.1</a></td>
</tr>
<tr class="odd">
<td><p>SAL 2.7</p></td>
<td><p><a href="https://confluence.atlassian.com/display/BAMBOO/Bamboo%203.4%20Release%20Notes" class="external-link">Bamboo 3.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%204.1%20Release%20Notes" class="external-link">Confluence 4.1</a></p></td>
<td><p> </p></td>
<td><p><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.8%20Release%20Notes" class="external-link">Crucible 2.8</a></p></td>
<td><p><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%202.8%20Release%20Notes" class="external-link">FishEye 2.8</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA+5.0+Release+Notes" class="external-link">JIRA 5.0</a></p></td>
<td><a href="https://confluence.atlassian.com/display/STASH/Stash+1.0+release+notes" class="external-link">Stash 1.0</a></td>
</tr>
<tr class="even">
<td><p>SAL 2.6</p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%204.0%20Release%20Notes" class="external-link">Confluence 4.0</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/Crowd/Crowd%202.3.1%20Release%20Notes" class="external-link">Crowd 2.3</a></p></td>
<td><p><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.7%20Release%20Notes" class="external-link">Crucible 2.7</a></p></td>
<td><p><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%202.7%20Release%20Notes" class="external-link">FishEye 2.7</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.4%20Release%20Notes" class="external-link">JIRA 4.4</a></p></td>
<td> </td>
</tr>
<tr class="odd">
<td>SAL 2.5</td>
<td> </td>
<td> </td>
<td> </td>
<td><a href="https://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.6%20Release%20Notes" class="external-link">Crucible 2.6</a></td>
<td><a href="https://confluence.atlassian.com/display/FISHEYE/FishEye%202.6%20Release%20Notes" class="external-link">FishEye 2.6</a></td>
<td> </td>
<td> </td>
</tr>
<tr class="even">
<td><p>SAL 2.3</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>SAL 2.2</p></td>
<td><p><a href="http://confluence.atlassian.com/display/BAMBOO/Bamboo%203.0%20Release%20Notes" class="external-link">Bamboo 3.0</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.4%20Release%20Notes" class="external-link">Confluence 3.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.2.2%20Release%20Notes" class="external-link">Crowd 2.2</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.4%20Release%20Notes" class="external-link">Crucible 2.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%202.4%20Release%20Notes" class="external-link">FishEye 2.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.3%20Release%20Notes" class="external-link">JIRA 4.3</a></p></td>
<td> </td>
</tr>
<tr class="even">
<td><p>SAL 2.1</p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.3%20Release%20Notes" class="external-link">Confluence 3.3</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.2%20Release%20Notes" class="external-link">JIRA 4.2</a></p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>SAL 2.0</p></td>
<td><p><a href="http://confluence.atlassian.com/display/BAMBOO/Bamboo%202.3%20Release%20Notes" class="external-link">Bamboo 2.3</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.0%20Release%20Notes" class="external-link">Confluence 3.0</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.0%20Release%20Notes" class="external-link">Crowd 2.0</a></p></td>
<td><p>Crucible 1.6.5</p></td>
<td><p>FishEye 1.6.5</p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.0%20Release%20Notes" class="external-link">JIRA 4.0</a></p></td>
<td> </td>
</tr>
</tbody>
</table>

INFO: There is also a detailed list of [services available per application](https://developer.atlassian.com/display/DOCS/SAL+Services).

### Atlassian User Interface (AUI)

{{% note %}}

This page has moved.

The AUI / Product version matrix has been moved to <a href="https://bitbucket.org/atlassian/aui-adg/wiki/versions/product-version-matrix" class="external-link">the AUI-ADG bitbucket repository</a>.

{{% /note %}}

### Atlassian REST Plugin Module

The matrix below shows the applications which include and support the REST API plugin. The applications are listed horizontally across the top and the REST plugin versions are listed vertically on the left.

-   Version numbers without brackets show the **earliest** release of the application which supports the relevant REST plugin version.
-   Version numbers in brackets show a future application release expected to support the relevant version of the REST plugin.

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
<th><p> </p></th>
<th><p>Bamboo</p></th>
<th><p>Confluence</p></th>
<th><p>Crowd</p></th>
<th><p>Crucible</p></th>
<th><p>FishEye</p></th>
<th><p>JIRA</p></th>
<th>Stash</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>REST plugin 1.0</p></td>
<td><p><a href="http://confluence.atlassian.com/display/BAMBOO/Bamboo%202.4%20Release%20Notes" class="external-link">Bamboo 2.4</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.3%20Release%20Notes" class="external-link">Crucible 2.3</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%202.3%20Release%20Notes" class="external-link">FishEye 2.3</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.0%20Release%20Notes" class="external-link">JIRA 4.0</a></p></td>
<td> </td>
</tr>
<tr class="even">
<td><p>REST plugin 1.1</p></td>
<td><p><a href="http://confluence.atlassian.com/display/BAMBOO/Bamboo%202.6%20Release%20Notes" class="external-link">Bamboo 2.6</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.1%20Release%20Notes" class="external-link">Confluence 3.1</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.1%20Release%20Notes" class="external-link">Crowd 2.1</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>REST plugin 2.0</p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.3%20Release%20Notes" class="external-link">Confluence 3.3</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td> </td>
</tr>
<tr class="even">
<td><p>REST plugin 2.1</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.2%20Release%20Notes" class="external-link">JIRA 4.2</a></p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>REST plugin 2.2</p></td>
<td><p>(Bamboo 3.0)</p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%203.4%20Release%20Notes" class="external-link">Confluence 3.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.2.2%20Release%20Notes" class="external-link">Crowd 2.2</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CRUCIBLE/Crucible%202.4%20Release%20Notes" class="external-link">Crucible 2.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/FISHEYE/FishEye%202.4%20Release%20Notes" class="external-link">FishEye 2.4</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.3%20Release%20Notes" class="external-link">JIRA 4.3</a></p></td>
<td> </td>
</tr>
<tr class="even">
<td><p>REST plugin 2.5</p></td>
<td><p>(Bamboo 3.4)</p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%204.0%20Release%20Notes" class="external-link">Confluence 4.0</a></p></td>
<td><p><a href="http://confluence.atlassian.com/display/CROWD/Crowd%202.3.1%20Release%20Notes" class="external-link">Crowd 2.3</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/JIRA/JIRA%204.4%20Release%20Notes" class="external-link">JIRA 4.4</a></p></td>
<td> </td>
</tr>
<tr class="odd">
<td><p>REST plugin 2.6</p></td>
<td><p> </p></td>
<td><p><a href="http://confluence.atlassian.com/display/DOC/Confluence%204.2%20Release%20Notes" class="external-link">Confluence 4.2</a></p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p>(JIRA 5.1)</p></td>
<td>  <a href="https://confluence.atlassian.com/display/STASH/Stash+1.0+release+notes" class="external-link">Stash 1.0</a></td>
</tr>
<tr class="even">
<td><p>REST plugin 2.7</p></td>
<td><p> </p></td>
<td><p>(Confluence 5.0)</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><a href="https://confluence.atlassian.com/display/STASH/Stash+1.3+release+notes" class="external-link">Stash 1.3</a></td>
</tr>
</tbody>
</table>

## Platform Release Notes

-   [Plugin Development Platform 2.8 Release Notes](/server/framework/atlassian-sdk/plugin-development-platform-2-8-release-notes)
-   [Plugin Development Platform 2.9 Release Notes](/server/framework/atlassian-sdk/plugin-development-platform-2-9-release-notes)
-   [Plugin Development Platform 2.10 Release Notes](/server/framework/atlassian-sdk/plugin-development-platform-2-10-release-notes)
-   [Plugin Development Platform 2.11 Release Notes](/server/framework/atlassian-sdk/plugin-development-platform-2-11-release-notes)
-   [Plugin Development Platform 2.12 Release Notes](/server/framework/atlassian-sdk/plugin-development-platform-2-12-release-notes)
-   [Plugin Development Platform 2.13 Release Notes](/server/framework/atlassian-sdk/plugin-development-platform-2-13-release-notes)
















































































































































































































































































































