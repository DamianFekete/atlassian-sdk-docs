---
title: Browsing and Testing REST APIs in Your Application 8947336
aliases:
    - /server/framework/atlassian-sdk/browsing-and-testing-rest-apis-in-your-application-8947336.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8947336
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8947336
confluence_id: 8947336
platform:
product:
category:
subcategory:
---
# Documentation : Browsing and Testing REST APIs in your Application

The Atlassian REST API Browser (RAB) is a tool for discovering the REST APIs and other remote APIs available in Atlassian applications, including JIRA, Confluence, and the other Atlassian products.

RAB shows you all the REST and JSON-RPC resources in the application, displays the methods for each resource, and allows you to make test calls against the methods. If you have installed a plugin that creates additional REST resources for the application, RAB will also discover those resources.

This page tells you how to use RAB once you have got it up and running. If you have not already done so, please see [Running the REST API Browser in the Atlassian Plugin SDK](https://developer.atlassian.com/display/RAB/Running+the+REST+API+Browser+in+the+Atlassian+Plugin+SDK).

### Viewing resources and methods

The screenshots below show the REST API Browser running in JIRA 5.0.

**To view a REST API:**

1.  Go to the application's administration screen. For example:
    -   In JIRA: Click **Administration** at top right of the screen.
    -   In Confluence: Click **Browse** &gt; **Confluence Admin**.
2.  Click **REST API Browser**.
3.  Choose an API from the dropdown list at the top left of the screen. In this example, we have chosen the JIRA REST API (**Atlassian JIRA - Plugins - REST Plugin**):  
    <img src="/server/framework/atlassian-sdk/images/rab-chooseapi.png" class="confluence-thumbnail" />
4.  Choose a resource from the list on the left of the screen. In this example, we have chosen **/user/search**:  
    <img src="/server/framework/atlassian-sdk/images/rab-jirausersearch.png" class="confluence-thumbnail" />

For each resource, you can see the methods (for example: GET, POST, PUT) and the parameters available.

### Real-time testing

You can test a method in a resource by sending a request and viewing the response in real time.

**To send a request:**

1.  Enter the values for the **parameters**, as prompted.
2.  If required, add a **custom parameter**. This is useful under the following circumstances:
    -   Some of the resources in JIRA have implicit parameters that are not in the default parameter list. An example might be the `perPage` or the `startItem` parameter.
    -   The developer who added the REST resource may not have listed all the parameters in the Javadoc.
3.  Choose a **representation** from the options available. For example, `application/json`.
4.  Click **Execute**.

The screenshot below shows the REST API Browser running in JIRA 5.0. In this example, we are running a GET request using the `/user/search` resource, asking for details of username "admin". You can see:

-   A form, prompting you for the parameters relevant to the resource and method.
-   The request, as formulated by the REST API Browser.
-   The response headers.
-   The JSON in the response body.

<img src="/server/framework/atlassian-sdk/images/rab-testapi.png" class="confluence-thumbnail" />

##### RELATED TOPICS

<a href="/pages/createpage.action?spaceKey=RAB&amp;title=Overview+of+the+Atlassian+REST+API+Browser" class="createlink">Overview of the Atlassian REST API Browser</a>  
[Running the REST API Browser in the Atlassian Plugin SDK](https://developer.atlassian.com/display/RAB/Running+the+REST+API+Browser+in+the+Atlassian+Plugin+SDK)  
[Documenting your APIs with the Atlassian REST API Browser](https://developer.atlassian.com/display/RAB/Documenting+your+APIs+with+the+Atlassian+REST+API+Browser)


















































































































































































































































































































