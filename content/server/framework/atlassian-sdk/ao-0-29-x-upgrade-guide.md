---
aliases:
- /server/framework/atlassian-sdk/ao-0.29.x-upgrade-guide-35720070.html
- /server/framework/atlassian-sdk/ao-0.29.x-upgrade-guide-35720070.md
category: devguide
confluence_id: 35720070
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=35720070
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=35720070
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/ao-0-18-x-upgrade-guide/ao-0-29-x-upgrade-guide
new_url: /server/framework/atlassian-sdk/ao-0-29-x-upgrade-guide
platform: server
product: atlassian-sdk
subcategory: learning
title: AO 0.29.x upgrade guide
---
# AO 0.29.x upgrade guide

## Impact

`@StringLength(450)` is the maximum allowed, reduced from the 767. Users must specify `@StringLength(UNLIMITED)` if more than 450 characters are needed.

May not explicitly invoke `Query.select("*")`; instead invoke `Query.select()` to achieve the same results i.e. all columns.

## New Features

<a href="http://h2database.com/" class="external-link">H2</a> 1.3 support

## Notable Bugfixes

Under SQL Server, string columns of length 450 or less will be created as type NVARCHAR, rather than VARCHAR, to support non-latin characters.

Plugin no longer includes java source files for the library.

## Changes

Key

Summary

T

Created

Updated

Due

Assignee

Reporter

P

Status

Resolution

Fix Version/s

[AO-586](https://ecosystem.atlassian.net/browse/AO-586?src=confmacro)

[Make sure AO core works against both Guava 11 and Guava 18](https://ecosystem.atlassian.net/browse/AO-586?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon" />](https://ecosystem.atlassian.net/browse/AO-586?src=confmacro)

Jan 13, 2015

Jan 13, 2015

James Winters

James Winters

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

0.29.2

[AO-567](https://ecosystem.atlassian.net/browse/AO-567?src=confmacro)

[Remove Refapp SPI From Plugin](https://ecosystem.atlassian.net/browse/AO-567?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon" />](https://ecosystem.atlassian.net/browse/AO-567?src=confmacro)

Oct 21, 2014

Oct 27, 2014

Alex Courtis

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon" />

Resolved

Fixed

0.29.1

[AO-552](https://ecosystem.atlassian.net/browse/AO-552?src=confmacro)

[Guard Against "SELECT \*", Document Query](https://ecosystem.atlassian.net/browse/AO-552?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon" />](https://ecosystem.atlassian.net/browse/AO-552?src=confmacro)

Sep 11, 2014

Oct 27, 2014

Nick Clarke

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon" />

Resolved

Fixed

0.29.1

[AO-546](https://ecosystem.atlassian.net/browse/AO-546?src=confmacro)

[Retrieve Database Connection From Refapp Instead Of Creating](https://ecosystem.atlassian.net/browse/AO-546?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon" />](https://ecosystem.atlassian.net/browse/AO-546?src=confmacro)

Aug 19, 2014

Oct 27, 2014

Alex Courtis

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

0.29.1

[AO-386](https://ecosystem.atlassian.net/browse/AO-386?src=confmacro)

[SQLServer String column type should be NVARCHAR to support non-latin characters](https://ecosystem.atlassian.net/browse/AO-386?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-386?src=confmacro)

Nov 19, 2012

Jan 11, 2016

Alex Courtis

Tim Pettersen

<img src="https://ecosystem.atlassian.net/images/icons/priorities/critical.svg" alt="Critical" class="icon" />

Resolved

Fixed

0.29.1

[AO-213](https://ecosystem.atlassian.net/browse/AO-213?src=confmacro)

[The activeobjects-plugin-0.17.2.x.jar ships with source for the net/ao package embedded.](https://ecosystem.atlassian.net/browse/AO-213?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-213?src=confmacro)

Nov 06, 2011

Oct 11, 2015

James Winters

Brenden Bain

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.0.1, 1.1.0, 0.28.14, 0.29.4

<a href="https://developer.atlassian.com/plugins/servlet/applinks/oauth/login-dance/authorize?applicationLinkID=61b6191d-d412-3043-a96c-75b7bceaed1f" class="static-oauth-init">Authenticate</a> to retrieve your issues

[6 issues](https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&jqlQuery=project+%3D+AO+AND+fixVersion+in+%280.29.1%2C+0.29.2%2C+0.29.3%2C+0.29.4%29+&src=confmacro "View all matching issues in JIRA.")































































































































































































































































































































