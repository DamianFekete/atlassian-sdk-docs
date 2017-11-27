---
title: Basics Of Exposing REST APIs via Plugins 4915229
aliases:
    - /server/framework/atlassian-sdk/basics-of-exposing-rest-apis-via-plugins-4915229.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=4915229
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=4915229
confluence_id: 4915229
platform:
product:
category:
subcategory:
---
# Documentation : Basics of Exposing REST APIs via Plugins

This page gives an overview of a REST implementation, using the [Atlassian REST plugin module](https://developer.atlassian.com/display/REST/REST+Plugin+Module).

## Getting from the URL to the Java Objects

Given a URL like this:

``` javascript
http://myhost.com:port/myapp/rest/api-name/api-version/resource-name
```

We can break the URL into these parts:

1.  `http://myhost.com:port`
2.  `/myapp`
3.  `/rest`
4.  `/api-name/api-version`
5.  `/resource-name`

Mapping each part of the URL:

1.  The operating system directs the request to the application server (e.g. Tomcat) that handles the specified port.
2.  Tomcat directs the request to the application `myapp`.
3.  The application's <a href="http://wiki.metawerx.net/wiki/Web.xml" class="external-link">web.xml</a> deployment descriptor file maps the URLs to the relevant servlets. So in this case, it maps `/rest` to our REST servlet, which points to our [REST plugin module type](https://developer.atlassian.com/display/REST/REST+Plugin+Module).
4.  Now the REST plugin module takes over. The relevant part of the URL (`api-name` and `api-version`) are defined as the `path` and `version` in the `atlassian-plugin.xml` file e.g.
    ``` javascript
    <rest key="helloWorldRest" path="/helloworld" version="1.0">
        <description>Provides hello world services.</description>
    </rest>
    ```

5.  The final part of the URL mapping (`resource-name` and sub-elements) is done via annotations on the class, used to declare the URI path, the HTTP method and the media type. <a href="https://jersey.dev.java.net/" class="external-link">Jersey</a> (based on <a href="https://jsr311.dev.java.net/" class="external-link">JAX-RS</a>) reads the `@Provider` and `@Path` annotations and maps them to classes and methods, so that we know which method is called for each REST resource and method. See the <a href="https://jersey.dev.java.net/use/getting-started.html" class="external-link">Jersey documentation</a>.

## Getting from the Java Objects to XML and JSON

<a href="http://java.sun.com/developer/technicalArticles/WebServices/jaxb/" class="external-link">JAXB</a> converts the Java classes to XML or JSON and vice versa, making use of <a href="https://jaxb.dev.java.net/nonav/2.1.3/docs/api/javax/xml/bind/annotation/package-summary.html" class="external-link">JAXB annotations</a>. (Available in Java 1.5 and later.)

For example a Java `User` object with JAXB annotations may look something like this:

``` javascript
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

``` javascript
<user>
    <firstName>John</firstName>
    <lastName>Smith</lastName>
</user>
```

By default, on conversion the XML element name will be the same as the object name. Alternatively, you can add the XML element name to the annotation. Something like this: `@XmlRootElement(name="principal")`. There are specific annotations for arrays, etc. See <a href="https://jaxb.dev.java.net/" class="external-link">JAXB's documentation</a> for more details on this.

![(info)](/server/framework/atlassian-sdk/images/icons/emoticons/information.png) We have no schema or DTD.

Jersey also handles JSON based on the same JAXB objects as in the example above. The JSON for the example would be:

``` javascript
{
  "firstName":"John",
  "lastName":"Smith"
}
```

A trivial REST service class with a single URL returning an instance of `User` would look like this:

``` javascript
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

##### Related Topics

<a href="/pages/createpage.action?spaceKey=REST&amp;title=Developing+a+REST+Service+Plugin" class="createlink">Developing a REST Service Plugin</a>  
[REST Plugin Module](https://developer.atlassian.com/display/REST/REST+Plugin+Module)  
[Guidelines for Atlassian REST API Design](https://developer.atlassian.com/display/REST/Guidelines+for+Atlassian+REST+API+Design)
















































































































































































































































































































