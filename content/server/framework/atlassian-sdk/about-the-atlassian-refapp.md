---
aliases:
- /server/framework/atlassian-sdk/about-the-atlassian-refapp-2818632.html
- /server/framework/atlassian-sdk/about-the-atlassian-refapp-2818632.md
category: devguide
confluence_id: 2818632
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818632
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818632
date: '2017-12-08'
guides: guides
legacy_title: About the Atlassian RefApp
platform: server
product: atlassian-sdk
subcategory: learning
title: About the Atlassian RefApp
---
# About the Atlassian RefApp

The Atlassian Reference Application, or reference implementation, is known as the 'RefApp'. It is a model implementation of the Atlassian Plugin Framework 2. It takes the form of a simple web application, which implements the plugin framework and does not do much more than that.

 

## Purpose and Scope of the RefApp

The RefApp is useful to developers who want to develop cross-product plugins. A cross-product plugin is one that works with more than one Atlassian application. It is probably not of interest to developers wanting to write plugins for a specific Atlassian application.

In other words, if you are creating a plugin to be run in Confluence as well as JIRA, say, you could start by creating a RefApp plugin (by running `atlas-create-refapp-plugin`). If creating product-specific plugins, such as for JIRA or Confluence only, you would of course use the use the application-specific 'atlas-create' command.

## What Does the RefApp Do?

The RefApp is a demonstration application that represents the lowest common denominator of the Atlassian applications. It's a way of codifying the shared framework of all the applications.

Atlassian applications were built independently by different teams. We made many of the same technology choices, but no application is exactly like any other. By developing the RefApp, we can make sure that we do not depend on any functionality that JIRA provides but Confluence does not (for example). In the same way, the RefApp gives the applications an agreed-upon target to make sure they can support cross-application plugins.

## Creating your Plugin for the RefApp

To create a RefApp plugin, use the steps in [create a plugin skeleton](/server/framework/atlassian-sdk/creating-a-plugin-skeleton-with-the-atlassian-sdk) but run `atlas-create-refapp-plugin` to create the plugin project.

Now you can start the RefApp as described in the [SDK guide](/server/framework/atlassian-sdk/start-a-host-application-with-a-plugin-installed), using `atlas-run` to download and run the RefApp with your new plugin already installed.

This is the RefApp home page as displayed in a web browser:

<img src="/server/framework/atlassian-sdk/images/refapphome.png" width="650" />

The default login credentials for a system administrator account in the RefApp are admin/admin.

## Finding your Plugin in the RefApp

Once you have created your plugin and started the RefApp, you can verify that your plugin was installed by going to <a href="http://localhost:5990/refapp/index.jsp" class="uri external-link">localhost:5990/refapp/index.jsp</a>. Your plugin should appear in the list of plugins.

In addition to all installed plugins, the page shows bundle usage by the RefApp.

##### RELATED TOPICS

[atlas-create-refapp-plugin](/server/framework/atlassian-sdk/atlas-create-refapp-plugin)

















































































































































































































































































