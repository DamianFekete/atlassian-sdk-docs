---
aliases:
- /server/framework/atlassian-sdk/rest-plugin-2.2-release-notes-4915210.html
- /server/framework/atlassian-sdk/rest-plugin-2.2-release-notes-4915210.md
category: reference
confluence_id: 4915210
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915210
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915210
platform: server
product: atlassian-sdk
subcategory: updates
title: Rest Plugin 2.2 Release Notes 4915210
---
# REST plugin 2.2 release notes

**13 September 2010**

With pleasure, Atlassian presents the **Atlassian REST Plugin 2.2**.

Highlights of this release:

-   **Secure administration sessions.** Atlassian REST 2.2, when paired with [SAL 2.2](https://developer.atlassian.com/pages/viewpage.action?pageId=5242917), provides support for secure administration sessions, the aptly-named 'WebSudo'. Confluence already supports <a href="#websudo" class="unresolved">WebSudo</a>: When an administrator who is logged into Confluence attempts to access an administration function, they are prompted to log in again. Eventually, all the Atlassian applications will support WebSudo sessions. How can you get WebSudo with REST? See the [SAL documentation](/server/framework/atlassian-sdk/adding-websudo-support-to-your-plugin).

<!-- -->

-   **Faster startup time.** Now some Spring files are bundled with the REST plugin, thus minimising the effort of the plugin framework to load it. In addition, the REST plugin no longer bundles its own copy of JAXB, significantly reducing the number of classes it needs to load.

### Complete list of fixes in this release

| Key                                                                                                        | Summary                                                                                                                                                            | T                                                                                                                                                                                                                                                                                     | Created      | Updated      | Assignee      | Reporter       | P                                                                                                                                                | Status   | Resolution |     |
|------------------------------------------------------------------------------------------------------------|--------------------------------------------------------------------------------------------------------------------------------------------------------------------|---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|--------------|--------------|---------------|----------------|--------------------------------------------------------------------------------------------------------------------------------------------------|----------|------------|-----|
| <a href="https://ecosystem.atlassian.net/browse/REST-153?src=confmacro" class="external-link">REST-153</a> | <a href="https://ecosystem.atlassian.net/browse/REST-153?src=confmacro" class="external-link">standardize dependency versioning</a>                                | <a href="https://ecosystem.atlassian.net/browse/REST-153?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a>        | Sep 06, 2010 | Sep 28, 2015 | psongsiritat  | psongsiritat   | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" width="16" /> | RESOLVED | Fixed      |     |
| <a href="https://ecosystem.atlassian.net/browse/REST-151?src=confmacro" class="external-link">REST-151</a> | <a href="https://ecosystem.atlassian.net/browse/REST-151?src=confmacro" class="external-link">upgrade SAL to 2.2.0 beta9, PLUG to 2.6.0 beta2</a>                  | <a href="https://ecosystem.atlassian.net/browse/REST-151?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a>        | Sep 02, 2010 | Sep 28, 2015 | psongsiritat  | psongsiritat   | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |     |
| <a href="https://ecosystem.atlassian.net/browse/REST-149?src=confmacro" class="external-link">REST-149</a> | <a href="https://ecosystem.atlassian.net/browse/REST-149?src=confmacro" class="external-link">create a release note for rest 2.2.0</a>                             | <a href="https://ecosystem.atlassian.net/browse/REST-149?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a>        | Aug 31, 2010 | Sep 28, 2015 | Unassigned    | psongsiritat   | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |     |
| <a href="https://ecosystem.atlassian.net/browse/REST-147?src=confmacro" class="external-link">REST-147</a> | <a href="https://ecosystem.atlassian.net/browse/REST-147?src=confmacro" class="external-link">Create own host component import file to speed up startup</a>        | <a href="https://ecosystem.atlassian.net/browse/REST-147?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon confluence-external-resource" /></a> | Aug 25, 2010 | Sep 28, 2015 | Don Brown     | Don Brown      | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |     |
| <a href="https://ecosystem.atlassian.net/browse/REST-145?src=confmacro" class="external-link">REST-145</a> | <a href="https://ecosystem.atlassian.net/browse/REST-145?src=confmacro" class="external-link">Upgrade refapptest plugin to 4.2</a>                                 | <a href="https://ecosystem.atlassian.net/browse/REST-145?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a>        | Aug 09, 2010 | Sep 28, 2015 | Unassigned    | psongsiritat   | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |     |
| <a href="https://ecosystem.atlassian.net/browse/REST-144?src=confmacro" class="external-link">REST-144</a> | <a href="https://ecosystem.atlassian.net/browse/REST-144?src=confmacro" class="external-link">Upgrade SAL to 2.2 and Refapp to 2.7</a>                             | <a href="https://ecosystem.atlassian.net/browse/REST-144?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon confluence-external-resource" /></a> | Aug 02, 2010 | Sep 28, 2015 | Don Brown     | Don Brown      | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |     |
| <a href="https://ecosystem.atlassian.net/browse/REST-143?src=confmacro" class="external-link">REST-143</a> | <a href="https://ecosystem.atlassian.net/browse/REST-143?src=confmacro" class="external-link">Add a REST interceptor for the new WebSudo annotations (SAL 2.2)</a> | <a href="https://ecosystem.atlassian.net/browse/REST-143?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15318&amp;avatarType=issuetype" alt="Task" class="icon confluence-external-resource" /></a>        | Jul 26, 2010 | Sep 28, 2015 | Stefan Saasen | Stefan Saasen  | <img src="https://ecosystem.atlassian.net/images/icons/priorities/major.svg" alt="Major" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |     |
| <a href="https://ecosystem.atlassian.net/browse/REST-96?src=confmacro" class="external-link">REST-96</a>   | <a href="https://ecosystem.atlassian.net/browse/REST-96?src=confmacro" class="external-link">javax.xml.stream package imported from host application</a>           | <a href="https://ecosystem.atlassian.net/browse/REST-96?src=confmacro" class="external-link"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15310&amp;avatarType=issuetype" alt="Improvement" class="icon confluence-external-resource" /></a>  | Sep 23, 2009 | Sep 28, 2015 | Don Brown     | Andreas Knecht | <img src="https://ecosystem.atlassian.net/images/icons/priorities/minor.svg" alt="Minor" class="icon confluence-external-resource" />            | RESOLVED | Fixed      |     |

<a href="https://ecosystem.atlassian.net/secure/IssueNavigator.jspa?reset=true&amp;jqlQuery=project+%3D+REST+AND+fixVersion+%3D+2.2.0++&amp;src=confmacro" class="external-link" title="View all matching issues in JIRA.">8 issues</a>


























































































































































































