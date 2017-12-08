---
aliases:
- /server/framework/atlassian-sdk/rest-and-os-authtype-4915201.html
- /server/framework/atlassian-sdk/rest-and-os-authtype-4915201.md
category: devguide
confluence_id: 4915201
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915201
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915201
date: '2017-12-08'
legacy_title: REST and os_authType
platform: server
product: atlassian-sdk
subcategory: security
title: REST and os_authType
---
# REST and os\_authType

{{% note %}}

This functionality is part of the Atlassian REST plugin 2.1.0 and Seraph 2.2 releases. See the [REST API Plugin version matrix](https://developer.atlassian.com/display/DOCS/REST+API+Plugin+Version+Matrix) for availability.

{{% /note %}}

One common problem with REST API access to Atlassian applications is dealing with authentication. 

To authenticate some remote clients use cookies, just like a web browser does. That is, they acquire a login and a cookie and then submit the cookie with each request. The downside to this approach is that cookies eventually expire. When this happens you are treated as an anonymous user.

As a user, you've probably noticed this when, once in a while, you go to an Atlassian app and have to log in again. As a human, this situation is pretty easy to detect and fix. For something that is programmatically interacting with an application, it is much harder to detect! Imagine that you submit a query to JIRA and, instead of getting back 200 results, you get back only the 5 issues that anonymous users can see. Nothing obviously **failed** but you don't get the results you want.

To avoid this, Atlassian applications treat cookie expiration differently under the **/rest** URLs. If you submit an expired cookie to a REST resource under the **/rest** URL, you receive a 401 error response instead of silently being treated as an anonymous user. Thus, the REST application can resubmit credentials in this case.

Note that this behaviour does not apply, by default, to other parts of the system. This only affects **/rest** URLs.

However, some applications may want to replicate this behaviour across the entirely of the system. For instance, if you are performing some kind of screen-scraping you might like to have this happen **everywhere**.

You can trigger this behaviour by adding the **os\_authType** query parameter in your URL. **os\_authType** supports the following parameters and behaviour:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>os_authType</p></th>
<th><p>behaviour</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>basic</p></td>
<td><p>The server will return a 401 error response and perform an HTTP Basic Authentication challenge if no username and password is specified</p></td>
</tr>
<tr class="even">
<td><p>cookie</p></td>
<td><p>The server will return a 401 error response if a valid cookie is not provided in the request</p></td>
</tr>
<tr class="odd">
<td><p>any</p></td>
<td><p>If a username and password are not specified <strong>and</strong> there is not valid cookie, the server will return a 401 error response</p></td>
</tr>
</tbody>
</table>































































































































































































