---
aliases:
- /server/framework/atlassian-sdk/plugin-development-platform-2.11-release-notes-852078.html
- /server/framework/atlassian-sdk/plugin-development-platform-2.11-release-notes-852078.md
category: devguide
confluence_id: 852078
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852078
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852078
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/about-the-platform/plugin-development-platform-2-11-release-notes
new_url: /server/framework/atlassian-sdk/plugin-development-platform-2-11-release-notes
platform: server
product: atlassian-sdk
subcategory: updates
title: Plugin Development Platform 2.11 release notes
---
# Plugin Development Platform 2.11 release notes

**23 May 2011**With pleasure, Atlassian presents the **Atlassian Plugin Development Platform 2.11**.

**Release Components:** 

-   <a href="https://studio.atlassian.com/svn/PLUG/branches/atlassian-plugins-2.7.x" class="external-link">Plugin Framework</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10240&amp;version=12280" class="external-link">2.8</a> (updated)
-   <a href="https://studio.atlassian.com/svn/SAL/branches/sal-2.5.x/" class="external-link">SAL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10108&amp;version=12441" class="external-link">2.6</a> (updated)
-   <a href="https://studio.atlassian.com/svn/REST/branches/rest-2.4.x/" class="external-link">REST</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10292&amp;version=13185" class="external-link">2.5</a> (updated)
-   <a href="https://studio.atlassian.com/svn/AJS/branches/auiplugin-3.4.x" class="external-link">AUI</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10270&amp;version=12234" class="external-link">3.4</a>
-   <a href="https://studio.atlassian.com/svn/ATR/branches/atlassian-template-renderer-1.2.x" class="external-link">Template Renderer</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10301&amp;version=11896" class="external-link">1.3</a> (updated)
-   <a href="https://studio.atlassian.com/svn/UPM/branches/atlassian-universal-plugin-manager-1.3.x" class="external-link">UPM</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10360&amp;version=12985" class="external-link">1.4</a> (updated)
-   <a href="https://studio.atlassian.com/svn/EVENT/branches/atlassian-event-2.1.x/" class="external-link">EVENT</a> - verision <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10693&amp;version=12210" class="external-link">2.1</a>
-   <a href="https://studio.atlassian.com/svn/OAUTH/branches/atlassian-oauth-1.2.x/" class="external-link">OAUTH</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10330&amp;version=12125" class="external-link">1.2</a>
-   <a href="https://studio.atlassian.com/svn/TRUST/branches/atlassian-trusted-apps-2.4.x/" class="external-link">Trusted Apps</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10110&amp;version=12452" class="external-link">2.5</a> (updated)
-   <a href="https://studio.atlassian.com/svn/APL/branches/applinks-3.4.x" class="external-link">APL</a> - version <a href="https://studio.atlassian.com/secure/ReleaseNote.jspa?projectId=10130&amp;version=12419" class="external-link">3.5</a> (updated)

 

 

 

**Wondering where are the Plugin Framework release notes?**  
Starting with Atlassian Plugin Development Platform 2.9, we've combined the releases of the plugin framework as well as other key plugins, libraries, and API's that plugin developers depend on into the Atlassian Plugin Development Platform. The platform has been used internally for many releases to test and deliver a set of capabilities our products and plugins could build upon, and starting with version 2.9, this platform has been made available to the public.

**What issues were resolved?**  
For a list of what issues were resolved in each platform component, click the version in the component version table.

**Haven't used the Atlassian Plugin Framework yet?**  
Take a look at the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/developing-with-the-atlassian-plugin-sdk-23299291.html) and the [Plugin Framework documentation](/server/framework/atlassian-sdk/common-coding-tasks).

**Comments, Requests and Feedback**  
We would love your feedback. Please log your requests, bug reports and comments in our <a href="https://studio.atlassian.com/browse/PLUG" class="external-link">issue tracker</a>.

## Highlights of this Release

 

 

### 1. Conditional comments for JavaScript web resources

Earlier we have supported conditional comments for CSS files, which allows for example to enable a CSS file only for a specific browser. This release adds support for using conditional comments with JavaScript files. This is documented on the [Web Resource Module](https://developer.atlassian.com/display/CONFDEV/Web+Resource+Module) page.

Example:

``` xml
<resource type="download" name="html5.js" location="/scripts/html5.js">
<param name="conditionalComment" value="lt IE 9"/>
<param name="source" value="webContextStatic"/>
</resource>
```

 

 

### 2. TimeZone information

Plugins can now get the timezone of users and the timezone of the application. To use this module, import <a href="http://confluence.atlassian.com/display/SAL/SAL+Services#SALServices-%21package2.gif%21%7B%7Bcom.atlassian.sal.api.timezone%7D%7D" class="external-link">com.atlassian.sal.api.timezone.TimeZoneManager</a> in your atlassian-plugins.xml, it will be passed to the constructor of your module.

 

 

### 3. Multipart Requests

com.atlassian.sal.api.net.Request now supports the method setFiles(). It allows posting attachments to REST end points using the SAL request API. See [SAL Services](/server/framework/atlassian-sdk/sal-services)

 

 

### 4. Better logging of dynamic plugin module events

The logging is more explicit when the modules are activated or disabled, a "Disabling" state was created between Enabled and Disabled, and the key replaces the name when the name is unset.

 

 

### 5. Harmonize web-panel with web-item and web-section

These 3 elements now implement the same descriptor, so that web-panels can have labels like web-items. See [Web Panel Plugin Module](/server/framework/atlassian-sdk/web-panel-plugin-module)




















































































































































































































































