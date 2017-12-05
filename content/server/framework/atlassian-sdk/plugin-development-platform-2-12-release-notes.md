---
aliases:
- /server/framework/atlassian-sdk/plugin-development-platform-2.12-release-notes-7897299.html
- /server/framework/atlassian-sdk/plugin-development-platform-2.12-release-notes-7897299.md
category: devguide
confluence_id: 7897299
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=7897299
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=7897299
platform: server
product: atlassian-sdk
subcategory: updates
title: Plugin Development Platform 2.12 Release Notes 7897299
---
# Plugin Development Platform 2.12 release notes

**10 August 2011**With pleasure, Atlassian presents the **Atlassian Plugin Development Platform 2.12**.

**  
**

**Release Components:** 

-   <a href="https://studio.atlassian.com/svn/PLUG/branches/atlassian-plugins-2.7.x" class="external-link">Plugin Framework</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10240&amp;version=13186" class="external-link">2.9</a> (updated)
-   <a href="https://studio.atlassian.com/svn/SAL/branches/sal-2.5.x/" class="external-link">SAL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10108&amp;version=12441" class="external-link">2.6</a>
-   <a href="https://studio.atlassian.com/svn/REST/branches/rest-2.4.x/" class="external-link">REST</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10292&amp;version=13185" class="external-link">2.5</a>
-   <a href="https://studio.atlassian.com/svn/AJS/branches/auiplugin-3.4.x" class="external-link">AUI</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10270&amp;version=12439" class="external-link">3.5</a> (updated)
-   <a href="https://studio.atlassian.com/svn/ATR/branches/atlassian-template-renderer-1.2.x" class="external-link">Template Renderer</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10301&amp;version=11896" class="external-link">1.3</a>
-   <a href="https://studio.atlassian.com/svn/UPM/branches/atlassian-universal-plugin-manager-1.3.x" class="external-link">UPM</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10360&amp;version=13235" class="external-link">1.5</a> (updated)
-   <a href="https://studio.atlassian.com/svn/EVENT/branches/atlassian-event-2.1.x/" class="external-link">EVENT</a> - verision <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10693&amp;version=12210" class="external-link">2.1</a>
-   <a href="https://studio.atlassian.com/svn/OAUTH/branches/atlassian-oauth-1.2.x/" class="external-link">OAUTH</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10330&amp;version=12125" class="external-link">1.2</a>
-   <a href="https://studio.atlassian.com/svn/TRUST/branches/atlassian-trusted-apps-2.4.x/" class="external-link">Trusted Apps</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10110&amp;version=12452" class="external-link">2.5</a>
-   <a href="https://studio.atlassian.com/svn/APL/branches/applinks-3.4.x" class="external-link">APL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10130&amp;version=12419" class="external-link">3.5</a>

**Wondering where the Plugin Framework release notes are?**  
Starting with Atlassian Plugin Development Platform 2.9, we've combined the releases of the plugin framework as well as other key plugins, libraries, and API's that plugin developers depend on into the Atlassian Plugin Development Platform. The platform has been used internally for many releases to test and deliver a set of capabilities our products and plugins can build upon. From version 2.9, this platform is available to the public.

**What issues were resolved?**  
For a list of the issues resolved in each platform component, click the version in the table of components.

**Comments, Requests and Feedback**  
We would love your feedback. Please log your requests, bug reports and comments in our <a href="https://studio.atlassian.com/browse/PLUG" class="external-link">issue tracker</a>.

 

## Highlights of this Release

### 1 Universal Plugin Manager can now work entirely offline

 

When the plugin exchange server is unavailable, the Universal Plugin Manager will not try to access the Atlassian Plugin Exchange. See <a href="http://confluence.atlassian.com/display/UPM/Problems+Connecting+to+the+Atlassian+Plugin+Exchange" class="external-link">Problems Connecting to the Atlassian Plugin Exchange</a>. Instead it can work entirely offline.

 

### 2 Notification of plugin upgrades on administration page

 

Once a day the plugin manager will run a check in the background if there is any plugins that needs to be updated. Whenever upgrades are available, it will notify the administrators on the administration console screens. You don't have to go to the universal plugin manager screen anymore!

 

### 3 Various improvements in AUI

 

 

AUI has many new features including <a href="http://documentcloud.github.com/underscore/" class="external-link">Underscore.js</a>, new methods to get contextPath, the escapeHtml method that avoids XSS vulnerabilities, new default design for tables and a lot more. Try it for yourself in the <a href="http://docs.atlassian.com/aui/3.5.0/sandbox/" class="external-link">sandbox</a>. See the [AUI 3.5 Release Notes](https://developer.atlassian.com/display/AUI/AUI+3.5+Release+Notes) for details.

### 4 New context batching

 

This version of the plugin framework introduces context batching. This lowers the number of CSS and JavaScript requests. thus improving page loading performance.














































































































































































































































































