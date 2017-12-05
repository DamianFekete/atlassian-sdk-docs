---
aliases:
- /server/framework/atlassian-sdk/rest-plugin-2.1-release-notes-4915220.html
- /server/framework/atlassian-sdk/rest-plugin-2.1-release-notes-4915220.md
category: reference
confluence_id: 4915220
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915220
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915220
platform: server
product: atlassian-sdk
subcategory: updates
title: Rest Plugin 2.1 Release Notes 4915220
---
# REST plugin 2.1 release notes

**28 July 2010**With pleasure, Atlassian presents the **Atlassian REST Plugin 2.1**.

Atlassian REST 2.1, when paired with Seraph 2.2, provides more reliable use of REST resources by scripts and programs. The full explanation is a bit technical. Here's a developer's way of putting it into human-readable words:

> You know how after a while you get logged out of JIRA or Confluence. As a person you notice that pretty easily because the page just looks different. But a program isn't that smart. It doesn't know that it has suddenly been logged out and is now doing things as 'anonymous' and not 'jsmith'. The new REST + Seraph combination means they get an error message instead of just suddenly becoming 'anonymous' when using REST.

Do you generate your REST API documentation using the Jersey <a href="http://wikis.sun.com/display/Jersey/WADL" class="external-link">WADL</a>? With version 2.1 of the REST plugin, you can now have JSON examples as well as XML in your generated documentation. The plugin provides a new doclet based on `com.sun.jersey.wadl.resourcedoc.ResourceDoclet` that allows JSON examples. You will need to change your `pom.xml` to use this doclet.

This release also enables self-expansion of entities, along with other improvements described below.

### Complete List of Fixes in this Release

| Key                                                                                                        | Summary                                                                                                                                                            | T                                                                                                                                                                                                                                                                                     | Created      | Updated      | Assignee                        | Reporter                        | P                                                                                                                                                | Status   | Resolution |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|--------------|---------------------------------|---------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------|
| <a href="https://ecosystem.atlassian.net/browse/REST-141?src=confmacro" class="external-link">REST-141</a> | <a href="https://ecosystem.atlassian.net/browse/REST-141?src=confmacro" class="external-link">atlassian-rest-common doesn't export all packages</a>                | <a href="https://ecosystem.atlassian.net/browse/REST-141?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon confluence-external-resource" /></a>         | Jul 15, 2010 | Sep 28, 2015 | Luis Miranda \[OOO until 2018\] | Luis Miranda \[OOO until 2018\] | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" width="16" /> | RESOLVED | Fixed      |
| <a href="https://ecosystem.atlassian.net/browse/REST-140?src=confmacro" class="external-link">REST-140</a> | <a href="https://ecosystem.atlassian.net/browse/REST-140?src=confmacro" class="external-link">Enable self expanding functionality</a>                              | <a href="https://ecosystem.atlassian.net/browse/REST-140?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon confluence-external-resource" /></a> | Jul 08, 2010 | Sep 28, 2015 | Luis Miranda \[OOO until 2018\] | Luis Miranda \[OOO until 2018\] | <img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |
| <a href="https://ecosystem.atlassian.net/browse/REST-138?src=confmacro" class="external-link">REST-138</a> | <a href="https://ecosystem.atlassian.net/browse/REST-138?src=confmacro" class="external-link">Framework doesn't handle inherited ListWrapper fields</a>            | <a href="https://ecosystem.atlassian.net/browse/REST-138?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" alt="Bug" class="icon confluence-external-resource" /></a>         | Jul 02, 2010 | Sep 28, 2015 | Luis Miranda \[OOO until 2018\] | Luis Miranda \[OOO until 2018\] | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |
| <a href="https://ecosystem.atlassian.net/browse/REST-136?src=confmacro" class="external-link">REST-136</a> | <a href="https://ecosystem.atlassian.net/browse/REST-136?src=confmacro" class="external-link">add request attribute for /rest/ to force os_authType for seraph</a> | <a href="https://ecosystem.atlassian.net/browse/REST-136?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15311&amp;avatarType=issuetype" alt="New Feature" class="icon confluence-external-resource" /></a> | Jun 30, 2010 | Sep 28, 2015 | Justus Pendleton                | Justus Pendleton                | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |
| <a href="https://ecosystem.atlassian.net/browse/REST-134?src=confmacro" class="external-link">REST-134</a> | <a href="https://ecosystem.atlassian.net/browse/REST-134?src=confmacro" class="external-link">Allow for JSON examples in generated REST documentation</a>          | <a href="https://ecosystem.atlassian.net/browse/REST-134?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon confluence-external-resource" /></a> | Jun 28, 2010 | Sep 28, 2015 | Luis Miranda \[OOO until 2018\] | Luis Miranda \[OOO until 2018\] | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |

<a href="https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&amp;jqlQuery=project+%3D+REST+AND+fixVersion+%3D+2.1.0+&amp;src=confmacro" class="external-link" title="View all matching issues in JIRA.">5 issues</a>



























































































































































































