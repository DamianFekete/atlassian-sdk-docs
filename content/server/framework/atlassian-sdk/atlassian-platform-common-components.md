---
aliases:
- /server/framework/atlassian-sdk/atlassian-platform-common-components-2818631.html
- /server/framework/atlassian-sdk/atlassian-platform-common-components-2818631.md
category: devguide
confluence_id: 2818631
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818631
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818631
date: '2017-12-08'
guides: guides
legacy_title: Atlassian Platform Common Components
platform: server
product: atlassian-sdk
subcategory: learning
title: Atlassian Platform common components
---
# Atlassian Platform common components

Using Atlassian's plugin development tools, developers can create plugins (add-ons) that extend the functionality of Atlassian applications such as [JIRA](https://developer.atlassian.com/display/JIRADEV), [Confluence](https://developer.atlassian.com/display/CONFDEV) and others. The Atlassian plugin development platform is a set of components upon which you can develop your plugin.This document gives an overview of those components.

## Components of the plugin development platform

![](/server/framework/atlassian-sdk/images/plugindevelopmentplatform.png)

These are the major components in the Atlassian Plugin Development Platform:

-   **Shared Access Layer (SAL).** The API for accessing common services, regardless of the underlying Atlassian application interfaces. [More...](https://developer.atlassian.com/display/DOCS/Shared+Access+Layer)
-   **Atlassian User Interface (AUI).** A set of reusable, cross-browser tested JavaScript and CSS UI components. [More...](https://developer.atlassian.com/display/AUI)
-   **Atlassian Template Renderer (ATR).** API for rendering your textual content. [More...](https://developer.atlassian.com/display/DOCS/Atlassian+Template+Renderer)
-   **Atlassian Event.** A library that allows plugins to send and consume internal messages. See the <a href="http://docs.atlassian.com/atlassian-event/" class="external-link">Javadoc</a>.
-   **Activity Streams.** API for sending and consuming activity streams. [More...](https://developer.atlassian.com/display/DOCS/Activity+Streams)
-   **Gadgets.** Framework for developing OpenSocial gadgets. [More...](https://developer.atlassian.com/display/GADGETS)
-   **Universal Plugin Manager (UPM).** The tool for installing, managing, upgrading, and diagnosing Atlassian plugins. [More...](https://developer.atlassian.com/display/UPM)
-   **Atlassian REST Plugin Module.** An Atlassian plugin module that you can use to create plugin points easily in Atlassian applications, by exposing services and data entities as REST APIs. [More...](https://developer.atlassian.com/display/DOCS/REST+API+Development)
-   **Trusted Apps.** Protocol for authenticating Atlassian applications.
-   **Application Links (AppLinks).** API for interacting with AppLinks, an Atlassian plugin module that allows you to connect to external applications. [More...](https://developer.atlassian.com/display/DOCS/Application+Links)
-   **OAuth.** Our OAuth implementation for accepting and sending authenticated requests.
-   **Plugin Framework.** The framework that executes the plugins and manages the available plugin modules. [More...](https://developer.atlassian.com/display/DOCS/Plugin+Framework)
-   **Active Objects.** For plugin data storage. An ORM layer that enables easier, faster and more scalable data access and storage than our old Bandana and PluginSettings APIs. [More...](https://developer.atlassian.com/display/DOCS/Active+Objects)
-   **Speakeasy.** A new, experimental extension mechanism for Atlassian's products. Useful for easy plugin prototyping. [More...](https://developer.atlassian.com/display/DOCS/Speakeasy)
-   **JIRA Issue Collector.** Library for collecting user feedback from any page.

## About plugins

A plugin is a bundle of code, resources and configuration files that can be dropped into an Atlassian product to add new functionality or change the behaviour of existing features.

Every plugin is made up of one or more plugin modules. A single plugin may do many things, while a plugin module represents a single function of the plugin.

There are two versions of plugins in the Atlassian Plugin Framework:

-   **Version 1 plugins.** These may be static (deployed in `WEB-INF/lib`) or dynamic (via the web UI, only in Confluence) and should work the same as they did in version 1 of the Atlassian Plugin Framework. The capabilities and features available to version 1 plugins vary significantly across products.
-   **Version 2 plugins.** These plugins are dynamically deployed on an internal <a href="http://osgi.org" class="external-link">OSGi</a> container to provide a consistent set of features and behaviours, regardless of the application the plugin is running on. Version 2 plugins have to be specifically declared as such, using the `plugins-version="2"` attribute in `atlassian-plugin.xml`.

## Version matrix

See [About the Platform](/server/framework/atlassian-sdk/about-the-platform).

## Using the plugin development platform dependency management POMs

If you would like to have just one version to change when upgrading to a new version of the Atlassian Plugin Development Platform, you can use the `atlassian-platform-libraries` and `atlassian-platform-plugins` POM artifacts to set the versions via Maven's <a href="http://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#Importing_Dependencies" class="external-link">&quot;import&quot; scope</a>. This will allow you to change the platform version and have all the appropriate versions of platform modules set automatically.


















































































































































































































































































