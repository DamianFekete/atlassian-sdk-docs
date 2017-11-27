---
aliases:
- /server/framework/atlassian-sdk/rest-plugin-2.1-release-notes-4915220.html
- /server/framework/atlassian-sdk/rest-plugin-2.1-release-notes-4915220.md
category: reference
confluence_id: 4915220
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915220
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915220
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/rest-api-development/rest-plugin-release-notes/rest-plugin-2-1-release-notes
new_url: /server/framework/atlassian-sdk/rest-plugin-2-1-release-notes
platform: server
product: atlassian-sdk
subcategory: updates
title: REST plugin 2.1 release notes
---
# REST plugin 2.1 release notes

**28 July 2010**

With pleasure, Atlassian presents the **Atlassian REST Plugin 2.1**.

Atlassian REST 2.1, when paired with Seraph 2.2, provides more reliable use of REST resources by scripts and programs. The full explanation is a bit technical. Here's a developer's way of putting it into human-readable words:

> You know how after a while you get logged out of JIRA or Confluence. As a person you notice that pretty easily because the page just looks different. But a program isn't that smart. It doesn't know that it has suddenly been logged out and is now doing things as 'anonymous' and not 'jsmith'. The new REST + Seraph combination means they get an error message instead of just suddenly becoming 'anonymous' when using REST.

Do you generate your REST API documentation using the Jersey <a href="http://wikis.sun.com/display/Jersey/WADL" class="external-link">WADL</a>? With version 2.1 of the REST plugin, you can now have JSON examples as well as XML in your generated documentation. The plugin provides a new doclet based on `com.sun.jersey.wadl.resourcedoc.ResourceDoclet` that allows JSON examples. You will need to change your `pom.xml` to use this doclet.

This release also enables self-expansion of entities, along with other improvements described below.

### Complete List of Fixes in this Release

key

summary

priority

status

Unable to locate JIRA server for this macro. It may be due to Application Link configuration.






























































































































































































































