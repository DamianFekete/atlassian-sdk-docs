---
aliases:
- /server/framework/atlassian-sdk/ao-1.2.0-upgrade-guide-39999656.html
- /server/framework/atlassian-sdk/ao-1.2.0-upgrade-guide-39999656.md
category: devguide
confluence_id: 39999656
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=39999656
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=39999656
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/ao-1-2-0-upgrade-guide
new_url: /server/framework/atlassian-sdk/ao-1-2-0-upgrade-guide
platform: server
product: atlassian-sdk
subcategory: learning
title: AO 1.2.0 upgrade guide
---
# AO 1.2.0 upgrade guide

## Impact

There is no impact on users of either the ActiveObjects library or the Atlassian plugin - it is backwards compatible with 1.1.x.

## New Features

Added support for composite indexes. Composite indexes can be declared using @Indexes annotation. Example usage is shown below:

``` java
import net.java.ao.Entity;
import net.java.ao.schema.Index;
import net.java.ao.schema.Indexes;
 
@Indexes({
    @Index(name = "names", methodNames = {"getFirstName", "getLastName"}),
    @Index(name = "age", methodNames = "getAge")
})
public interface Person extends Entity {
    public String getFirstName();
    public void setFirstName(String firstName);
    public void setLastName(String lastName);
    public String getLastName();
    public int getAge();
    public void setAge(int age);
}
```

Please note two things:

-   It is still possible to declare single column indexes using @Indexed annotation.
-   The new way of declaring indexes may be also used to declare single column indexes.

For more information please refer to java docs.

## Notable Bugfixes

There are no bugfixes in this release.

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

[AO-96](https://ecosystem.atlassian.net/browse/AO-96?src=confmacro)

[Add possibility in AO to create multi-column indexes](https://ecosystem.atlassian.net/browse/AO-96?src=confmacro)

[<img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15311&amp;avatarType=issuetype" alt="New Feature" class="icon" />](https://ecosystem.atlassian.net/browse/AO-96?src=confmacro)

Feb 02, 2011

Apr 27, 2017

Sebastian Pawlak

Samuel Berrigaud

<img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon" />

Resolved

Fixed

1.2.0

<a href="https://developer.atlassian.com/plugins/servlet/applinks/oauth/login-dance/authorize?applicationLinkID=61b6191d-d412-3043-a96c-75b7bceaed1f" class="static-oauth-init">Authenticate</a> to retrieve your issues

[1 issue](https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&jqlQuery=project+%3D+AO+AND+fixVersion+%3D+%221.2.0%22+++++&src=confmacro "View all matching issues in JIRA.")



































































































































































































































































































