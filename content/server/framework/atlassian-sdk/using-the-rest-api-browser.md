---
aliases:
- /server/framework/atlassian-sdk/using-the-rest-api-browser-8945910.html
- /server/framework/atlassian-sdk/using-the-rest-api-browser-8945910.md
category: devguide
confluence_id: 8945910
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8945910
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8945910
date: '2017-12-08'
guides: guides
legacy_title: Using the REST API Browser
platform: server
product: atlassian-sdk
subcategory: learning
title: Using the REST API Browser
---
# Using the REST API Browser

 

The Atlassian REST API Browser (RAB) is a tool for discovering the REST APIs and other remote APIs available in Atlassian applications, including JIRA and Confluence.

The RAB shows you the REST and JSON-RPC resources in the application, displays the methods for each resource, and allows you to make test calls against the methods. The RAB shows you the core application resources, as well as any exposed by plugins you have installed as well. If the REST APIs use the prescribed <a href="http://www.oracle.com/technetwork/java/javase/documentation/index-137868.html#tag" class="external-link">Javadoc annotations</a>, you will also see inline documentation, including parameter descriptions.

## Getting the REST API Browser

Already using the [Atlassian Plugin SDK](https://developer.atlassian.com/display/DOCS/Working+with+the+SDK)? Then you already have the RAB. See "Using the REST API Browser locally" below to get started.

## Using the REST API Browser in Atlassian Cloud applications

Although the REST API Browser is included in JIRA Server, Confluence Server and Stash instances by default, or any application with the developer toolbox plugin, it is not available in Atlassian Cloud applications.

## Using the REST API Browser locally

To use the RAB on an Atlassian application instance started with the SDK, follow these steps:

1.  Run `atlas-run` or `atlas-debug` or `atlas-run-standalone` as usual. The Atlassian application (JIRA, Confluence, or any of the others) will be installed with the REST API Browser plugin enabled.
2.  Log in to the application as an administrator and navigate to the administration console.
3.  Click **REST API Browser** from the navigation menu (it's with the **ADVANCED** or **ADD-ONS** links).
4.  Choose a resource from the left menu. You can either browse through the list, or enter text in the **Search** field to filter the resources that are shown.  
    The resource page appears. Notice that the RAB displays the HTTP methods (GET, POST, PUT, and so on) applicable to each resource as tabs at the top of the page. It also contains fields for any parameters accepted by the resource.

    {{% note %}}

    After entering a search term, you can use the **Link to filtered results** to save or share a link to the filtered results. 

    {{% /note %}}

5.  To test a resource, enter any required parameter values in the fields and click **Send**.  
    The results appear in the Response section of the page, as shown by the following screenshot.  

    <img src="/server/framework/atlassian-sdk/images/newrabviewer.png" width="650" />

## Public versus Private APIs

By default, the RAB only shows the API resources that are specified to be public. However, you can clear the **Show only public APIs** checkbox to see private APIs as well.

However, we do not recommend using non-public APIs in your plugin or client code. Whether private or experimental, non-public APIs are subject to change and are not supported.

## Using the REST API Browser to document your APIs

If you are developing a Java plugin with a REST API of its own, you can ensure that RAB will document your REST resources too. See [Documenting your APIs with the Atlassian REST API Browser](/server/framework/atlassian-sdk/documenting-your-apis-with-the-atlassian-rest-api-browser).
























































































































































