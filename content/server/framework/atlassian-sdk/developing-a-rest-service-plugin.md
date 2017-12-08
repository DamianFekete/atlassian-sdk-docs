---
aliases:
- /server/framework/atlassian-sdk/developing-a-rest-service-plugin-2818694.html
- /server/framework/atlassian-sdk/developing-a-rest-service-plugin-2818694.md
category: devguide
confluence_id: 2818694
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818694
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818694
date: '2017-12-08'
guides: tutorials
legacy_title: Developing a REST Service Plugin
platform: server
product: atlassian-sdk
subcategory: learning
title: Developing a REST service plugin
---
# Developing a REST service plugin

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Applicable:</p></td>
<td><p>This tutorial applies to <strong>RefApp 3.3.6</strong></p></td>
</tr>
<tr class="even">
<td><p>Level of experience:</p></td>
<td><p>This is an intermediate tutorial. You should have completed at least one beginner tutorial before working through this tutorial. See the <a href="/server/framework/atlassian-sdk/tutorials">list of tutorials in DAC</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Time estimate:</p></td>
<td><p>It should take you approximately half an hour to complete this tutorial.</p></td>
</tr>
</tbody>
</table>

 

## About this tutorial

In this tutorial, you will create a plugin that exposes a REST service. Behind the scenes, Atlassian REST services are implemented with <a href="http://jersey.java.net" class="external-link">Jersey</a>, which is the reference implementation of the <a href="https://jsr311.java.net/" class="external-link">JSR-311</a> standard.

{{% note %}}

Any REST API added by a plugin should resemble, as much as possible, the form of the REST interfaces already exposed by the platform and other plugins. This makes life easier for those who want to use your API. You can make sure your API fits in with the others by following the [Atlassian REST API design guidelines](https://developer.atlassian.com/display/REST/Atlassian+REST+API+Design+Guidelines+version+1).

{{% /note %}}

We will create the service in a plugin built for the Atlassian reference application, *RefApp*. The RefApp encapsulates common components of the Atlassian platform. Thus, it serves as a platform against which you can create plugins targeted for multiple Atlassian applications.

### Plugin source code

We encourage you to work through this tutorial. If you want to skip ahead or check your work when you are done, you can find the plugin source code on Atlassian Bitbucket. To clone the repository, issue the following command:

``` bash
git clone git@bitbucket.org:serverecosystem/message.git
```

Alternatively, you can download the source using the **get source** option here:

<a href="https://bitbucket.org/serverecosystem/message" class="uri external-link">https://bitbucket.org/serverecosystem/message</a>

## Step 1. Create the plugin project

In this step, you use an `atlas-` command to create your plugin project. The `atlas-` commands are part of the Atlassian Plugin SDK, and automate much of the work of plugin development for you.

1.  Open a terminal and navigate to the directory where you want to create your REST plugin project home directory.
2.  Enter the following command:

    ``` bash
    atlas-create-refapp-plugin
    ```

3.  When prompted, enter the following values for your plugin project parameters:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <tbody>
    <tr class="odd">
    <td><p>group-id</p></td>
    <td><p><code>com.atlassian.plugins.tutorial</code></p></td>
    </tr>
    <tr class="even">
    <td><p>artifact-id</p></td>
    <td><code>Message</code></td>
    </tr>
    <tr class="odd">
    <td><p>version</p></td>
    <td><p><code>1.0</code></p></td>
    </tr>
    <tr class="even">
    <td><p>package</p></td>
    <td><p><code>com.atlassian.plugins.tutorial</code></p></td>
    </tr>
    </tbody>
    </table>

4.  Confirm your entries when prompted.

The command creates a directory named `Message` with all the initial project files. This tutorial refers to this directory as your project home. Unless otherwise indicated, all directory paths are relative to the project home.

## Step 2. Add the REST module

So far, we have a basic plugin project with a POM file, descriptor file, and an example servlet. Let's add the REST module to the project, again using the Atlassian Plugin SDK:

1.  Change to the new `Message` directory.
2.  Run the following command:

    ``` bash
    atlas-create-refapp-plugin-module
    ```

3.  Enter 7, REST Module Plugin. 
4.  At the prompts, enter values for the classname, package name, REST path on which to serve your resource, and version. Alternatively, you can accept the suggested values for these properties by just hitting enter. Here are the defaults:    
    -   Classname: MyRestResource
    -   Package Name: com.atlassian.plugins.tutorial.rest
    -   REST path: /myrestresource
    -   Version: 1.0 

    The remaining instructions assume the use of the default options. If you enter other values, you will need to adjust certain details, such as the URL for accessing the service.
5.  Enter N when prompted to show advanced setup options.
6.  Enter N when asked whether you'd like to add another plugin module.

The SDK finishes up, adding REST source files to the project. 

## Step 3. Look over the source files

Navigate to the following directory: 

``` bash
<project_home>/src/main/java/com/atlassian/plugins/tutorial/rest/
```

 

This directory contains two source files that implement the REST services: 

-   `MyRestResource.java` 
-   `MyRestResourceModel.java`

Open the files to have a look. Notice the contents of `MyRestResource.java`. The `getMessage()` method returns the canonical "Hello World" message.

Also notice the annotations. These are <a href="https://jaxb.java.net/nonav/jaxb20-pfd/api/index.html" class="external-link">JAXB</a> annotations. For your reference, here's a rundown of what they are, starting with those in `MyRestResource.java`. 

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Annotation</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>@Path</code></p></td>
<td><p>Identifies the URI path that a resource class or class method will serve requests for. <code>@Path</code> annotations on methods are relative to the <code>@Path</code> annotation on the enclosing class.</p>
<p><strong>Source:</strong> <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/Path.html" class="external-link">Path</a></p>
<p><strong>Scope:</strong> Class or Method</p></td>
</tr>
<tr class="even">
<td><p><code>@GET</code></p></td>
<td><p>Identifies that the class method will handle requests for a GET http message. Having more than one @GET annotation on a method in a class will fail unless @Path annotations are used to distinguish them. Other annotations are available such as <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/DELETE.html" class="external-link">DELETE</a>, <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/POST.html" class="external-link">POST</a>, <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/HEAD.html" class="external-link">HEAD</a>, etc.  See: <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/package-summary.html" class="external-link">javax.ws.rs</a>.</p>
<p><strong>Source:</strong> <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/GET.html" class="external-link">GET</a></p>
<p><strong>Scope:</strong> Method</p></td>
</tr>
<tr class="odd">
<td><p><code>@AnonymousAllowed</code></p></td>
<td><p>Identifies that the method can be called without supplying user credentials. If this annotation did not exist then a session would need to be established with your application or you would need to pass in os_username and os_password parameters.</p>
<p><strong>Scope:</strong> Method</p></td>
</tr>
<tr class="even">
<td><p><code>@Produces</code></p></td>
<td><p>It specifies the content types the method may return. If this annotation is not present, the method may return any content type; if it is present, the method must return one of the types specified.</p>
<p>Source: <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/Produces.html" class="external-link">Produces</a></p>
<p><strong>Scope:</strong> Method</p></td>
</tr>
<tr class="odd">
<td><p><code>@XmlRootElement</code></p></td>
<td><p>Maps a class or an enum type to an XML element.</p>
<p><strong>Source:</strong> <a href="https://jaxb.java.net/nonav/jaxb20-pfd/api/javax/xml/bind/annotation/XmlRootElement.html" class="external-link">XmlRootElement</a></p>
<p><strong>Scope:</strong> Class or enum</p></td>
</tr>
<tr class="even">
<td><p><code>@XmlAccessorType</code></p></td>
<td><p>Controls whether fields or properties are serialised by default.</p>
<p><strong>Source:</strong> <a href="https://jaxb.java.net/nonav/jaxb20-pfd/api/javax/xml/bind/annotation/XmlAccessorType.html" class="external-link">XmlAccessorType</a></p>
<p><strong>Scope:</strong> Class or enum</p></td>
</tr>
<tr class="odd">
<td><p><code>@XmlAttribute</code></p></td>
<td><p>Maps a property or field to an XML Attribute.</p>
<p><strong>Source:</strong> <a href="https://jaxb.java.net/nonav/jaxb20-pfd/api/javax/xml/bind/annotation/XmlAttribute.html" class="external-link">XmlAttribute</a></p>
<p><strong>Scope:</strong> Property or field</p></td>
</tr>
</tbody>
</table>

We'll build on the source code--including the annotations--in a bit. But first let's try running the plugin.

## Step 4. Run the plugin

Start the RefApp using the following SDK command. Thanks to some SDK magic, your plugin is loaded in the application automatically:

``` bash
atlas-run
```

The first time you run the command, the application takes a few minutes to download packages and other resources needed for the RefApp.

When the application finishes starting up, you can use a REST browser or just a plain web browser to test the service. If you use the default project settings, the service is exposed at the following URL: 

`http://<host>:5990/refapp/rest/myrestresource/1.0/message`

Substitute *`<host>`* with the host name appropriate for your Atlassian application.

You should see a page with text that resembles:

``` xml
This XML file does not appear to have any style information associated with it. The document tree is shown below.
<message key="default">
    <value>Hello World</value>
</message>
```

After confirming the service works, shut down the RefApp by returning to the terminal where you started the RefApp and entering Ctrl-C.

## Step 5. Extend the plugin with parameters

We've got our "Hello World" message working, but let's make our plugin more flexible by parameterizing it. Specifically, we'll allow the caller to pass a parameter that is used as the resource identity (from the REST client's point-of-view). It also populates the body of the response message, replacing the "Hello World" string.

While this isn't necessarily a realistic example of a REST implementation, it illustrates at a high level two approaches for implementing REST services.

1.  Open `MyRestResource.java` for editing.
2.  Replace the `getMessage()` method with this:

    ``` java
    public Response getMessage(@QueryParam("key") String key)
    {
       if(key!=null)
          return Response.ok(new MyRestResourceModel(key, getMessageFromKey(key))).build();
       else
          return Response.ok(new MyRestResourceModel("default","Hello World")).build();
    }
    ```

3.  Add two new methods, one of which takes a path parameter and another that takes a query parameter.

    ``` java
    @GET
    @AnonymousAllowed
    @Produces({MediaType.APPLICATION_JSON, MediaType.APPLICATION_XML})
    @Path("/{key}")
    public Response getMessageFromPath(@PathParam("key") String key)
    {
       return Response.ok(new MyRestResourceModel(key, getMessageFromKey(key))).build();
    }

    private String getMessageFromKey(String key) {
       // In reality, this data would come from a database or some component
       // within the hosting application, for demonstration purpopses I will
       // just return the key
       return key;
    }
    ```

4.  Open `MyRestResourceModel.java` and add a new element declaration:

    ``` java
    @XmlAttribute
    private String key;
    ```

5.  Replace the class constructor with this one:

    ``` java
    public MyRestResourceModel(String key, String message) {
       this.key = key;
       this.message = message;
    }
    ```

6.  Finally, add two new methods to the class:

    ``` java
    public String getKey() {
       return key;
    }
     
    public void setKey(String key) {
       this.key = key;
    }
    ```

Notice we've added a few more annotations: 

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Annotation</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>@XmlElement</code></p></td>
<td><p>Maps a property or field to an XML Element.</p>
<p><strong>Source:</strong> <a href="https://jaxb.java.net/nonav/jaxb20-pfd/api/javax/xml/bind/annotation/XmlElement.html" class="external-link">XmlElement</a></p>
<p><strong>Scope:</strong> Property or field</p></td>
</tr>
<tr class="even">
<td><p><code>@PathParam</code></p></td>
<td><p>It maps a method variable to an element in the @Path.</p>
<p><strong>Source:</strong> <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/PathParam.html" class="external-link">PathParam</a></p>
<p><strong>Scope:</strong> Method Parameter</p></td>
</tr>
<tr class="odd">
<td><p><code>@QueryParam</code></p></td>
<td><p>It maps a method variable to a query parameter.</p>
<p><strong>Source:</strong> <a href="https://jsr311.java.net/nonav/javadoc/javax/ws/rs/QueryParam.html" class="external-link">QueryParam</a></p>
<p><strong>Scope:</strong> Method Parameter</p></td>
</tr>
</tbody>
</table>

That's it! We've parameterized the REST resource in a couple of ways: we've enabled the service to accept parameters as either a query parameter or as value in the path. In a more realistic implementation, the REST resources might be dynamically composed in some other manner, such as by using values from a database. The following tip provides more information on the two approaches used by our plugin.

{{% tip %}}

**When should I use** `PathParams` **or** `QueryParams`**?**  
Since you can map information from the request into the method in different ways, you may be wondering when to use `PathParams` over `QueryParams`. Here are some guidelines for you to think about.

Query parameters usually mean the resource will not be cached by a proxy or your browser. So if you're passing in an `id` to find some information about some sort of entity, then use a path parameter.

On the other hand, if your input is something that might be changed with your data (like a user's full name), then you should use a query parameter. Your aim should be to provide a single authoritative URL for your resources so your clients can predict and cache its results. If a user got married and you used their name in the URL then it might change and caches and links would now fail.

{{% /tip %}}

 

## Step 6. Adjust the test code

When we used the SDK to add the REST module to our project, the SDK helpfully added some tests for the code it generated. However, if we run `atlas-run` the same way we did before, we'll get a test build failure due to modifications we made to the source code. The method under test now expects a parameter.

We'll leave the full explanation of testing matters to [another tutorial](https://developer.atlassian.com/display/DOCS/Writing+and+Running+Plugin+Tests) for now, and just make a small adjustment to our tests to get them working:

1.  Navigate to the test directory for the plugin:  

    ``` bash
    <project_home>/src/test/java/ut/com/atlassian/plugins/tutorial/rest 
    ```

2.  Open `MyRestResourceTest.java` for editing.  
    The test checks whether the `getMessage()` method returns the "Hello World" message. But the method, as we've modified it, now expects a parameter. We'll hard-code one.  
3.  Add an input value to the `getMessage()` method invocation. Since our test still expects our original "Hello World" message in the response, add that. As modified, the relevant line of code should look like this:   

    ``` java
     Response response = resource.getMessage("Hello World");
    ```

      

## Step 7. Try it again, this time testing with the REST API Browser

Let's try the plugin again but this time let's use the REST API Browser (RAB), a page for browsing and testing REST APIs built into the RefApp (and every other Atlassian application). Developers who want to use your REST service would use the browser to discover and test the REST interface.  

1.  Start the RefApp again: 

    ``` bash
    atlas-run
    ```

2.  In a web browser, open the RefApp application:  
    `http://<host>:5990/refapp/`
3.  Log in with the default username and password, admin/admin.
4.  Click on the username link at the top right, **A.D.Ministrator**.
5.  Click on **REST API Browser**. This link appears in the left side menu under **RESTAPI DEV**.  
    The browser shows one of the services exposed by the application, along with the resources in that service. 
6.  Uncheck **Show only public APIs** and search using the term **message**.
7.  Choose **Message** from the list of services. This is the plugin service we created.  
    The REST browser shows two resources for our service: /message and /message/{key}. The second is the path parameter resource, and the first takes a parameter as a query parameter.
8.  Enter a key value for either of the resources and click **Execute**. The key value can be any string you like, such as "greeting".  
    The results appear below the resource.  
    <img src="/server/framework/atlassian-sdk/images/screen-shot-2016-12-14-at-11.29.02-am.png" height="400" />  
      

9.  Experiment by trying the other resource as well. Notice that if you click execute without a parameter, you'll get our default response, "Hello World."

    {{% tip %}}

For information on adding documentation for your resources and parameters (which REST browsers such as this one can display), see [Documenting your APIs with the Atlassian REST API Browser](/server/framework/atlassian-sdk/documenting-your-apis-with-the-atlassian-rest-api-browser).

    {{% /tip %}}

As a further exercise, try installing the plugin to another Atlassian application, such as JIRA. Start up JIRA in another terminal using the `atlas-run-standalone` command, and use the <a href="https://confluence.atlassian.com/display/UPM/Installing+Add-ons#InstallingAdd-ons-Installingbyfileupload" class="external-link">UPM to install</a> the JAR file directly from the `<project_home>/target` directory. Just as you did with the RefApp, you can open the REST API Browser from the Administration Console of the application and test the Message service.

## Next steps

Congratulations! You've created and parameterized a REST resource exposed by your Atlassian plugin. To continue learning about REST in Atlassian plugins, see the application-specific documentation on building REST services, including:

-   [JIRA REST API Tutorials](https://developer.atlassian.com/display/JIRADEV/JIRA+REST+API+Tutorials)
-   [Confluence REST APIs](https://developer.atlassian.com/display/CONFDEV/Confluence+REST+APIs+-+Prototype+Only)
-   [Remote API Reference](https://developer.atlassian.com/display/CROWDDEV/Remote+API+Reference)
-   [Stash REST API Overview](https://developer.atlassian.com/stash/docs/latest/reference/rest-api.html)

For general information on using REST for Atlassian plugin development, see:

-   [About the Atlassian RefApp](/server/framework/atlassian-sdk/about-the-atlassian-refapp)
-   [Atlassian REST API Design Guidelines version 1](/server/framework/atlassian-sdk/atlassian-rest-api-design-guidelines-version-1)
-   [REST Plugin Module](/server/framework/atlassian-sdk/rest-plugin-module)

































































































































































































