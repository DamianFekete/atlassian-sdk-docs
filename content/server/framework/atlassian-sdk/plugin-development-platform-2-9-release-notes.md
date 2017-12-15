---
aliases:
- /server/framework/atlassian-sdk/plugin-development-platform-2.9-release-notes-852143.html
- /server/framework/atlassian-sdk/plugin-development-platform-2.9-release-notes-852143.md
category: devguide
confluence_id: 852143
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852143
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852143
date: '2017-12-08'
legacy_title: Plugin Development Platform 2.9 Release Notes
platform: server
product: atlassian-sdk
subcategory: updates
title: Plugin Development Platform 2.9 release notes
---
# Plugin Development Platform 2.9 release notes

**10 February 2011** With pleasure, Atlassian presents the **Atlassian Plugin Development Platform 2.9**.

**Release Components:** 

-   <a href="https://studio.atlassian.com/svn/PLUG/branches/atlassian-plugins-2.7.x" class="external-link">Plugin Framework</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10240&version=11993" class="external-link">2.7</a> (updated)
-   <a href="https://studio.atlassian.com/svn/SAL/branches/sal-2.5.x/" class="external-link">SAL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10108&version=12077" class="external-link">2.4</a>, see also <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10108&version=12003" class="external-link">2.3</a> (updated)
-   <a href="https://studio.atlassian.com/svn/REST/branches/rest-2.4.x/" class="external-link">REST</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10292&version=12218" class="external-link">2.4</a>, see also <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10292&version=12023" class="external-link">2.3</a>(updated)
-   <a href="https://studio.atlassian.com/svn/AJS/branches/auiplugin-3.4.x" class="external-link">AUI</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10270&version=11858" class="external-link">3.3</a> (updated)
-   <a href="https://studio.atlassian.com/svn/ATR/branches/atlassian-template-renderer-1.2.x" class="external-link">Template Renderer</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10301&version=11243" class="external-link">1.2</a>
-   <a href="https://studio.atlassian.com/svn/UPM/branches/atlassian-universal-plugin-manager-1.3.x" class="external-link">UPM</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10360&version=11968" class="external-link">1.2</a> (updated)
-   <a href="https://studio.atlassian.com/svn/EVENT/branches/atlassian-event-2.1.x/" class="external-link">EVENT</a> - verision <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10693&version=12064" class="external-link">2.0</a>
-   <a href="https://studio.atlassian.com/svn/OAUTH/branches/atlassian-oauth-1.2.x/" class="external-link">OAUTH</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10330&version=12125" class="external-link">1.2</a> (updated)
-   <a href="https://studio.atlassian.com/svn/TRUST/branches/atlassian-trusted-apps-2.4.x/" class="external-link">Trusted Apps</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10110&version=11823" class="external-link">2.3</a> (updated)
-   <a href="https://studio.atlassian.com/svn/APL/branches/applinks-3.4.x" class="external-link">APL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10130&version=12161" class="external-link">3.2</a> (updated)

**Wondering where are the Plugin Framework release notes?**  
Starting with Atlassian Plugin Development Platform 2.9, we've combined the releases of the plugin framework as well as other key plugins, libraries, and API's that plugin developers depend on into the Atlassian Plugin Development Platform. The platform has been used internally for many releases to test and deliver a set of capabilities our products and plugins could build upon, and starting with version 2.9, this platform has been made available to the public.

**What issues were resolved?**  
For a list of what issues were resolved in each platform component, click the version in the component version table.

**Comments, Requests and Feedback**  
We would love your feedback. Please log your requests, bug reports and comments in our <a href="http://jira.atlassian.com/browse/PLUG" class="external-link">issue tracker</a>.

## Highlights of this Release

1.  **New Universal Plugin Manager Plugin**

    This is the first release of the Plugin Development Platform that contains the Universal Plugin Manager. The Universal Plugin Manager lets system administrators dynamically install plugins from either local files or from <a href="http://plugins.atlassian.com" class="uri external-link">plugins.atlassian.com</a> as well as manage those plugins and modules.

2.  **New Application Links Plugin**

    This is the first release of the Plugin Development Platform that contains the Application Links Plugin. The Application Links Plugin is responsible for storing relationships with external Atlassian and non-Atlassian applications, as well as storing links between individual application entities such as JIRA projects or Confluence spaces. This gives system administrators a one-stop-shop for setting up relationships between external applications, including any authentication options. Furthermore, The Application Links Plugin provides an API for plugins, allowing them to easily contact external applications without having to ask for external URLs or authentication configuration information.

3.  **New Authentication Libraries**

    To support the new Application Links Plugin, the Trusted Applications library and Atlassian OAUTH plugin both received new releases and were added to the platform. Products using these will no longer contain administration screens for their configuration, but will rely on the Application Links Plugin to set their configuration.

4.  **Web Resource Conditions**

    Just like web links and sections can specify when they should be displayed, so now can web resources via a condition. This feature is particularly useful when combined with the web resource contexts feature that allows you to specify a context, or set of pages, that the web resource should appear. With the condition, you now can specify also when, within this context, it should appear allowing you to restrict its usage to only admins or during certain times.

5.  **Other Things Worth Mentioning**

    This release includes a number of improvements and bug fixes. Here are a few worth mentioning:

    -   Faster plugin startup
    -   More flexible plugin configuration (don't need atlassian-plugin.xml if you want to register modules dynamically)
    -   Plugins can now hook into the Spring ApplicationContext creation
    -   AUI has an i18n JavaScript web resource transformer to generate web resources containing i18n messages
    -   CSS Web resources can now specify CSS conditionals for better supporting later IE browsers
    -   <a href="http://docs.atlassian.com/aui/3.3.0/sandbox/sandbox.html" class="external-link">AUI Sandbox</a> now deployed with every release to let the developer experiment with AUI components
    -   REST now supports file uploads via `@MultipartFormParam`
