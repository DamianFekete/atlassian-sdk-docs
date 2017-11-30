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

| Key                                                                                                    | Summary                                                                                                                                                                  | T                                                                                                                                                                                                                                                                            | Created      | Updated      | Assignee         | Reporter         | P                                                                                                                                                | Status   | Resolution | Fix Version/S |
|--------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|--------------|------------------|------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------|---------------|
| <a href="https://ecosystem.atlassian.net/browse/AO-693?src=confmacro" class="external-link">AO-693</a> | <a href="https://ecosystem.atlassian.net/browse/AO-693?src=confmacro" class="external-link">Postgres 9.4 Testing</a>                                                     | <a href="https://ecosystem.atlassian.net/browse/AO-693?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a> | Oct 28, 2015 | Nov 30, 2015 | Elena Vasilyeva  | Alex Courtis     | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" width="16" /> | RESOLVED | Fixed      | 1.0.0         |
| <a href="https://ecosystem.atlassian.net/browse/AO-654?src=confmacro" class="external-link">AO-654</a> | <a href="https://ecosystem.atlassian.net/browse/AO-654?src=confmacro" class="external-link">Remove &quot;Missing Reverse OneToMany&quot; Warning</a>                     | <a href="https://ecosystem.atlassian.net/browse/AO-654?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a> | Jun 15, 2015 | Jul 03, 2015 | Unassigned       | Alex Courtis     | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      | 0.30.x, 1.0.0 |
| <a href="https://ecosystem.atlassian.net/browse/AO-648?src=confmacro" class="external-link">AO-648</a> | <a href="https://ecosystem.atlassian.net/browse/AO-648?src=confmacro" class="external-link">Add A Guard For Multiple Registrations Of Same &lt;ao&gt; Configuration</a>  | <a href="https://ecosystem.atlassian.net/browse/AO-648?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon confluence-external-resource" /></a>  | May 21, 2015 | Oct 28, 2015 | Alex Courtis     | Alex Courtis     | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |               |
| <a href="https://ecosystem.atlassian.net/browse/AO-643?src=confmacro" class="external-link">AO-643</a> | <a href="https://ecosystem.atlassian.net/browse/AO-643?src=confmacro" class="external-link">AO table for jira-development-integration-plugin is not created</a>          | <a href="https://ecosystem.atlassian.net/browse/AO-643?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon confluence-external-resource" /></a>  | May 13, 2015 | Jan 11, 2016 | Alex Courtis     | Eric Sukmajaya   | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      | 1.0.0         |
| <a href="https://ecosystem.atlassian.net/browse/AO-640?src=confmacro" class="external-link">AO-640</a> | <a href="https://ecosystem.atlassian.net/browse/AO-640?src=confmacro" class="external-link">Migrate From Deprecated AutowireCapable Plugin To ContainerManagedPlugin</a> | <a href="https://ecosystem.atlassian.net/browse/AO-640?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a> | May 03, 2015 | Jul 03, 2015 | Alex Courtis     | Alex Courtis     | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      | 0.30.x, 1.0.0 |
| <a href="https://ecosystem.atlassian.net/browse/AO-592?src=confmacro" class="external-link">AO-592</a> | <a href="https://ecosystem.atlassian.net/browse/AO-592?src=confmacro" class="external-link">back down from H2 1.4 (beta) to 1.3 (stable)</a>                             | <a href="https://ecosystem.atlassian.net/browse/AO-592?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a> | Jan 29, 2015 | Jul 03, 2015 | Alex Courtis     | Alex Courtis     | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      | 1.0.0         |
| <a href="https://ecosystem.atlassian.net/browse/AO-569?src=confmacro" class="external-link">AO-569</a> | <a href="https://ecosystem.atlassian.net/browse/AO-569?src=confmacro" class="external-link">Update to Spring 4.1.4+</a>                                                  | <a href="https://ecosystem.atlassian.net/browse/AO-569?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a> | Oct 30, 2014 | Jul 03, 2015 | Unassigned       | Marcos Scriven   | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      | 1.0.0         |
| <a href="https://ecosystem.atlassian.net/browse/AO-488?src=confmacro" class="external-link">AO-488</a> | <a href="https://ecosystem.atlassian.net/browse/AO-488?src=confmacro" class="external-link">50 ActiveObject Entity limit per add-on? YGTBKM! Now it's 200</a>            | <a href="https://ecosystem.atlassian.net/browse/AO-488?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon confluence-external-resource" /></a>  | Nov 22, 2013 | Jul 01, 2016 | Alex Courtis     | Andy Brook       | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      | 0.30.x, 1.0.0 |
| <a href="https://ecosystem.atlassian.net/browse/AO-639?src=confmacro" class="external-link">AO-639</a> | <a href="https://ecosystem.atlassian.net/browse/AO-639?src=confmacro" class="external-link">Release new version of AO that has a more recent amps version</a>            | <a href="https://ecosystem.atlassian.net/browse/AO-639?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a> | Apr 30, 2015 | Jul 03, 2015 | Martin Henderson | Martin Henderson | <img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon confluence-external-resource" />            | RESOLVED | Fixed      | 1.0.0         |
| <a href="https://ecosystem.atlassian.net/browse/AO-637?src=confmacro" class="external-link">AO-637</a> | <a href="https://ecosystem.atlassian.net/browse/AO-637?src=confmacro" class="external-link">&lt;ao&gt; Modules Are Keyed By &lt;plugin-key&gt; Only</a>                  | <a href="https://ecosystem.atlassian.net/browse/AO-637?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon confluence-external-resource" /></a>  | Apr 15, 2015 | Aug 27, 2015 | Unassigned       | Alex Courtis     | <img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |               |

<a href="https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&amp;jqlQuery=project+%3D+AO+and+fixVersion+%3D+%221.0.0%22+order+by+priority+desc++&amp;src=confmacro" class="external-link" title="View all matching issues in JIRA.">10 issues</a>










































































































































































































































