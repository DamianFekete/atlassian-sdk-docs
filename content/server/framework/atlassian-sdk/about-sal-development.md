---
aliases:
- /server/framework/atlassian-sdk/about-sal-development-5242930.html
- /server/framework/atlassian-sdk/about-sal-development-5242930.md
category: devguide
confluence_id: 5242930
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5242930
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5242930
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/shared-access-layer/about-sal-development
new_url: /server/framework/atlassian-sdk/about-sal-development
platform: server
product: atlassian-sdk
subcategory: learning
title: About SAL development
---
# About SAL development

The developer documentation is for people who want to use SAL when developing plugins for the Atlassian applications.

 

## About the Shared Access Layer (SAL)

The Shared Access Layer, or SAL for short, provides a consistent, cohesive API to common plugin tasks, regardless of the Atlassian application into which your plugin is deployed. SAL is most useful for cross-application plugin development. If you are developing your plugin for a single application only, you can simply use the application's own API. If your plugin will run in two applications or more, you will find SAL's services useful. These common services include, but are not limited to:

-   Job scheduling
-   Internationalisation lookups
-   Persistence for plugin settings
-   A plugin upgrade framework

SAL is one of the ingredients in the Atlassian plugin development platform, along with the Atlassian Plugin Framework version 2.

-   If you want to see the how SAL fits into the platform, take a look at the overview of the <a href="/pages/createpage.action?spaceKey=SAL&amp;title=Atlassian+Plugin+Development+Platform" class="createlink">plugin development platform</a>.
-   If you are interested in the Atlassian Plugin Framework 2, see the [plugin framework documentation](https://developer.atlassian.com/display/PLUGINFRAMEWORK).

## How it Works

The diagram below gives a conceptual overview of SAL as a layer between a plugin and the applications (JIRA, Confluence and FishEye). Let's assume that the plugin provides a portal on a JIRA dashboard, and that it needs to store a user preference setting.

![](/server/framework/atlassian-sdk/images/saloverview.png)

The dashboard plugin sends a request to SAL, asking for the preference to be saved in JIRA. SAL communicates with JIRA via the SAL JIRA plugin.

Alternatively, the dashboard plugin may need to save the preference in Confluence. The dashboard plugin will use the same SAL API call, specifying Confluence as the application. SAL will handle the communications with Confluence.

Here is another diagram, giving more detail of SAL in action. Again, let's assume that the dashboard plugin allows users to save a preference to JIRA.  
  
![](/server/framework/atlassian-sdk/images/sal-in-action-50pc.png)

## Using a SAL Service

To use a SAL service, you will need to declare a [component import module](/server/framework/atlassian-sdk/component-import-plugin-module) in your `atlassian-plugin.xml`. For example, if you want to get the UserManager, the component import would look like this:

``` xml
<component-import key="userManager" interface="com.atlassian.sal.api.user.UserManager" />
```

You also need to update you project's `pom.xml` to include SAL:

``` javascript
        <dependency>
            <groupId>com.atlassian.sal</groupId>
            <artifactId>sal-api</artifactId>
            <version>2.0.0</version>
            <scope>provided</scope>
        </dependency>
```

Please refer to the list of available [SAL services](https://developer.atlassian.com/display/SAL/SAL+Services).

##### RELATED TOPICS

[SAL Services](https://developer.atlassian.com/display/SAL/SAL+Services)  
[Plugin Framework](https://developer.atlassian.com/display/PLUGINFRAMEWORK)


























































































































































































































