---
aliases:
- /server/framework/atlassian-sdk/plugin-development-platform-2.13-release-notes-8290316.html
- /server/framework/atlassian-sdk/plugin-development-platform-2.13-release-notes-8290316.md
category: devguide
confluence_id: 8290316
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8290316
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8290316
date: '2017-12-08'
legacy_title: Plugin Development Platform 2.13 Release Notes
platform: server
product: atlassian-sdk
subcategory: updates
title: Plugin Development Platform 2.13 release notes
---
# Plugin Development Platform 2.13 release notes

**18 October 2011** With pleasure, Atlassian presents the **Atlassian Plugin Development Platform 2.13**.

**Release Components:**

-   <a href="https://studio.atlassian.com/svn/PLUG/branches/atlassian-plugins-2.7.x" class="external-link">Plugin Framework</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10240&version=14684" class="external-link">2.10</a> (updated)
-   <a href="https://studio.atlassian.com/svn/SAL/branches/sal-2.5.x/" class="external-link">SAL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10108&version=13242" class="external-link">2.7</a> (updated)
-   <a href="https://studio.atlassian.com/svn/REST/branches/rest-2.4.x/" class="external-link">REST</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10292&version=13185" class="external-link">2.5</a>
-   <a href="https://studio.atlassian.com/svn/AJS/branches/auiplugin-3.4.x" class="external-link">AUI</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10270&version=12439" class="external-link">3.5</a>
-   <a href="https://studio.atlassian.com/svn/ATR/branches/atlassian-template-renderer-1.2.x" class="external-link">Template Renderer</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10301&version=11896" class="external-link">1.3</a>
-   <a href="https://studio.atlassian.com/svn/UPM/branches/atlassian-universal-plugin-manager-1.3.x" class="external-link">UPM</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10360&version=13235" class="external-link">1.5</a>
-   <a href="https://studio.atlassian.com/svn/EVENT/branches/atlassian-event-2.1.x/" class="external-link">EVENT</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10693&version=12210" class="external-link">2.1</a>
-   <a href="https://studio.atlassian.com/svn/OAUTH/branches/atlassian-oauth-1.2.x/" class="external-link">OAUTH</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10330&version=12282" class="external-link">1.3</a> (updated)
-   <a href="https://studio.atlassian.com/svn/TRUST/branches/atlassian-trusted-apps-2.4.x/" class="external-link">Trusted Apps</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10110&version=12452" class="external-link">2.5</a>
-   <a href="https://studio.atlassian.com/svn/APL/branches/applinks-3.4.x" class="external-link">APL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10130&version=12419" class="external-link">3.6.1</a> (updated)
-   <a href="https://studio.atlassian.com/svn/STRM/branches/activity-stream-4.1.x/" class="external-link">STRM</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10452&version=12406" class="external-link">5.0</a> (updated)

**What's in these release notes?**

These notes combine the releases of the plugin framework as well as other key plugins, libraries, and APIs that plugin developers depend on.

**What issues were resolved?**  
For a list of what issues were resolved in each platform component, click the version in the component table.

**Comments, requests and feedback**  
We would love your feedback. Please log your requests, bug reports and comments in our <a href="https://studio.atlassian.com/browse/PLUG" class="external-link">issue tracker</a>.

## Highlights of this release

1.  **Introducing Activity Streams**

    Activity stream presents a unified view of what's happening across linked Atlassian applications such as JIRA, Confluence, Bamboo, FishEye and Crucible. Imagine how convenient it would be to see a recent commit message from inside your JIRA dashboard!

2.  **Some UI improvements in OAuth**

    UI enhancements in OAuth plugin token administration page and authorisation form, plus a number of bug fixes. See <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10330&version=12282" class="external-link">Atlassian OAuth Plugin Release Notes</a> for details.

3.  **Shared Application Layer now supports retrieval of Server ID and SEN**

    The latest SAL 2.7 includes an API to retrieve server ID and Support Entitlement Number (SEN).

4.  **Introducing new API and user interface in Application Links**

    Application Links has new API and user interfaces that conform to the new OAuth specs. Using the new API, you can present a user interface that is more consistent across different products when requesting OAuth authorisation.

5.  **Extra packages in Java 7 are available**

    If you're running our products on Java 7, the new packages are now made available through your plugins. Simply state the required packages in OSGi import.
