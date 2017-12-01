---
aliases:
- /server/framework/atlassian-sdk/documenting-your-apis-with-the-atlassian-rest-api-browser-8945929.html
- /server/framework/atlassian-sdk/documenting-your-apis-with-the-atlassian-rest-api-browser-8945929.md
category: devguide
confluence_id: 8945929
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8945929
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8945929
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/rest-api-development/documenting-your-apis-with-the-atlassian-rest-api-browser
new_url: /server/framework/atlassian-sdk/documenting-your-apis-with-the-atlassian-rest-api-browser
platform: server
product: atlassian-sdk
subcategory: learning
title: Documenting your APIs with the Atlassian REST API Browser
---
# Documenting your APIs with the Atlassian REST API Browser

The Atlassian REST API Browser (RAB) is a tool for discovering REST and other types of remote APIs exposed by Atlassian applications. The RAB displays the APIs exposed by the application as well as by any plugins installed in the application.

The RAB is available as part of the <a href="https://marketplace.atlassian.com/plugins/com.atlassian.devrel.developer-toolbox-plugin" class="external-link">Developer Toolbox</a> or <a href="https://marketplace.atlassian.com/plugins/com.atlassian.labs.rest-api-browser" class="external-link">on its own</a>. Any developer instance of an Atlassian application has the Developer Toolbox included.

This page tells you how to use RAB to document any REST resources that you have added to an Atlassian application. (For more about how client developers would use the RAB, see [Using the REST API Browser](/server/framework/atlassian-sdk/using-the-rest-api-browser).)

## Adding a REST resource that will appear in RAB

If you add a REST API to a plugin using the SDK and install the plugin to the Atlassian application, the RAB automatically displays its REST API. You only need to add the API descriptions that you want to appear in the RAB.

To add those descriptions, use Javadoc annotations described in the Oracle guide to writing Javadoc comments: <a href="http://www.oracle.com/technetwork/java/javase/documentation/index-137868.html#tag" class="external-link">How to Write Doc Comments for the Javadoc Tool</a>. RAB will display the inline documentation inside the browser.

Note that:

-   There are some additional Javadoc tags that you can use to provide REST-specific documentation. 
-   You can also include a custom `application-doc.xml` file in your `src/main/resources/` folder that can provide any custom static documentation in the WADL file.
-   Mark your APIs with one of these annotations: `@PublicApi` or `@ExperimentalApi`. Any resource without one of these two annotations will be treated as private. These annotations are defined in the `atlassian-annotation` library, which your Atlassian application should already be using. Other developers who have your plugin installed will consider public APIs safe to use in their own code, whereas experimental APIs will be considered subject to change.

## RAB source

The RAB source code is <a href="https://bitbucket.org/atlassian/rest-api-browser" class="external-link">available on Bitbucket</a>.

##### RELATED TOPICS

<a href="/pages/createpage.action?spaceKey=RAB&amp;title=Overview+of+the+Atlassian+REST+API+Browser" class="createlink">Overview of the Atlassian REST API Browser</a>
































































































































































































