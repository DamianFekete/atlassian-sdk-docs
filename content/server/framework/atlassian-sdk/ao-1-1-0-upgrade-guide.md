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

| Key                                                                                                    | Summary                                                                                                                                                                                   | T                                                                                                                                                                                                                                                                                   | Created      | Updated      | Assignee             | Reporter             | P                                                                                                                                                    | Status   | Resolution | Fix Version/S                 |
|--------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|--------------|----------------------|----------------------|------------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------|-------------------------------|
| <a href="https://ecosystem.atlassian.net/browse/AO-677?src=confmacro" class="external-link">AO-677</a> | <a href="https://ecosystem.atlassian.net/browse/AO-677?src=confmacro" class="external-link">Add H2 to TestActiveObjects</a>                                                               | <a href="https://ecosystem.atlassian.net/browse/AO-677?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="confluence-external-resource icon" /></a> | Aug 31, 2015 | Sep 25, 2015 | Unassigned           | Felix Haehnel        | <img src="https://ecosystem.atlassian.net/images/icons/priorities/trivial.svg" alt="Trivial" class="confluence-external-resource icon" width="16" /> | RESOLVED | Fixed      | 1.0.1, 1.1.0                  |
| <a href="https://ecosystem.atlassian.net/browse/AO-675?src=confmacro" class="external-link">AO-675</a> | <a href="https://ecosystem.atlassian.net/browse/AO-675?src=confmacro" class="external-link">ao-plugin 1.1.x hanging webdriver tests with ao 1.1.0</a>                                     | <a href="https://ecosystem.atlassian.net/browse/AO-675?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="confluence-external-resource icon" /></a>         | Aug 27, 2015 | Sep 08, 2015 | Alex Courtis         | Alex Courtis         | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />                | RESOLVED | Fixed      | 1.1.0                         |
| <a href="https://ecosystem.atlassian.net/browse/AO-672?src=confmacro" class="external-link">AO-672</a> | <a href="https://ecosystem.atlassian.net/browse/AO-672?src=confmacro" class="external-link">&quot;multiple active objects configurations&quot; Errors On Restarting Dependent Plugins</a> | <a href="https://ecosystem.atlassian.net/browse/AO-672?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="confluence-external-resource icon" /></a>         | Aug 19, 2015 | Oct 28, 2015 | Alex Courtis         | Alex Courtis         | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />                | RESOLVED | Fixed      | 1.0.1, 1.1.0                  |
| <a href="https://ecosystem.atlassian.net/browse/AO-655?src=confmacro" class="external-link">AO-655</a> | <a href="https://ecosystem.atlassian.net/browse/AO-655?src=confmacro" class="external-link">Move activeobjects-bamboo-spi into Bamboo codebase</a>                                        | <a href="https://ecosystem.atlassian.net/browse/AO-655?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15311&amp;avatarType=issuetype" alt="New Feature" class="confluence-external-resource icon" /></a> | Jun 15, 2015 | Oct 09, 2015 | Krystian Brazulewicz | Krystian Brazulewicz | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />                | RESOLVED | Fixed      | 1.1.0                         |
| <a href="https://ecosystem.atlassian.net/browse/AO-635?src=confmacro" class="external-link">AO-635</a> | <a href="https://ecosystem.atlassian.net/browse/AO-635?src=confmacro" class="external-link">Table alias in order by clause in Postgres should not be quoted</a>                           | <a href="https://ecosystem.atlassian.net/browse/AO-635?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="confluence-external-resource icon" /></a>         | Mar 18, 2015 | Jan 11, 2016 | Unassigned           | Georg Schmidl        | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />                | RESOLVED | Fixed      | 1.1.0                         |
| <a href="https://ecosystem.atlassian.net/browse/AO-634?src=confmacro" class="external-link">AO-634</a> | <a href="https://ecosystem.atlassian.net/browse/AO-634?src=confmacro" class="external-link">Support for having clauses</a>                                                                | <a href="https://ecosystem.atlassian.net/browse/AO-634?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15311&amp;avatarType=issuetype" alt="New Feature" class="confluence-external-resource icon" /></a> | Mar 17, 2015 | Aug 31, 2015 | Alex Courtis         | Georg Schmidl        | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />                | RESOLVED | Fixed      | 1.1.0                         |
| <a href="https://ecosystem.atlassian.net/browse/AO-633?src=confmacro" class="external-link">AO-633</a> | <a href="https://ecosystem.atlassian.net/browse/AO-633?src=confmacro" class="external-link">Active Objects quotes table alias in group by clause in Postgres</a>                          | <a href="https://ecosystem.atlassian.net/browse/AO-633?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="confluence-external-resource icon" /></a>         | Mar 17, 2015 | Jan 11, 2016 | Alex Courtis         | Georg Schmidl        | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />                | RESOLVED | Fixed      | 1.1.0                         |
| <a href="https://ecosystem.atlassian.net/browse/AO-538?src=confmacro" class="external-link">AO-538</a> | <a href="https://ecosystem.atlassian.net/browse/AO-538?src=confmacro" class="external-link">Add NuoDB Support</a>                                                                         | <a href="https://ecosystem.atlassian.net/browse/AO-538?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="confluence-external-resource icon" /></a> | Jul 16, 2014 | Aug 26, 2015 | Alex Courtis         | Alex Courtis         | <img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="confluence-external-resource icon" />                | RESOLVED | Fixed      | 1.1.0                         |
| <a href="https://ecosystem.atlassian.net/browse/AO-213?src=confmacro" class="external-link">AO-213</a> | <a href="https://ecosystem.atlassian.net/browse/AO-213?src=confmacro" class="external-link">The activeobjects-plugin-0.17.2.x.jar ships with source for the net/ao package embedded.</a>  | <a href="https://ecosystem.atlassian.net/browse/AO-213?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="confluence-external-resource icon" /></a>         | Nov 06, 2011 | Oct 11, 2015 | James Winters        | Brenden Bain         | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="confluence-external-resource icon" />                | RESOLVED | Fixed      | 1.0.1, 1.1.0, 0.28.14, 0.29.4 |

<a href="https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&amp;jqlQuery=project+%3D+AO+AND+fixVersion+%3D+%221.1.0%22++++&amp;src=confmacro" class="external-link" title="View all matching issues in JIRA.">9 issues</a>




































































































































































































































































