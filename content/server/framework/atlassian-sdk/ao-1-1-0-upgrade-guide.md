---
aliases:
- /server/framework/atlassian-sdk/ao-1.1.0-upgrade-guide-35720053.html
- /server/framework/atlassian-sdk/ao-1.1.0-upgrade-guide-35720053.md
category: devguide
confluence_id: 35720053
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=35720053
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=35720053
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/ao-1-1-0-upgrade-guide
new_url: /server/framework/atlassian-sdk/ao-1-1-0-upgrade-guide
platform: server
product: atlassian-sdk
subcategory: learning
title: AO 1.1.0 upgrade guide
---
# AO 1.1.0 upgrade guide

## Impact

There is no impact on users of either the ActiveObjects library or the Atlassian plugin - it is compatible with the previous release.

## New Features

Limited `HAVING` support for `net.java.ao.Query`

<a href="http://www.nuodb.com/" class="external-link">NuoDB</a> support.

## Notable Bugfixes

Postgres table aliases no longer quoted during `GROUP BY` and `ORDER BY`.

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

[AO-677](https://ecosystem.atlassian.net/browse/AO-677?src=confmacro)

[Add H2 to TestActiveObjects](https://ecosystem.atlassian.net/browse/AO-677?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon" />](https://ecosystem.atlassian.net/browse/AO-677?src=confmacro)

Aug 31, 2015

Sep 25, 2015

Unassigned

Felix Haehnel

<img src="https://ecosystem.atlassian.net/images/icons/priorities/trivial.svg" alt="Trivial" class="icon" />

Resolved

Fixed

1.0.1, 1.1.0

[AO-675](https://ecosystem.atlassian.net/browse/AO-675?src=confmacro)

[ao-plugin 1.1.x hanging webdriver tests with ao 1.1.0](https://ecosystem.atlassian.net/browse/AO-675?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-675?src=confmacro)

Aug 27, 2015

Sep 08, 2015

Alex Courtis

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.1.0

[AO-672](https://ecosystem.atlassian.net/browse/AO-672?src=confmacro)

["multiple active objects configurations" Errors On Restarting Dependent Plugins](https://ecosystem.atlassian.net/browse/AO-672?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-672?src=confmacro)

Aug 19, 2015

Oct 28, 2015

Alex Courtis

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.0.1, 1.1.0

[AO-655](https://ecosystem.atlassian.net/browse/AO-655?src=confmacro)

[Move activeobjects-bamboo-spi into Bamboo codebase](https://ecosystem.atlassian.net/browse/AO-655?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15311&amp;avatarType=issuetype" alt="New Feature" class="icon" />](https://ecosystem.atlassian.net/browse/AO-655?src=confmacro)

Jun 15, 2015

Oct 09, 2015

Krystian Brazulewicz

Krystian Brazulewicz

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.1.0

[AO-635](https://ecosystem.atlassian.net/browse/AO-635?src=confmacro)

[Table alias in order by clause in Postgres should not be quoted](https://ecosystem.atlassian.net/browse/AO-635?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-635?src=confmacro)

Mar 18, 2015

Jan 11, 2016

Unassigned

Georg Schmidl

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.1.0

[AO-634](https://ecosystem.atlassian.net/browse/AO-634?src=confmacro)

[Support for having clauses](https://ecosystem.atlassian.net/browse/AO-634?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15311&amp;avatarType=issuetype" alt="New Feature" class="icon" />](https://ecosystem.atlassian.net/browse/AO-634?src=confmacro)

Mar 17, 2015

Aug 31, 2015

Alex Courtis

Georg Schmidl

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.1.0

[AO-633](https://ecosystem.atlassian.net/browse/AO-633?src=confmacro)

[Active Objects quotes table alias in group by clause in Postgres](https://ecosystem.atlassian.net/browse/AO-633?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-633?src=confmacro)

Mar 17, 2015

Jan 11, 2016

Alex Courtis

Georg Schmidl

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.1.0

[AO-538](https://ecosystem.atlassian.net/browse/AO-538?src=confmacro)

[Add NuoDB Support](https://ecosystem.atlassian.net/browse/AO-538?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon" />](https://ecosystem.atlassian.net/browse/AO-538?src=confmacro)

Jul 16, 2014

Aug 26, 2015

Alex Courtis

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon" />

Resolved

Fixed

1.1.0

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

[9 issues](https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&jqlQuery=project+%3D+AO+AND+fixVersion+%3D+%221.1.0%22++++&src=confmacro "View all matching issues in JIRA.")



































































































































































































































































































