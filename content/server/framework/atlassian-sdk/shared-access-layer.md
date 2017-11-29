---
aliases:
- /server/framework/atlassian-sdk/shared-access-layer-5242946.html
- /server/framework/atlassian-sdk/shared-access-layer-5242946.md
category: devguide
confluence_id: 5242946
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5242946
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5242946
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/shared-access-layer
new_url: /server/framework/atlassian-sdk/shared-access-layer
platform: server
product: atlassian-sdk
subcategory: learning
title: Shared Access Layer
---
# Shared Access Layer

The Shared Access Layer, or SAL for short, provides a consistent, cohesive API to common plugin tasks, regardless of the Atlassian application into which your plugin is deployed. SAL is most useful for cross-application plugin development. If you are developing your plugin for a single application only, you can simply use the application's own API. If your plugin will run in two applications or more, you will find SAL's services useful. These common services include, but are not limited to:

-   Job scheduling
-   Internationalisation lookups
-   Persistence for plugin settings
-   A plugin upgrade framework

SAL is a component of the Atlassian plugin development platform. Check our [SAL availability guide](/server/framework/atlassian-sdk/sal-version-matrix), then take a look at the [SAL services](/server/framework/atlassian-sdk/sal-services). To view the changes made in each release of SAL, visit the <a href="https://ecosystem.atlassian.net/browse/SAL" class="external-link">SAL project page in JIRA</a>.

## Main Topics

**[Adding SAL Dependency](/server/framework/atlassian-sdk/adding-sal-dependency)**  
What to put in your plugin's pom to use SAL.

** **[**Atlassian Plugin SDK**](/server/framework/atlassian-sdk/index)  
Get started with developing an Atlassian plugin.

**[SAL Services](/server/framework/atlassian-sdk/sal-services)**  
Take a look at the services that SAL offers.

## Atlassian Development Hubs

-   [Atlassian Connect](https://developer.atlassian.com/static/connect/docs/)
-   [Developer Quick Start](https://developer.atlassian.com/display/DOCS/Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project)
-   [Plugin Framework](https://developer.atlassian.com/display/DOCS/Plugin+Framework)
-   [Gadgets](https://developer.atlassian.com/display/GADGETS)
-   [REST APIs](https://developer.atlassian.com/display/DOCS/REST+API+Development)
-   [Confluence](https://developer.atlassian.com/display/CONFDEV)
-   [Jira](https://developer.atlassian.com/display/JIRADEV)
-   [Jira Software](https://developer.atlassian.com/display/JIRADEV/JIRA+Software)
-   [Bamboo](https://developer.atlassian.com/display/BAMBOODEV)
-   [Crowd](https://developer.atlassian.com/display/CROWDDEV)
-   [Fisheye/Crucible](https://developer.atlassian.com/display/FECRUDEV)
-   [Jira Mobile Connect](https://developer.atlassian.com/display/JMC)

 

## Resources

<a href="http://docs.atlassian.com/sal-api/" class="external-link">Javadoc</a>

[Installation guide](/server/framework/atlassian-sdk/sal-version-matrix)

[Using SAL to store plugin settings](https://developer.atlassian.com/display/SAL/Storing+plugin+settings)

### Help

<a href="https://answers.atlassian.com/" class="external-link">Answers from the community</a>

<a href="http://my.atlassian.com/" class="external-link">Mailing lists at my.atlassian.com</a>

<a href="https://studio.atlassian.com/browse/SAL" class="external-link">Feature requests and bug reports</a>

<a href="http://blogs.atlassian.com/developer/" class="external-link">Atlassian developer blog</a>



















































































































































































































































