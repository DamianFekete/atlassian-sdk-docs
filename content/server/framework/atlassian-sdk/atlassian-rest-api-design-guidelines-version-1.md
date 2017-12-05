---
aliases:
- /server/framework/atlassian-sdk/atlassian-rest-api-design-guidelines-version-1-4915226.html
- /server/framework/atlassian-sdk/atlassian-rest-api-design-guidelines-version-1-4915226.md
category: devguide
confluence_id: 4915226
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915226
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915226
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: Atlassian REST API Design Guidelines Version 1 4915226
---
# Atlassian REST API design guidelines version 1

This document provides guidelines to Atlassian developers who are designing REST APIs for Atlassian applications. We are publishing these design principles and guidelines for viewing by the wider community for these reasons:

-   If you are a developer/administrator who wants to interact with the REST API in one or more of the Atlassian applications, it will help you to know the principles behind our REST API design.
-   If you are developing a plugin that exposes a REST API, you can follow these guidelines to ensure consistency between your plugin and the host application's APIs.
-   We invite and welcome feedback on these design principles.

{{% note %}}

REST API Principle Policy

These design guidelines focus on the implementation details for REST modules. Any implementations must also follow the [Atlassian REST API policy](https://developer.atlassian.com/display/HOME/Atlassian+REST+API+policy) which define the principles behind Atlassian's REST APIs.

{{% /note %}}

 

## Background to Atlassian REST APIs

Atlassian is currently working towards creating standardised REST APIs across all of our applications. Some of our applications already provide REST APIs, and some applications are providing new REST APIs or updating their existing APIs in an upcoming release. (Date of writing this paragraph: April 2009.)

Each application (Confluence, JIRA, Crowd, etc) will provide its own REST APIs, exposing the application-specific functionality. The goal is for these application-specific APIs to share common design standards, as described on this page.

For details of each application's APIs, please refer to the development hub in the documentation for the application concerned.

## Goal of these Guidelines

These guidelines are for Atlassian developers who are designing REST APIs for Atlassian applications. The goal is to keep REST API implementations as consistent as possible. These guidelines apply to all REST APIs, including:

-   REST APIs that use Atlassian's Jersey-based [REST plugin module type](https://developer.atlassian.com/display/REST/REST+Plugin+Module).
-   Other REST APIs not based on the plugin.

## Using these Guidelines

###### Following or Moving Away from the Guidelines

These guidelines provide one way of doing things that might not always be the only way nor the best way. If you think that is the case, feel free to *move away from* the guidelines. You should be aware of potential repercussions such as security issues, consistency issues, etc.

{{% note %}}

We strongly recommend that someone who is familiar with these guidelines should review your REST API code.

{{% /note %}}

 

###### Examples used in the Guidelines

The examples used in these guidelines assume that we have a REST API supplied by an Atlassian plugin called the 'Unified Plugin Manager' plugin, 'UPM' or 'upm'. (This is a real plugin that is currently under development.) The UPM allows you to discover and manage the plugins installed on an Atlassian application.

## REST Resources

### URIs for Resources

#### URI Structure

Given a list of `foo` entities, the following URI scheme provides access to the list of `foo` entities and to a particular `foo`:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>URI</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>/foo</code></p></td>
<td><p>This returns a list of the <code>foo</code> items. By default items in the list are a minimal representation of a <code>foo</code> entity. Note that we use the <strong>singular</strong> for the directory name.</p>
<p><strong>Method:</strong> GET.</p></td>
</tr>
<tr class="even">
<td><p><code>/foo/{key</code>}</p></td>
<td><p>This returns the full content of the <code>foo</code> identified by the given <code>key</code>.</p>
<p><strong>Method:</strong> GET.</p></td>
</tr>
</tbody>
</table>

Sub-elements of a `foo` entity are made available as sub-resources of `/foo/{key`}.

###### Examples

For our example, let's take a plugin resource within the 'upm' REST API.

Use this URI to access a list of plugins:

``` xml
http://host:port/context/rest/upm/1/plugin
```

Use this URI to access the plugin resource with a key of `a-plugin-key`:

``` xml
http://host:port/context/rest/upm/1/plugin/a-plugin-key
```

Structure of the above URI:

-   `host` and `port` define the host and port where the application lives.
-   `context` is the servlet context of the application. For example, for Confluence this would typically be `confluence`.
-   `rest` denotes the REST API.
-   `upm` is the path declared in the REST module type in the plugin descriptor.
-   `1` is the API version. See the section on API version control [below](#below).

#### Standard Query Parameters in URIs

Below is a list of standard query parameters. These names are reserved in our REST APIs and should be used according to the notes in the table below.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Query Parameter</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>expand</code></p></td>
<td><p>Used for title expansion. See section on title expansion <a href="#below">below</a>.</p></td>
</tr>
<tr class="even">
<td><p><code>start-index</code></p></td>
<td><p>An integer specifying the starting point when paging through a list of entities. Defaults to 0.</p></td>
</tr>
<tr class="odd">
<td><p><code>max-results</code></p></td>
<td><p>The maximum number of results when paging through a list of entities. No default is provided. We recommend that APIs should define their own default. Applications should also define a hard limit on the number of items that can be requested at the same time.</p></td>
</tr>
</tbody>
</table>

### Entities

#### Representations (Content Types) of Entities

By default, REST APIs must support multiple content types.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Representation</p></th>
<th><p>Requested via...</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>JSON</p></td>
<td><p>Requested via one of the following:</p>
<ul>
<li><code>application/json</code> in the HTTP Accept header</li>
<li><code>.json</code> extension</li>
</ul></td>
</tr>
<tr class="even">
<td><p>XML</p></td>
<td><p>Requested via one of the following:</p>
<ul>
<li><code>application/xml</code> in the HTTP Accept header</li>
<li><code>.xml</code> extension</li>
</ul></td>
</tr>
</tbody>
</table>

#### Hypertext Linking within an Entity

Entities can have links to each other. This is represented by the `<link>` tag. The `<link>` tag supports the following attributes:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Attribute</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>href</code></p></td>
<td><p>The URI of the entity linked to.</p></td>
</tr>
<tr class="even">
<td><p><code>rel</code></p></td>
<td><p>The relationship between the <em>containing</em> entity and the entity linked to.<br />
Examples of possible values:</p>
<ul>
<li><code>self</code> -- denotes that the URI points to the entity itself, see Entity ID <a href="#below">below</a>.</li>
<li><code>edit</code> -- denotes the URI used to update the entity,</li>
<li><code>delete</code> -- denotes the URI used to delete the entity,</li>
<li><code>add</code> -- denotes the URI used to create the entity.</li>
</ul></td>
</tr>
<tr class="odd">
<td><p><code>title</code></p></td>
<td><p>Optional. A short description of the entity linked to.</p></td>
</tr>
</tbody>
</table>

Links to the URI that will perform operations on an entity have their `rel` attribute set to `edit`, `delete` or `add`. We recommend that entities provide these links as part of their content.

Links should follow some simple rules:

-   Links use the same base URL independently of server-side implementation. So, if the REST API is available at `http://host:port/context/rest/api/`, then links to other resources should use this as their base URL.
-   Whenever the user specifies an extension, such as `.xml`, `.json`, etc, links should have this same extension as far as possible.
-   Links do not have query parameters.

###### Example

The following plugin entity has a `<link>` tag with a `rel` attribute identifying the entity's own ID via a URI pointing to itself:

``` xml
<plugin key="a-plugin-key" enabled="true" expand="modules,info">
  <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key" />
  <info name="A plugin"/>
  <modules size="2" expand="module"/>
</plugin>
```

#### Entity ID

Every addressable entity should have a `<link>` tag with the attribute `rel="self"` pointing to its own URI. See the section on linking [above](#above).

#### Version Control for Entities

Entities SHOULD be served with an <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.19" class="external-link">ETag header</a>.

*Read-only* entities and lists of entities may be served without an ETag header. Providing an ETag header for these resources will help with caches and conditional requests, but the header need not be included if calculating the ETag is too expensive or difficult.

The ETag for a resource MUST be the same regardless of the requested representation or title expansion state.

The server MUST treat <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.24" class="external-link">If-Match</a> and <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.26" class="external-link">If-None-Match</a> headers provided by clients as defined in <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html" class="external-link">RFC 2616</a>.

`PUT` or `DELETE` API requests SHOULD provide an <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.24" class="external-link">If-Match</a> header, and SHOULD react meaningfully to 412 (Precondition Failed) responses.

#### Collections of Entities

Collections of entities should define the following attributes:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Attribute</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>size</code></p></td>
<td><p>The total size of items available in the collection. This can be different from the actual number of items currently listed in the collection if the <code>start-index</code> and <code>max-result</code> query parameters have been used.</p></td>
</tr>
<tr class="even">
<td><p><code>start-index</code></p></td>
<td><p>If used to <em>filter</em> the collection elements.</p></td>
</tr>
<tr class="odd">
<td><p><code>max-result</code></p></td>
<td><p>If used to <em>filter</em> the collection elements.</p></td>
</tr>
</tbody>
</table>

###### Example

In the response below, the `<modules>` entity has a `size` attribute indicating that there are 2 plugin modules in the collection:

``` xml
<plugin key="a-plugin-key" enabled="true" expand="modules,info">
  <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key" />
  <info name="A plugin"/>
  <modules size="2" expand="module"/>
</plugin>
```

#### Title Expansion for Entities

In order to be minimise network traffic and simplify some APIs from the client perspective, we recommend that APIs provide title expansion. This works by using the `expand` query parameter and setting its value to the last path element of the entity's schema.

The `expand` query parameter allows a comma-separated list of identifiers to expand. For example, the value `modules,info` requests the expansion of entities for which the `expand` identifier is `modules` and `info`.

You can use the dot notation to specify expansion of entities within another entity. For example `modules.module` would expand the plugin entity (because its `expand` identifier is `modules`) and the module entities within the plugin. See example 4 [below](#below).

Expandable entities should be declared by parent entities in the form of an `expand` attribute. In example 1, the plugin entity declares `modules` and `info` as being expandable. The attribute should not be confused with the query parameter which specifies which entities *are* expanded.

###### Example 1. Accessing a Resource without Title Expansion

For our example, let's take a plugin resource within the 'upm' REST API.

Use this URI to access the plugin resource without specifying title expansion:  
<a href="http://hostport" class="external-link">http://host:port/context/rest/upm/1/plugin/a-plugin-key</a>

The response will contain:

``` xml
<plugin key="a-plugin-key" enabled="true" expand="modules,info">
  <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key" />
  <info name="A plugin"/>
  <modules size="2" expand="module"/>
</plugin>
```

###### Example 2. Expanding the `info` Element

Use the following URI to expand the `info` element in our plugin resource:  
<a href="http://hostport" class="external-link">http://host:port/context/rest/upm/1/plugin/a-plugin-key?expand=info</a>.

Now the response will contain:

``` xml
<plugin key="a-plugin-key" enabled="true" expand="modules,info">
  <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key" />
  <info name="A plugin">
    <description>This is an awesome plugin</description>
    <version>1.1</version>
  </info>
  <modules size="2" expand="module"/>
</plugin>
```

###### Example 3. Expanding the Collection of Modules

Use this URI to expand the module collection in our plugin resource:  
<a href="http://hostport" class="external-link">http://host:port/context/rest/upm/1/plugin/a-plugin-key?expand=modules</a>

The response will contain:

``` xml
<plugin key="a-plugin-key" enabled="true" expand="modules,info">
  <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key" />
  <info name="A plugin"/>
  <modules size="2" expand="module">
    <module key="module-key-1">
      <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key/module/module-key-1" />
    </module>
    <module key="module-key-2">
      <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key/module/module-key-2" />
    </module>
  </modules>
</plugin>
```

Note that the above URI does not expand each individual module.

###### Example 4: Using the Dot Notation to Expand Entities within another Entity

Use the following URI to expand the modules inside the collection within our plugin resource:  
<a href="http://hostport" class="external-link">http://host:port/context/rest/upm/1/plugin/a-plugin-key?expand=modules.module</a>

The response will contain:

``` xml
<plugin key="a-plugin-key" enabled="true" expand="modules,info">
  <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key" />
  <info name="A plugin"/>
  <modules size="2" expand="module">
    <module key="module-key-1">
      <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key/module/module-key-1" />
      <name>Module 1</name>
      <description>This is my first module</description>
    </module>
    <module key="module-key-2">
      <link rel="self" href="http://host:port/context/rest/upm/1/plugin/a-plugin-key/module/module-key-2" />
      <name>Module 2</name>
      <description>This is my second module</description>
    </module>
  </modules>
</plugin>
```

###### Using Index Values to Expand a Collection

You can also set indices to expand a given set of items in the collection. The index is 0 based:

-   `modules[3]` will expand only the module at index 3 of the collection.
-   `modules[1:3]` will expand modules ranging from index 1 to 3 (included). Note that `[:3]` and `[3:]` notations also work and the range goes respectively from the beginning of the collection and to the end of the collection.
-   `modules[-1]` will expand the last module. Other negative index values also work and indices are counted from the end of the collection.

## Version Control for APIs

APIs must be subject to version control. The version number of an API appears in its URI. For example, use this URI structure to request version 1 of the 'upm' API:

``` xml
http://host:port/context/rest/upm/1/...
```

When an API has multiple versions, we recommend:

-   Two versions should be supported at the same time.
-   If two or more versions are available, applications may provide a shortcut to the latest version using the `latest` key-word.

For example, if versions 1 and 2 of the 'upm' API are available, the following two URIs would point to the same resources:

-   <a href="http://hostport" class="external-link">http://host:port/context/rest/upm/latest/</a>

-   <a href="http://hostport" class="external-link">http://host:port/context/rest/upm/2/</a>

### When to Change the Version

A version number indicates a certain level of backwards-compatibility the client can expect, and as such, extra care should be taken to maintain this trust. The following lists which types of changes necessitate a new version and which don't:

#### Changes That Don't Require a New Version

-   New resources
-   New HTTP methods on existing resources
-   New data formats
-   New attributes or elements on existing data types

#### Change That Require a New Version

-   Removed or renamed URIs
-   Different data returned for same URI
-   Removal of support for HTTP methods on existing URIs

## Security

### Authentication

Every REST API MUST at least accept <a href="http://www.ietf.org/rfc/rfc2617.txt" class="external-link">basic authentication</a>.

Other authentication options are optional, such as [Trusted Apps](/server/framework/atlassian-sdk/trusted-application-authentication), OS username and password as query parameters, or 'remember me' cookies.

By default, access to all resources (using any method) requires the client to be authenticated. Resources that should be available anonymously MUST be marked as such. The default implementation SHOULD use the `AnonymousAllowed` annotation.

### Authorisation

Authorisation is NOT handled by the REST APIs themselves. It is the responsibility of the service layer to make sure the authenticated client (user) has the correct permissions to access the given resource.

### Cross-site request forgery 

Atlassian uses the XSRF acronym for <a href="https://en.wikipedia.org/wiki/Cross-site_request_forgery" class="external-link">Cross-site request forgery</a> and not CSRF.

To protect against <a href="https://en.wikipedia.org/wiki/Cross-site_request_forgery" class="external-link">XSRF</a> attacks:

1.  Ensure that GET requests are idempotent
2.  For rest api classes or methods that **will** **not** be used in normal browser 'form' posts
    1.  annotate them with **@Consumes({MediaType.APPLICATION\_XML, MediaType.APPLICATION\_JSON})**

        ``` java
        Class example:
        @Path("/a")
        @Consumes({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
        public class RestHelloWorldService { ... }

         
        Method example:
        public class RestAnotherService { 
        ...
            @Consumes({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
            @POST
            @Path("/b")
            public Response getUncompletedUsers() { ... }
        }
        ```

        This protects against xsrf as browser cross-domain simple requests cannot have a content type of MediaType.APPLICATION\_XML or MediaType.APPLICATION\_JSON. See <a href="http://www.w3.org/TR/cors/#terminology" class="uri external-link">http://www.w3.org/TR/cors/#terminology</a> for further information on "simple requests". It is also noting that because of issues in the implementation of the <a href="https://w3c.github.io/beacon/" class="external-link">beacon API</a> in Chrome, atlassian-rest performs <a href="https://confluence.atlassian.com/display/KB/Cross+Site+Request+Forgery%28CSRF%29+protection+changes+in+Atlassian+Rest" class="external-link">origin xsrf checks</a> on requests in some cases to prevent content-types that should not be allowed to be sent cross-domain without <a href="https://github.com/w3c/beacon/pull/23" class="external-link">CORS permitting them</a>.

    2.  For atlassian-rest versions prior to 3.0.0  
        1.  annotate them with @[com.atlassian.plugins.rest.common.security.RequiresXsrfCheck](https://developer.atlassian.com/static/javadoc/rest/2.5/reference/com/atlassian/plugins/rest/common/security/RequiresXsrfCheck.html). The atlassian-rest-refimpl-plugin has an <a href="https://bitbucket.org/atlassian/atlassian-rest/src/6130a9bc1766379e9a7dee1c96d78b9e45f627f8/atlassian-rest-refimpl-plugin/src/main/java/com/atlassian/plugins/rest/xsrf/XsrfCheck.java?at=master" class="external-link">example of using this annotation</a>.  
    3.  In atlassian-rest version 3.0.0 and later mutative resources such as `POST` are automatically XSRF protected.

3.  For rest api classes or methods that **will** be used from normal browser 'form' posts
    1.  As of atlassian-rest 2.8.0-m9 the [com.atlassian.plugins.rest.common.security.RequiresXsrfCheck](https://developer.atlassian.com/static/javadoc/rest/2.5/reference/com/atlassian/plugins/rest/common/security/RequiresXsrfCheck.html)  annotation can be used to perform xsrf token validation on rest form submissions. This xsrf token   
        validation implementation uses the [SAL](https://developer.atlassian.com/display/DOCS/Shared+Access+Layer) provided [XsrfTokenValidator](https://developer.atlassian.com/static/javadoc/sal/2.6/reference/com/atlassian/sal/api/xsrf/XsrfTokenValidator.html) and  [XsrfTokenAccessor](https://developer.atlassian.com/static/javadoc/sal/2.6/reference/com/atlassian/sal/api/xsrf/XsrfTokenAccessor.html) interfaces. A plugin which uses this annotation to provide xsrf token validation on a rest method will need to ensure that in all corresponding forms there is a hidden xsrf token parameter with a xsrf token value obtained from the [XsrfTokenAccessor](https://developer.atlassian.com/static/javadoc/sal/2.6/reference/com/atlassian/sal/api/xsrf/XsrfTokenAccessor.html) interface. For example, the exampleXsrfTokenProtectedMethod method annotated with the [RequiresXsrfCheck](https://developer.atlassian.com/static/javadoc/rest/2.5/reference/com/atlassian/plugins/rest/common/security/RequiresXsrfCheck.html) annotation in the following class

        ``` java
        @Path("/exampleXsrfTokenProtectedMethod")
        @Consumes({MediaType.TEXT_PLAIN})
        public class RestHelloWorldService {
         
         @POST
         @com.atlassian.plugins.rest.common.security.RequiresXsrfCheck 
         public Response exampleXsrfTokenProtectedMethod( args... ) { ... }
         
        }
        ```

        would have a corresponding form similar to the following

        ``` xml
        <form name="do-something" action="/rest/examplePlugin/latest/exampleXsrfTokenProtectedMethod" method="post" enctype="text/plain">
                 <input type="hidden" name="atl_token" value="xsrfTokenValueHere">
                 <input type="text" name="something">
        </form>
        ```

#### Migrating to Atlassian Rest 3.0.0

In version 3.0.0 and later of atlassian-rest XSRF protection is enabled by default. It is possible to opt-out of XSRF protection for a rest method by using the com.atlassian.annotations.security.XsrfProtectionExcluded annotation as provided by Atlassian annotations (versions &gt;= 0.12). Please avoid using the XsrfProtectionExcluded annotation as much as possible. For completeness, here is an example of using the XsrfProtectionExcluded annotation.

``` java
package com.random.plugin.code.rest;

import com.atlassian.annotations.security.XsrfProtectionExcluded;

import javax.ws.rs.Path;
import javax.ws.rs.POST;

/**
 */
@Path ("/thing")
public class XsrfCheck
{
    @Path("post")
    @POST
    @XsrfProtectionExcluded // does not mutate state.
    public String nonMutativePost()
    {
        return "Request succeeded";
    }

}
```

 

The following diagram shows when XSRF protection is enforced on a request to a rest resource in atlassian-rest 3.0.0 and later versions. 

<img src="/server/framework/atlassian-sdk/images/39373982.png" class="gliffy-macro-image" />

Also in atlassian-rest 3.0.0 a value of "nocheck" for the X-Atlassian-Token XSRF header has been deprecated and will result in a warning when used appearing in the logs. Since, rest 2.9.1 a value of **"no-check"**, is accepted in addition to the old "nocheck" rest value for the X-Atlassian-Token header ( <a href="https://ecosystem.atlassian.net/browse/REST-263?src=confmacro" class="jira-issue-key"><img src="https://ecosystem.atlassian.net/secure/viewavatar?size=xsmall&amp;avatarId=15303&amp;avatarType=issuetype" class="icon" />REST-263</a> - REST-164 Implemented checking the X-Atlassian-Token header with the wrong value Resolved ).

 

#### Using the jQuery ajaxSetup or ajaxPrefilter function to add the XSRF header to jQuery ajax requests

 

By using jQuery's <a href="https://api.jquery.com/jquery.ajaxsetup/" class="external-link">ajaxSetup</a> or the <a href="https://api.jquery.com/jquery.ajaxprefilter/" class="external-link">ajaxPrefilter</a>  function it is possible to make all <a href="https://developer.mozilla.org/en-US/docs/Web/JavaScript/Same_origin_policy_for_JavaScript" class="external-link">same origin </a>jQuery ajax requests contain the CSRF X-Atlassian-Token header. This is incredibly useful as it means that existing jQuery ajax usages should not need to be modified.

 

For example bamboo uses the ajaxPrefilter function like so:

``` javascript
AJS.$.ajaxPrefilter(
        function(options, originalOptions, jqXHR) {
            function isMutativeHttpMethod(method) {
                return !(/^(GET|HEAD|OPTIONS|TRACE)$/.test(method));
            }
            if (isMutativeHttpMethod(options.type)) {
                options.crossDomain = false;
                jqXHR.setRequestHeader("X-Atlassian-Token", "no-check");
            }
        });

```

 

Here is an example using <span class="underline">ajaxSetup</span> instead of ajaxPrefilter:

``` javascript
function isMutativeHttpMethod(method) {
        return !(/^(GET|HEAD|OPTIONS|TRACE)$/.test(method));
    }
 
$.ajaxSetup({
    crossDomain: false,
    beforeSend: function(xhr, settings) {
        if (isMutativeHttpMethod(settings.type)) {
            xhr.setRequestHeader("X-Atlassian-Token", "no-check");
        }
    }
});
```

 

##### CORS

If <a href="https://en.wikipedia.org/wiki/Cross-origin_resource_sharing" class="external-link">CORS</a> is configured in a product such that it permits setting the content-type or the X-Atlassian-Token header then XSRF protection can be bypassed by CORS allowed origins. This is intentional and supported by design.

## Caching

REST APIs SHOULD support conditional GET requests. This will allow the client to cache resource representations. For conditional GET requests to work, the client MUST send the <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.19" class="external-link">ETag</a> value when requesting resources using the <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.26" class="external-link">If-None-Match</a> request header. The ETag is the one provided by a previous request to that same URI. See the section on version control for entities [below](#below).

Server implementations should acknowledge the `If-None-Match` header and check whether the response should be a `304` (Not Modified). See the section on response codes [below](#below).

## Concurrency

PUT or DELETE API requests SHOULD provide an <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec14.html#sec14.24" class="external-link">If-Match</a> header, and SHOULD react meaningfully to `412` (Precondition Failed) responses. See the section on response codes [below](#below).

The ETag is the one provided by a previous GET request to that same URI. See the section on version control for entities [below](#below).

## Not Yet Covered in these Guidelines

Some items worth discussing in the guidelines are currently out of scope:

-   Common entities
-   Batching
-   Gzip
-   OpenSearch
-   Internationalisation (i18n)

## Appendix A: Response Codes

This list shows the common HTTP response codes and some brief guidelines on how to use them. For the complete list of HTTP response codes, please refer to <a href="http://www.w3.org/Protocols/rfc2616/rfc2616-sec6.html#sec6.1.1" class="external-link">section 6 of RFC 2616</a>.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Code</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>200</p></td>
<td><p>Request was processed as expected.</p>
<p><strong>Name:</strong> OK.</p>
<p><strong>Notes:</strong></p>
<ul>
<li>GET request returns a representation of the requested entity,</li>
<li>The body of other requests will be a Status entity as described in the Status section of this document <a href="#below">below</a>.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>201</p></td>
<td><p>Request created an entity.</p>
<p><strong>Name:</strong> Created.</p>
<p><strong>Notes:</strong></p>
<div>
<ul>
<li>This cannot happen on GET or DELETE requests.</li>
<li>This will happen on POST and may happen on PUT requests.</li>
<li>The response should set the <code>Location</code> header to the URI for the created resource.</li>
<li>The body of the response is a Status entity as described in the Status section of this document <a href="#below">below</a>.</li>
</ul>
</div></td>
</tr>
<tr class="odd">
<td><p>202</p></td>
<td><p>The request has been acknowledged but cannot be processed <em>in real time</em>.<br />
For example, the request may have scheduled a job on the server.</p>
<p><strong>Name:</strong> Accepted.</p>
<p><strong>Notes:</strong></p>
<ul>
<li>The response should set the <code>Location</code> header with the URI to the resource representing the pending action.</li>
<li>The body of the response is a Status entity as described in the Status section of this document <a href="#below">below</a>.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>204</p></td>
<td><p><strong>Name:</strong> No content.</p></td>
</tr>
<tr class="odd">
<td><p>301</p></td>
<td><p>The requested resource has been moved to another location (URI).</p>
<p><strong>Name:</strong> Moved Permanently.</p>
<p><strong>Notes:</strong></p>
<div>
<ul>
<li>The response should set the <code>Location</code> header to the URI of the new location of the resource.</li>
<li>The body of the response is a Status entity as described in the Status_ section of this document <a href="#below">below</a>.</li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>304</p></td>
<td><p>The requested resource has not been modified.<br />
The client's <em>cached</em> representation is still valid.</p>
<p><strong>Name:</strong> Not Modified.</p>
<p><strong>Notes:</strong></p>
<ul>
<li>No body is allowed for these responses.</li>
</ul></td>
</tr>
<tr class="odd">
<td><p>401</p></td>
<td><p>Client is not authenticated or does not have sufficient permission to perform this request.</p>
<p><strong>Name:</strong> Unauthorized.</p>
<p><strong>Notes:</strong></p>
<div>
<ul>
<li>The body of the response is a Status entity as described in the Status section of this document <a href="#below">below</a>.</li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>404</p></td>
<td><p>No resource was found at this location (URI).</p>
<p><strong>Name:</strong> Not found.</p>
<p><strong>Notes:</strong></p>
<div>
<ul>
<li>The body of the response is a Status entity as described in the Status section of this document <a href="#below">below</a>.</li>
</ul>
</div></td>
</tr>
<tr class="odd">
<td><p>412</p></td>
<td><p>The client specified some preconditions that are not valid.</p>
<p><strong>Name:</strong> Precondition Failed.</p>
<p><strong>Notes:</strong></p>
<div>
<ul>
<li>The body of the response is a Status entity as described in the Status section of this document <a href="#below">below</a>.</li>
</ul>
</div></td>
</tr>
<tr class="even">
<td><p>5xx</p></td>
<td><p>Any server-side error.</p>
<p><strong>Name:</strong> Server-Side Error.</p>
<p><strong>Notes:</strong></p>
<div>
<ul>
<li>These codes should not be set programmatically and are reserved for unexpected errors.</li>
</ul>
</div></td>
</tr>
</tbody>
</table>

## Appendix B: Basic Data Types

### Link

The link element is used for hyperlinking entities and as entity IDs:

``` xml
<link title="This is my resource" rel="edit" href="http://host:port/context/rest/api/1/myresource" />
```

See the sections on [linking](#above) and [entity IDs](#below) above.

### Status

Any request which produces a status code with no body will have a body formatted like this:

``` xml
<status>
  <plugin key="a-plugin-key" version="1.0" />
  <status-code>201</status-code>
  <sub-code>604</sub-code>
  <message>Some human readable message</message>
  <etag>233223</etag>
  <resources-created>
    <link rel="self" href="http:..." />
  </resources-created>
  <resources-updated />
</status>
```

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Element</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>plugin</code></p></td>
<td><p>Describes the plugin which provides the REST API. This element is present only if the REST API is provided by a plugin.</p></td>
</tr>
<tr class="even">
<td><p><code>status-code</code></p></td>
<td><p>The actual HTTP code of the response. See the section on response codes <a href="#below">above</a>.</p></td>
</tr>
<tr class="odd">
<td><p><code>sub-code</code></p></td>
<td><p>Another code that defines the error more specifically. It is up to REST API developers to define their various codes.</p></td>
</tr>
<tr class="even">
<td><p><code>resources-created</code></p></td>
<td><p>This element is present when resources have been created. It consists of <code>link</code> elements to the created resources.</p></td>
</tr>
<tr class="odd">
<td><p><code>resources-updated</code></p></td>
<td><p>This element is present when resources have been updated. It consists of <code>link</code> elements to the updated resources.</p></td>
</tr>
</tbody>
</table>

###### RELATED TOPICS

[Developing a REST Service Plugin](/server/framework/atlassian-sdk/developing-a-rest-service-plugin)  
[REST Plugin Module](https://developer.atlassian.com/display/REST/REST+Plugin+Module)  
[Basics of Exposing REST APIs via Plugins](/server/framework/atlassian-sdk/basics-of-exposing-rest-apis-via-plugins-4915229.html)


































































































































































































