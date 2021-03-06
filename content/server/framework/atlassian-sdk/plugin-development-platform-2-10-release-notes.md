---
aliases:
- /server/framework/atlassian-sdk/plugin-development-platform-2.10-release-notes-851970.html
- /server/framework/atlassian-sdk/plugin-development-platform-2.10-release-notes-851970.md
category: devguide
confluence_id: 851970
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851970
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851970
date: '2017-12-08'
legacy_title: Plugin Development Platform 2.10 Release Notes
platform: server
product: atlassian-sdk
subcategory: updates
title: Plugin Development Platform 2.10 release notes
---
# Plugin Development Platform 2.10 release notes

**19 April 2011**With pleasure, Atlassian presents the **Atlassian Plugin Development Platform 2.10**.

**Release Components:**

-   <a href="https://studio.atlassian.com/svn/PLUG/branches/atlassian-plugins-2.7.x" class="external-link">Plugin Framework</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10240&version=11993" class="external-link">2.7</a>
-   <a href="https://studio.atlassian.com/svn/SAL/branches/sal-2.5.x/" class="external-link">SAL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10108&version=12367" class="external-link">2.5</a> (updated)
-   <a href="https://studio.atlassian.com/svn/REST/branches/rest-2.4.x/" class="external-link">REST</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10292&version=12218" class="external-link">2.4</a>
-   <a href="https://studio.atlassian.com/svn/AJS/branches/auiplugin-3.4.x" class="external-link">AUI</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10270&version=12234" class="external-link">3.4</a> (updated)
-   <a href="https://studio.atlassian.com/svn/ATR/branches/atlassian-template-renderer-1.2.x" class="external-link">Template Renderer</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10301&version=11243" class="external-link">1.2</a>
-   <a href="https://studio.atlassian.com/svn/UPM/branches/atlassian-universal-plugin-manager-1.3.x" class="external-link">UPM</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10360&version=12155" class="external-link">1.3</a> (updated)
-   <a href="https://studio.atlassian.com/svn/EVENT/branches/atlassian-event-2.1.x/" class="external-link">EVENT</a> - verision <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10693&version=12210" class="external-link">2.1</a> (updated)
-   <a href="https://studio.atlassian.com/svn/OAUTH/branches/atlassian-oauth-1.2.x/" class="external-link">OAUTH</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10330&version=12125" class="external-link">1.2</a>
-   <a href="https://studio.atlassian.com/svn/TRUST/branches/atlassian-trusted-apps-2.4.x/" class="external-link">Trusted Apps</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10110&version=12266" class="external-link">2.4</a> (updated)
-   <a href="https://studio.atlassian.com/svn/APL/branches/applinks-3.4.x" class="external-link">APL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10130&version=12346" class="external-link">3.4</a>, see also <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10130&version=12320" class="external-link">3.3</a> (updated)

**Wondering where are the Plugin Framework release notes?**  
Starting with Atlassian Plugin Development Platform 2.9, we've combined the releases of the plugin framework as well as other key plugins, libraries, and API's that plugin developers depend on into the Atlassian Plugin Development Platform. The platform has been used internally for many releases to test and deliver a set of capabilities our products and plugins could build upon, and starting with version 2.9, this platform has been made available to the public.

**What issues were resolved?**  
For a list of what issues were resolved in each platform component, click the version in the component version table.

**Comments, Requests and Feedback**  
We would love your feedback. Please log your requests, bug reports and comments in our <a href="https://studio.atlassian.com/browse/PLUG" class="external-link">issue tracker</a>.

1.  **Basic IE9 Compatibility in AUI**  
    With the release of IE9 several changes were required to fix regressions in IE9. See [AUI 3.4 Release Notes](https://developer.atlassian.com/display/AUI/AUI+3.4+Release+Notes) for details.

2.  **jQuery 1.5 upgrade in AUI**  
    jQuery 1.5 is a major release which brings <a href="http://blog.jquery.com/2011/01/31/jquery-15-released/" class="external-link">multiple new features</a>.
3.  **WebSudo can now be enabled while in Atlassian developer mode**

    Atlassian developer mode (-Datlassian.dev.mode=true) changes the host application behaviour to be more developer friendly in various ways. One optimisation disables WebSudo functionality in order to make testing easier and faster. -Datlassian.dev.websudo=true can be used to revert this while using the developer mode.

4.  **Universal Plugin Manager adds a new tab displaying useful information about the state of the host application's OSGi container**

    When Atlassian developer mode is enabled, Universal Plugin Manager contains a 'Developer' tab displaying useful information.

    ![Developer tab](/server/framework/atlassian-sdk/images/developer-tab.png)
