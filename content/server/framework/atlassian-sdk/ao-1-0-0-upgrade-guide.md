---
aliases:
- /server/framework/atlassian-sdk/ao-1.0.0-upgrade-guide-35720049.html
- /server/framework/atlassian-sdk/ao-1.0.0-upgrade-guide-35720049.md
category: devguide
confluence_id: 35720049
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=35720049
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=35720049
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/ao-1-0-0-upgrade-guide
new_url: /server/framework/atlassian-sdk/ao-1-0-0-upgrade-guide
platform: server
product: atlassian-sdk
subcategory: learning
title: AO 1.0.0 upgrade guide
---
# AO 1.0.0 upgrade guide

# Major Release

The Active Objects plugin and library 1.0.0 release immediately followed the 0.29.4 release.

This change in versioning was made at a point in time in which it would ship with new major versions of Atlassian products. This does not indicate that 1.0.0 is any more stable or "release ready" than the previous release, however it does allow AO to follow proper <a href="http://semver.org/" class="external-link">Semantic Versioning</a> when making releases, using MAJOR, MINOR and PATCH increments to indicate the impact of the changes.

## Impact

There is no impact on users of either the ActiveObjects library or the Atlassian plugin - it is compatible with the previous release.

## New Features

No new features have been added.

## Notable Bugfixes

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

[AO-693](https://ecosystem.atlassian.net/browse/AO-693?src=confmacro)

[Postgres 9.4 Testing](https://ecosystem.atlassian.net/browse/AO-693?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon" />](https://ecosystem.atlassian.net/browse/AO-693?src=confmacro)

Oct 28, 2015

Nov 30, 2015

Elena Vasilyeva

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.0.0

[AO-654](https://ecosystem.atlassian.net/browse/AO-654?src=confmacro)

[Remove "Missing Reverse OneToMany" Warning](https://ecosystem.atlassian.net/browse/AO-654?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon" />](https://ecosystem.atlassian.net/browse/AO-654?src=confmacro)

Jun 15, 2015

Jul 03, 2015

Unassigned

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

0.30.x, 1.0.0

[AO-648](https://ecosystem.atlassian.net/browse/AO-648?src=confmacro)

[Add A Guard For Multiple Registrations Of Same &lt;ao&gt; Configuration](https://ecosystem.atlassian.net/browse/AO-648?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-648?src=confmacro)

May 21, 2015

Oct 28, 2015

Alex Courtis

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

0.30.x, 1.0.0

[AO-643](https://ecosystem.atlassian.net/browse/AO-643?src=confmacro)

[AO table for jira-development-integration-plugin is not created](https://ecosystem.atlassian.net/browse/AO-643?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-643?src=confmacro)

May 13, 2015

Jan 11, 2016

Alex Courtis

Eric Sukmajaya

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.0.0

[AO-640](https://ecosystem.atlassian.net/browse/AO-640?src=confmacro)

[Migrate From Deprecated AutowireCapable Plugin To ContainerManagedPlugin](https://ecosystem.atlassian.net/browse/AO-640?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon" />](https://ecosystem.atlassian.net/browse/AO-640?src=confmacro)

May 03, 2015

Jul 03, 2015

Alex Courtis

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

0.30.x, 1.0.0

[AO-592](https://ecosystem.atlassian.net/browse/AO-592?src=confmacro)

[back down from H2 1.4 (beta) to 1.3 (stable)](https://ecosystem.atlassian.net/browse/AO-592?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon" />](https://ecosystem.atlassian.net/browse/AO-592?src=confmacro)

Jan 29, 2015

Jul 03, 2015

Alex Courtis

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.0.0

[AO-569](https://ecosystem.atlassian.net/browse/AO-569?src=confmacro)

[Update to Spring 4.1.4+](https://ecosystem.atlassian.net/browse/AO-569?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon" />](https://ecosystem.atlassian.net/browse/AO-569?src=confmacro)

Oct 30, 2014

Jul 03, 2015

Unassigned

Marcos Scriven

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.0.0

[AO-488](https://ecosystem.atlassian.net/browse/AO-488?src=confmacro)

[50 ActiveObject Entity limit per add-on? YGTBKM! Now it's 200](https://ecosystem.atlassian.net/browse/AO-488?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-488?src=confmacro)

Nov 22, 2013

Jul 01, 2016

Alex Courtis

Andy Brook

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

0.30.x, 1.0.0

[AO-639](https://ecosystem.atlassian.net/browse/AO-639?src=confmacro)

[Release new version of AO that has a more recent amps version](https://ecosystem.atlassian.net/browse/AO-639?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon" />](https://ecosystem.atlassian.net/browse/AO-639?src=confmacro)

Apr 30, 2015

Jul 03, 2015

Martin Henderson

Martin Henderson

<img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon" />

Resolved

Fixed

1.0.0

[AO-637](https://ecosystem.atlassian.net/browse/AO-637?src=confmacro)

[&lt;ao&gt; Modules Are Keyed By &lt;plugin-key&gt; Only](https://ecosystem.atlassian.net/browse/AO-637?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon" />](https://ecosystem.atlassian.net/browse/AO-637?src=confmacro)

Apr 15, 2015

Aug 27, 2015

Unassigned

Alex Courtis

<img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon" />

Resolved

Fixed

0.30.x, 1.0.0

<a href="https://developer.atlassian.com/plugins/servlet/applinks/oauth/login-dance/authorize?applicationLinkID=61b6191d-d412-3043-a96c-75b7bceaed1f" class="static-oauth-init">Authenticate</a> to retrieve your issues

[10 issues](https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&jqlQuery=project+%3D+AO+and+fixVersion+%3D+%221.0.0%22+order+by+priority+desc++&src=confmacro "View all matching issues in JIRA.")





























































































































































































































































































































