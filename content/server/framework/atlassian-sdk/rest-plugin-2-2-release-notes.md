---
aliases:
- /server/framework/atlassian-sdk/rest-plugin-2.2-release-notes-4915210.html
- /server/framework/atlassian-sdk/rest-plugin-2.2-release-notes-4915210.md
category: reference
confluence_id: 4915210
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915210
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915210
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/rest-api-development/rest-plugin-release-notes/rest-plugin-2-2-release-notes
new_url: /server/framework/atlassian-sdk/rest-plugin-2-2-release-notes
platform: server
product: atlassian-sdk
subcategory: updates
title: REST plugin 2.2 release notes
---
# REST plugin 2.2 release notes

**13 September 2010**

With pleasure, Atlassian presents the **Atlassian REST Plugin 2.2**.

Highlights of this release:

-   **Secure administration sessions.** Atlassian REST 2.2, when paired with [SAL 2.2](https://developer.atlassian.com/pages/viewpage.action?pageId=5242917), provides support for secure administration sessions, the aptly-named 'WebSudo'. Confluence already supports ﻿<a href="#websudo" class="unresolved">WebSudo</a>: When an administrator who is logged into Confluence attempts to access an administration function, they are prompted to log in again. Eventually, all the Atlassian applications will support WebSudo sessions. How can you get WebSudo with REST? See the [SAL documentation](/server/framework/atlassian-sdk/adding-websudo-support-to-your-plugin).

<!-- -->

-   **Faster startup time.** Now some Spring files are bundled with the REST plugin, thus minimising the effort of the plugin framework to load it. In addition, the REST plugin no longer bundles its own copy of JAXB, significantly reducing the number of classes it needs to load.

### Complete List of Fixes in this Release

key

summary

priority

status

Unable to locate JIRA server for this macro. It may be due to Application Link configuration.




























































































































































































































