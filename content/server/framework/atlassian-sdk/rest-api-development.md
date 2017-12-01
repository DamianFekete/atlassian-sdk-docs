---
aliases:
- /server/framework/atlassian-sdk/rest-api-development-4915223.html
- /server/framework/atlassian-sdk/rest-api-development-4915223.md
category: devguide
confluence_id: 4915223
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915223
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915223
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/rest-api-development
new_url: /server/framework/atlassian-sdk/rest-api-development
platform: server
product: atlassian-sdk
subcategory: learning
title: REST API development
---
# REST API development

This page introduces you to using and developing REST APIs for Atlassian applications.

## REST and Atlassian Plugins

Atlassian applications expose REST APIs that developers can use to access services of the Atlassian platform remotely. The REST APIs are presented by the platform components as well as any plugins that have [implemented REST services](https://developer.atlassian.com/display/DOCS/Developing+a+REST+Service+Plugin). 

The REST APIs provide an alternative to the Java APIs used by in-process plugins. The REST APIs provide greater change-tolerance than in-process APIs. Before starting a plugin project, it's a good idea to start by looking at the REST APIs, even if you are developing a plugin intended to operate in-process with the host application. Of course, it's also the best option for developing remote applications that access Atlassian platform services. JIRA Studio is one example of such an application.

## Getting Started

To develop your own clients that use the Atlassian REST APIS, see the application-specific REST API documentation listed below. Also, the best place to get acquainted with the REST API available for use to a client application is by inspecting the target platform. Atlassian provides a tool for doing just that, the REST Application Browser (RAB). For information about the RAB, see [Using the REST API Browser](/server/framework/atlassian-sdk/using-the-rest-api-browser).

To create REST APIs in plugins you create for an Atlassian application, learn about the [Atlassian REST plugin module](/server/framework/atlassian-sdk/rest-plugin-module) and have a look at the tutorial, [Developing a REST Service Plugin](/server/framework/atlassian-sdk/developing-a-rest-service-plugin).

## Application-Specific REST API Documentation

[Bamboo REST APIs](https://developer.atlassian.com/display/BAMBOODEV/REST+APIs)  
[Confluence REST APIs](https://developer.atlassian.com/confdev/confluence-rest-api)  
[Crowd REST APIs](https://developer.atlassian.com/display/CROWDDEV/Overview+of+the+Crowd+REST+APIs)  
[FishEye/Crucible REST APIs](https://developer.atlassian.com/display/FECRUDEV/REST+API+Guide)  
[Jira REST APIs](https://developer.atlassian.com/display/JIRADEV/About+the+JIRA+REST+APIs)

## API Development

**[REST plugin module type](/server/framework/atlassian-sdk/rest-plugin-module)**

Use the REST module type to create plugin points in Atlassian applications, by exposing services and data entities as REST APIs.

 

## Tutorials

[Plugin Tutorial - Writing REST Services](/server/framework/atlassian-sdk/developing-a-rest-service-plugin)

[Using the FishEye REST API to Write a Gadget to Monitor Recent Changes](https://developer.atlassian.com/display/FECRUDEV/Plugin+Gadget+Tutorial+-+Using+the+FishEye+REST+API+to+Write+a+Gadget+to+Monitor+Recent+Changes)

## Help

<a href="https://answers.atlassian.com/" class="external-link">Answers from the community</a>

<a href="http://my.atlassian.com/" class="external-link">Mailing lists at my.atlassian.com</a>

<a href="https://studio.atlassian.com/browse/REST" class="external-link">Feature requests and bug reports</a>

<a href="http://blogs.atlassian.com/developer/" class="external-link">Atlassian developer blog</a>



































































































































































































