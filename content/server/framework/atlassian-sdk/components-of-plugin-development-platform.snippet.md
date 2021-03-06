---
aliases:
- /server/framework/atlassian-sdk/-components-of-plugin-development-platform-2818473.html
- /server/framework/atlassian-sdk/-components-of-plugin-development-platform-2818473.md
category: devguide
confluence_id: 2818473
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818473
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818473
date: '2017-12-08'
legacy_title: _Components of Plugin Development Platform
platform: server
product: atlassian-sdk
subcategory: other
title: _Components of Plugin Development Platform
---
# \_Components of Plugin Development Platform

These are the major components in the Atlassian Plugin Development Platform:

-   **Shared Access Layer (SAL).** The API for accessing common services, regardless of the underlying Atlassian application interfaces. [More...](/server/framework/atlassian-sdk/shared-access-layer)
-   **Atlassian User Interface (AUI).** A set of reusable, cross-browser tested JavaScript and CSS UI components. [More...](https://developer.atlassian.com/display/AUI)
-   **Atlassian Template Renderer (ATR).** API for rendering your textual content. [More...](/server/framework/atlassian-sdk/atlassian-template-renderer)
-   **Atlassian Event.** A library that allows plugins to send and consume internal messages. See the <a href="http://docs.atlassian.com/atlassian-event/" class="external-link">Javadoc</a>.
-   **Activity Streams.** API for sending and consuming activity streams. [More...](/server/framework/atlassian-sdk/activity-streams)
-   **Gadgets.** Framework for developing OpenSocial gadgets. [More...](https://developer.atlassian.com/display/GADGETS)
-   **Universal Plugin Manager (UPM).** The tool for installing, managing, upgrading, and diagnosing Atlassian plugins. [More...](https://developer.atlassian.com/display/UPM)
-   **Atlassian REST Plugin Module.** An Atlassian plugin module that you can use to create plugin points easily in Atlassian applications, by exposing services and data entities as REST APIs. [More...](/server/framework/atlassian-sdk/rest-api-development)
-   **Trusted Apps.** Protocol for authenticating Atlassian applications.
-   **Application Links (AppLinks).** API for interacting with AppLinks, an Atlassian plugin module that allows you to connect to external applications. [More...](/server/framework/atlassian-sdk/application-links)
-   **OAuth.** Our OAuth implementation for accepting and sending authenticated requests.
-   **Plugin Framework.** The framework that executes the plugins and manages the available plugin modules. [More...](/server/framework/atlassian-sdk/plugin-framework)
-   **Active Objects.** For plugin data storage. An ORM layer that enables easier, faster and more scalable data access and storage than our old Bandana and PluginSettings APIs. [More...](/server/framework/atlassian-sdk/active-objects)
-   **Speakeasy.** A new, experimental extension mechanism for Atlassian's products. Useful for easy plugin prototyping. [More...](/server/framework/atlassian-sdk/speakeasy)
-   **JIRA Issue Collector.** Library for collecting user feedback from any page.
