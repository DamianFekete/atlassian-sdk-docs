---
aliases:
- /server/framework/atlassian-sdk/plugin-development-platform-2.8-upgrade-guide-852113.html
- /server/framework/atlassian-sdk/plugin-development-platform-2.8-upgrade-guide-852113.md
category: devguide
confluence_id: 852113
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852113
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852113
date: '2017-12-08'
legacy_title: Plugin Development Platform 2.8 Upgrade Guide
platform: server
product: atlassian-sdk
subcategory: updates
title: Plugin Development Platform 2.8 upgrade guide
---
# Plugin Development Platform 2.8 upgrade guide

This upgrade guide documents the changes you need to make to the host application, when upgrading to the required versions of the modules of the Atlassian Plugin Development Platform. This guide is especially relevant for people who have [embedded](/server/framework/atlassian-sdk/embedding-the-plugin-framework) the Atlassian Plugin Framework into their own applications. It assumes the application is already using the previous version of the platform.

## Step 0. Review the Platform Release Notes

Take a look through the <a href="/server/framework/atlassian-sdk/plugin-development-platform-2-8-release-notes/" class="createlink">platform 2.8 release notes</a>, paying special attention to the linked release notes in any components of the platform.

## Step 1. Upgrade Platform Module Versions

Upgrade AUI to 3.2.0 (details at [AUI 3.2 Release Notes](https://developer.atlassian.com/display/AUI/AUI+3.2+Release+Notes). Note the action required to meet UI guidelines for dialog cancel controls.

## Step 2. Add web-resource-transformer Module Type

In the list of the plugin module descriptors your application supports, add `com.atlassian.plugin.webresource.transformer.WebResourceTransformerModuleDescriptor`. No additional application work is needed. See the documentation for this module type: [Web Resource Transformer Plugin Module](/server/framework/atlassian-sdk/web-resource-transformer-plugin-module).
