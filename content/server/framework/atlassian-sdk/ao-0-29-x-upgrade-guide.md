---
aliases:
- /server/framework/atlassian-sdk/ao-0.29.x-upgrade-guide-35720070.html
- /server/framework/atlassian-sdk/ao-0.29.x-upgrade-guide-35720070.md
category: devguide
confluence_id: 35720070
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=35720070
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=35720070
date: '2017-12-08'
guides: guides
legacy_title: AO 0.29.x Upgrade Guide
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

| Key                                                                                                    | Summary                                                                                                                                                                                  | T                                                                                                                                                                                                                                                                                   | Created      | Updated      | Assignee      | Reporter      | P                                                                                                                                                | Status   | Resolution | Fix Version/S                 |
|--------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|--------------|---------------|---------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------|-------------------------------|
| <a href="https://ecosystem.atlassian.net/browse/AO-586?src=confmacro" class="external-link">AO-586</a> | <a href="https://ecosystem.atlassian.net/browse/AO-586?src=confmacro" class="external-link">Make sure AO core works against both Guava 11 and Guava 18</a>                               | <a href="https://ecosystem.atlassian.net/browse/AO-586?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="confluence-external-resource icon" /></a>        | Jan 13, 2015 | Jan 13, 2015 | James Winters | James Winters | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" width="16" /> | RESOLVED | Fixed      | 0.29.2                        |
| <a href="https://ecosystem.atlassian.net/browse/AO-567?src=confmacro" class="external-link">AO-567</a> | <a href="https://ecosystem.atlassian.net/browse/AO-567?src=confmacro" class="external-link">Remove Refapp SPI From Plugin</a>                                                            | <a href="https://ecosystem.atlassian.net/browse/AO-567?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="confluence-external-resource icon" /></a> | Oct 21, 2014 | Oct 27, 2014 | Alex Courtis  | Alex Courtis  | <img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="confluence-external-resource icon" />            | RESOLVED | Fixed      | 0.29.1                        |
| <a href="https://ecosystem.atlassian.net/browse/AO-552?src=confmacro" class="external-link">AO-552</a> | <a href="https://ecosystem.atlassian.net/browse/AO-552?src=confmacro" class="external-link">Guard Against &quot;SELECT *&quot;, Document Query</a>                                       | <a href="https://ecosystem.atlassian.net/browse/AO-552?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="confluence-external-resource icon" /></a> | Sep 11, 2014 | Oct 27, 2014 | Nick Clarke   | Alex Courtis  | <img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="confluence-external-resource icon" />            | RESOLVED | Fixed      | 0.29.1                        |
| <a href="https://ecosystem.atlassian.net/browse/AO-546?src=confmacro" class="external-link">AO-546</a> | <a href="https://ecosystem.atlassian.net/browse/AO-546?src=confmacro" class="external-link">Retrieve Database Connection From Refapp Instead Of Creating</a>                             | <a href="https://ecosystem.atlassian.net/browse/AO-546?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="confluence-external-resource icon" /></a> | Aug 19, 2014 | Oct 27, 2014 | Alex Courtis  | Alex Courtis  | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />            | RESOLVED | Fixed      | 0.29.1                        |
| <a href="https://ecosystem.atlassian.net/browse/AO-386?src=confmacro" class="external-link">AO-386</a> | <a href="https://ecosystem.atlassian.net/browse/AO-386?src=confmacro" class="external-link">SQLServer String column type should be NVARCHAR to support non-latin characters</a>          | <a href="https://ecosystem.atlassian.net/browse/AO-386?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="confluence-external-resource icon" /></a>         | Nov 19, 2012 | Jan 11, 2016 | Alex Courtis  | Tim Pettersen | <img src="https://ecosystem.atlassian.net/images/icons/priorities/critical.svg" alt="Critical" class="confluence-external-resource icon" />      | RESOLVED | Fixed      | 0.29.1                        |
| <a href="https://ecosystem.atlassian.net/browse/AO-213?src=confmacro" class="external-link">AO-213</a> | <a href="https://ecosystem.atlassian.net/browse/AO-213?src=confmacro" class="external-link">The activeobjects-plugin-0.17.2.x.jar ships with source for the net/ao package embedded.</a> | <a href="https://ecosystem.atlassian.net/browse/AO-213?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="confluence-external-resource icon" /></a>         | Nov 06, 2011 | Oct 11, 2015 | James Winters | Brenden Bain  | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />            | RESOLVED | Fixed      | 1.0.1, 1.1.0, 0.28.14, 0.29.4 |

<a href="https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&amp;jqlQuery=project+%3D+AO+AND+fixVersion+in+%280.29.1%2C+0.29.2%2C+0.29.3%2C+0.29.4%29+&amp;src=confmacro" class="external-link" title="View all matching issues in JIRA.">6 issues</a>







































































































































































































































































