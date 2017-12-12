---
aliases:
- /server/framework/atlassian-sdk/rest-plugin-module-4915219.html
- /server/framework/atlassian-sdk/rest-plugin-module-4915219.md
category: reference
confluence_id: 4915219
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915219
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915219
date: '2017-12-08'
legacy_title: REST Plugin Module
platform: server
product: atlassian-sdk
subcategory: modules
title: REST plugin module
---
# REST plugin module

This page describes how to use the REST plugin module to expose a REST API from a plugin.

 

{{% note %}}

Plugin Framework 2 Only

The REST plugin module described below is available only for OSGi-based plugins using version 2.2 or later of the [Atlassian Plugin Framework](https://developer.atlassian.com/display/PLUGINFRAMEWORK).

{{% /note %}}

 

## Purpose of the REST Plugin Module

You can use the REST plugin module to expose services and data entities as REST APIs. The Atlassian REST plugin module is bundled with our applications.

REST APIs provide access to resources via URI paths. To use a REST API, your plugin or script will make an HTTP request and parse the response. You can choose JSON or XML for the response format. Your methods will be the standard HTTP methods like GET, PUT, POST and DELETE. Because the REST API is based on open standards, you can use any web development language to access the API.

## Mapping the URL to a Resource

A REST resource is exposed at a URL such as this:

``` xml
http://myhost.com:port/myapp/rest/api-name/api-version/resource-name
```

Here's how the parts of the URL are composed and used:

1.  `http://myhost.com:port` - The operating system directs the request to the application server (e.g. Tomcat) that handles the specified port.
2.  `/myapp` - Tomcat directs the request to the application myapp.
3.  `/rest` - The application's <a href="http://wiki.metawerx.net/wiki/Web.xml" class="external-link">web.xml</a> deployment descriptor file maps the URLs to the relevant servlets. So in this case, it maps /rest to our REST servlet, which points to our [REST plugin module type](https://developer.atlassian.com/display/REST/REST+Plugin+Module).
4.  `/api-name/api-version` - Now the REST plugin module takes over. The relevant part of the URL (`api-name` and `api-version`) are defined as the `path` and `version` in the `atlassian-plugin.xml` file. For example:

    ``` xml
    <rest key="helloWorldRest" path="/helloworld" version="1.0">
        <description>Provides hello world services.</description>
    </rest>
    ```

5.  `/resource-name` - The final part of the URL mapping (`resource-name` and sub-elements) is done via annotations on the class, used to declare the URI path, the HTTP method and the media type. <a href="https://jersey.github.io/" class="external-link">Jersey</a> (based on <a href="https://jsr311.java.net/" class="external-link">JAX-RS</a>) reads the `@Provider` and `@Path` annotations and maps them to classes and methods, so that we know which method is called for each REST resource and method. See the <a href="https://jersey.java.net/documentation/latest/getting-started.html" class="external-link">Jersey documentation</a>.

## About JAXB Annotations

<a href="http://www.oracle.com/technetwork/articles/javase/index-140168.html" class="external-link">JAXB</a> converts the Java classes to XML or JSON and vice versa, making use of <a href="https://docs.oracle.com/javase/tutorial/jaxb/intro/" class="external-link">JAXB annotations</a>. (Available in Java 1.5 and later.)

For example a Java `User` object with JAXB annotations may look something like this:

``` xml
import javax.xml.bind.annotation.*;

@XmlRootElement
public class User
{
    @XmlElement
    private String firstName;

    @XmlElement
    private String lastName;

    // This private constructor isn't used by any code, but JAXB requires any
    // representation class to have a no-args constructor.
    private User() { }

    public User(String firstName, String lastName)
    {
        this.firstName = firstName;
        this.lastName = lastName;
    }

    ...
}
```

The XML response content for user John Smith would be:

``` xml
<user>
    <firstName>John</firstName>
    <lastName>Smith</lastName>
</user>
```

By default, on conversion the XML element name will be the same as the object name. Alternatively, you can add the XML element name to the annotation. Something like this: `@XmlRootElement(name="principal")`. There are specific annotations for arrays, etc. See <a href="https://docs.oracle.com/javase/tutorial/jaxb/intro/" class="external-link">JAXB's documentation</a> for more details on this.

{{% note %}}

We have no schema or DTD.

{{% /note %}}

 

Jersey also handles JSON based on the same JAXB objects as in the example above. The JSON for the example would be:

``` javascript
{
  "firstName":"John",
  "lastName":"Smith"
}
```

A trivial REST service class with a single URL returning an instance of `User` would look like this:

``` java
import javax.ws.rs.*;
import javax.ws.rs.core.*;

@Path("/")
@Consumes({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
@Produces({MediaType.APPLICATION_XML, MediaType.APPLICATION_JSON})
public class RestHelloWorldService {
    @GET
    @Path("users")
    public Response getUncompletedUsers() {
        return Response.ok(new User("Fred","Bloggs")).build();
    }
}
```

## Configure the Module in the Plugin Descriptor

The root element for the REST plugin module is `rest`. It allows the following attributes and child elements for configuration.

#### Attributes

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>key</p></td>
<td><p>The identifier of the plugin module, i.e. the identifier of the REST module. This key must be unique within the plugin where it is defined. Sometimes you will need to uniquely identify a module. Do this with the <strong>complete module key</strong>. A module with key <code>fred</code> in a plugin with key <code>com.example.modules</code> will have a complete key of <code>com.example.modules:fred</code>.</p>
<p><strong>Requred.</strong></p>
<p><strong>Default: N/A</strong></p></td>
</tr>
<tr class="even">
<td><p>path</p></td>
<td><p>The path to the REST API exposed by this module. For example, if set to <code>/foo</code>, the REST API will be available at <a href="http://localhost:8080/context/rest/foo/1.0" class="uri external-link">http://localhost:8080/context/rest/foo/1.0</a>, where 1.0 is the version of the REST API.</p>
<p><strong>Requred.</strong></p>
<p><strong>Default: N/A</strong></p></td>
</tr>
<tr class="odd">
<td><p>version</p></td>
<td><p>This is the version of the REST API. This is not the same thing as the plugin version. Different versions of the same API can be provided by different plugins. Version numbers follow the same pattern as OSGi versions, i.e. <code>major.minor.micro.qualifier</code> where <code>major</code>, <code>minor</code> and <code>micro</code> are integers. If version is <code>none</code>, then the REST API will not contain a version number in its URL.</p>
<p><strong>Requred.</strong></p>
<p><strong>Default: N/A</strong></p></td>
</tr>
</tbody>
</table>

#### Elements

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>description</p></td>
<td><p>The description of the plugin module, i.e. the description of the REST module. The 'key' attribute can be specified to declare a localisation key for the value instead of text in the element body.</p>
<p><strong>Default: N/A</strong></p></td>
</tr>
<tr class="even">
<td><p>package</p></td>
<td><p>The package from which to start scanning for resources and providers. Can be specified multiple times. Defaults to scanning the whole plugin. <strong>Since 2.0</strong></p>
<p><strong>Default: N/A</strong></p></td>
</tr>
<tr class="odd">
<td><p>dispatcher</p></td>
<td><p>Determines when the filter is triggered. You can include multiple <code>dispatcher</code> elements.<br />
If this element is present, its content must be one of the following: <code>REQUEST</code>, <code>INCLUDE</code>, <code>FORWARD</code>, <code>ERROR</code>.<br />
Note: This element is only available in <a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852001">Plugin Framework 2.5</a> and later. In earlier versions of the framework, the filter will be fired on all conditions.</p>
<p><strong>Default: Filter will be triggered on <code>REQUEST</code> only.</strong></p></td>
</tr>
</tbody>
</table>

## Example

Here is an example `atlassian-plugin.xml` file containing a single public component:

``` xml
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
    <plugin-info>
        <description>A basic REST module test</description>
        <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
        <version>1.0</version>
    </plugin-info>

    <rest key="helloWorldRest" path="/helloworld" version="1.0">
        <description>Provides hello world services.</description>
    </rest>
</atlassian-plugin>
```

## Notes on REST API and Plugin Development

#### JAX-RS and Jersey

Here is some information to be aware of when developing a REST plugin module:

-   The REST module is based on JAX-RS. Specifically, it uses <a href="https://jersey.github.io/" class="external-link">Jersey</a>, which is the JAX-RS reference implementation.
-   The REST module is based on **version 1.0.2 of Jersey**.
-   Jersey is configured to use all its default providers, but you should be able to change the configuration by adding your own providers in your plugin. For example, you may want to <a href="http://blogs.sun.com/enterprisetechtips/entry/configuring_json_for_restful_web" class="external-link">enhance your JSON</a>.

#### Including the REST Plugin Module into your Project

You can include the REST plugin module as a Maven dependency from our <a href="http://docs.atlassian.com/atlassian-rest/" class="external-link">Maven repository</a>.

#### Developing your REST API as an Atlassian Plugin

To develop a REST API and deploy it into an Atlassian application, you will follow the same process as for any other Jersey application:

1.  Develop your JAX-RS resources, using the annotations `@Path`, `@Provider`, etc.
2.  Bundle your resource classes in your plugin JAR file, along with the plugin descriptor `atlassian-plugin.xml`.
3.  Deploy your plugin to the application.

See [Set up the Atlassian Plugin SDK and Build a Project](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project) and [Configuring the Plugin Descriptor](/server/framework/atlassian-sdk/configuring-the-plugin-descriptor).

#### Accessing your REST Resources

Your REST resources will be available at this URL:

``` xml
http://host:port/context/rest/helloworld/1.0
```

-   `host` and `port` define the host and port where the application lives.
-   `context` is the servlet context of the application. For example, for Confluence this would typically be `confluence`.
-   `helloworld` is the path declared in the REST module type in the plugin descriptor.
-   `1.0` is the API version.

If `1.0` is the latest version of the *helloworld* API installed, this version will also be available at this URL:

``` xml
http://host:port/context/rest/helloworld/latest
```

#### How the REST Plugin Module Finds your Providers and Resources

The REST plugin module scans your plugin for classes annotated with the `@Provider` and `@Path` annotation. The `@Path` annotations can be simply declared on a method within a class and do not need to be present at the entity level. 

For those not familiar with the JAX-RS specification, the @Path annotation can be declared at a package, class, or method level.  Furthermore, their effects are cumulative.  For example, if you define this at the package level:

``` java
@Path("/admin")
package myPackage;
```

then this at the class level:

``` java
package myPackage;

@Path("/myGroup")
public class MyGroup {...};
```

then this at the method level:

``` java
@Path("/myResource")
public void getResource() {...};
```

The final URL would be for the helloWorld plugin above:

``` xml
http://host:port/context/rest/helloworld/1.0/admin/myGroup/myResource
```

Notes:

-   The REST plugin module will not scan a library bundled with your plugin, typically bundled in the `META-INF/lib` directory of the JAR. So make sure you put all providers and resources at the top level in your plugin JAR. 
-   Only one resource method can be bound to the root "/" path.

#### Easy Way to Request JSON or XML Response Format

When using JAX-RS (and Jersey), the standard way to specify the content type of the response is to use the HTTP Accept header. While this is a good solution, it's not always a convenient one.

The REST plugin module allows you to use an extension to the resource name in the URL when requesting JSON or XML.

For example, let's assume I want to request JSON data for the resource at this address:

``` xml
http://host:port/context/rest/helloworld/latest/myresource
```

I have two options:

-   **Option 1:** Use the HTTP Accept header set to `application/json`.
-   **Option 2:**Simply request the resource via this URL:

    ``` xml
    http://host:port/context/rest/helloworld/latest/myresource.json
    ```

If I want content of type `application/xml`, I will simply change the extension to `.xml`. Currently the REST plugin module supports only `application/json` and `application/xml`.

#### Working with JSON in Firefox

A handy tool: The <a href="http://brh.numbera.com/software/jsonview/" class="external-link">JSONView</a> add-on for Firefox allows you to view JSON documents in the browser, with syntax highlighting. Here is a link to the <a href="https://addons.mozilla.org/en-US/firefox/addon/10869" class="external-link">Firefox add-on page</a>.

#### Differences in JSON and XML rendering of REST responses

By default, JSON responses include **any** object fields which are explicitly annotated with a JAXB annotation, while XML responses include public fields and fields with public getters.

To get the same behaviour for JSON you need to either annotate each field with `@XmlElement` or `@XmlAttribute`, or annotate the class or package with `@XmlAccessorType(XmlAccessType.PUBLIC_MEMBER)`.

## References

-   <a href="https://jsr311.java.net/" class="external-link">JAX-RS (JSR311) home page</a>
    -   <a href="https://jsr311.java.net/nonav/releases/1.0/spec/index.html" class="external-link">1.0 Spec</a> (<a href="http://jcp.org/aboutJava/communityprocess/final/jsr311/index.html" class="external-link">pdf</a>)
    -   <a href="https://jsr311.java.net/nonav/releases/1.0/index.html" class="external-link">1.0 API</a>
-   <a href="https://jersey.github.io/" class="external-link">Jersey home page</a>
    -   <a href="https://jersey.github.io/documentation/1.19.1/index.html" class="external-link">Wiki</a>
    -   1.0.3 API (<a href="https://jersey.github.io/apidocs/1.0.3/jersey/index.html" class="uri external-link">https://jersey.github.io/apidocs/1.0.3/jersey/index.html</a>) (implements JAX-RS 1.0)
    -   <a href="https://blogs.oracle.com/enterprisetechtips/entry/configuring_json_for_restful_web" class="external-link">Configuring JSON for RESTful Web Services in Jersey 1.0</a>

##### RELATED TOPICS

[Developing a REST Service Plugin](/server/framework/atlassian-sdk/developing-a-rest-service-plugin)  
[Atlassian REST API Design Guidelines version 1](/server/framework/atlassian-sdk/atlassian-rest-api-design-guidelines-version-1)  
[Guidelines for Atlassian REST API Design](https://developer.atlassian.com/display/REST/Guidelines+for+Atlassian+REST+API+Design)  
[Atlassian Plugin Framework Documentation](https://developer.atlassian.com/display/PLUGINFRAMEWORK)






































































































































































































