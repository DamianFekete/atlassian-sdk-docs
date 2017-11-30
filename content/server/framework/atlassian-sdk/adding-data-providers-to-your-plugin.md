---
aliases:
- /server/framework/atlassian-sdk/adding-data-providers-to-your-plugin-33736398.html
- /server/framework/atlassian-sdk/adding-data-providers-to-your-plugin-33736398.md
category: devguide
confluence_id: 33736398
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=33736398
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=33736398
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/adding-data-providers-to-your-plugin
new_url: /server/framework/atlassian-sdk/adding-data-providers-to-your-plugin
platform: server
product: atlassian-sdk
subcategory: learning
title: Adding data providers to your plugin
---
# Adding data providers to your plugin

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p>Atlassian Plugins Webresources 3.0 and later.</p></td>
</tr>
</tbody>
</table>

 

## Overview

Data providers are used to expose chunks of JSON data to your client-side JavaScript code.

Examples of data that you may want to expose to the client are:

-   plugin configuration options, for example, configuration that can be changed by an application administrator
-   information about the currently logged-in user, such as user details, recently viewed issue keys, or recently viewed pages
-   per-user configuration, such as whether the current user has seen onboarding information

A plugin is a good candidate for converting to a data provider, if there is any code in the plugin that either:

-   executes an AJAX request on page load, or
-   serializes configuration data into HTML during page rendering (e.g. using a `<meta>` tag).

Note that currently, data providers can only retrieve the global context, such as the logged-in user or per-instance configuration. Data providers do not have access to any context relating to the page being rendered. For example, a data provider can't find out if the current page is a "view issue page" or what the key of the issue being rendered is.

### Sample code

A demonstration plugin using data providers is available at <a href="https://bitbucket.org/atlassian/page-data-demo" class="uri external-link">https://bitbucket.org/atlassian/page-data-demo</a>. Code samples on this page are taken from that repository.

## Using data providers

There are two ways to use data providers:

-   in a `<web-resource>` definition, or
-   directly during page rendering.

### Defining a data provider in a web resource

As a plugin author (for example, if you are enhancing a page by adding yourself to a web-resource context), you should declare a data provider in a `<web-resource>` definition.

``` xml
<web-resource key="simple-web-resource">
    <data key="simple-data" class="com.atlassian.plugins.jira.page.data.demo.SimpleDemoDataProvider" />
</web-resource>
```

Data providers have two required attributes:

-   **key** - The key that client-side code will use to retrieve your JSON data. See [Consuming a data provider](#consuming-a-data-provider) below.
-   **class** - The class implementation that provides data. This class must implement the `WebResourceDataProvider` interface, detailed below.

`WebResourceDataProvider` (`com.atlassian.webresource.api.data.WebResourceDataProvider`) is the interface for all data providers. It contains a single method:

``` java
interface WebResourceDataProvider {
    Jsonable get();
}
```

See [About Jsonable's](#about-jsonable's) below for information on what this `get()` method should be returning.

### Injecting data during page rendering

If you are rendering a page yourself, you can inject JSON data directly into the page by using the `PageBuilderService`:

``` java
pageBuilderService.assembler().data().requireData("simple-data-key", createSimpleJsonable());
```

Note that `com.atlassian.webresource.api.assembler.PageBuilderService` is an injectable service, used when building HTML pages.

## About Jsonable's

`Jsonable` (`com.atlassian.json.marshal.Jsonable`) is an interface that streams JSON data to a `java.io.Writer`:

``` java
interface Jsonable {
    void write(Writer writer) throws IOException;
}
```

To implement a simple `DataProvider`, you can return a simple Jsonable interface such as `JsonableString`:

``` java
public class SimpleDemoDataProvider implements WebResourceDataProvider {
    @Override
    public Jsonable get() {
        return new JsonableString("Hello world!");
    }
}
```

`JsonableString` wraps a string in the Jsonable interface. Similar wrappers exist for Booleans (`JsonableBoolean`) and Number (`JsonableNumber`) respectively.

## Providing large data

The Jsonable interface is **designed to be streamy**. For larger objects, using the `Jsonable` interface correctly means that the JSON representation of your data will be written directly to the HTTP output stream. This avoids serialization to a potentially large JSON string in-memory.

You can provide your own lightweight `Jsonable` in your `WebResourceDataProvider`. The following code converts a <a href="https://code.google.com/p/google-gson/" class="external-link">GSON</a> object to the `Jsonable` interface:

``` java
public class GsonDemoDataProvider implements WebResourceDataProvider {
    @Override
    public Jsonable get() {
        return new Jsonable() {
            @Override
            public void write(Writer writer) throws IOException {
                Gson gson = new Gson();
                gson.toJson(sampleData(), Map.class, new PrintWriter(writer));
            }
        };
    }
    public Map<String, Object> sampleData() {
        Map<String, Object> map = new HashMap<String, Object>();
        map.put("name", "Fido");
        map.put("species", "Canine");
        map.put("breed", "Shiba Inu");
        return map;
    }
}
```

## Consuming a data provider

Declaring a `<data>` element means that the object it returns will be serialized as JSON and sent to the HTML page being rendered.

To access this data in the browser, call:

``` javascript
WRM.data.claim(complete-data-key)
```

`complete-data-key` is of the form `[groupId].[artifactId]:[web-resource-key].[data-key]`, where:

-   `groupId` and `artifactId` are the relevant values for your plugin
-   `web-resource-key` is the key of the `<web-resource>` in which your `<data>` element is defined
-   `data-key` is the key on your `<data>` element

An example from the sample plugin is:

``` javascript
var SIMPLE_DATA_KEY = 'com.atlassian.plugins.jira.page-data-demo:demo.simple-data';
console.log(WRM.data.claim(SIMPLE_DATA_KEY));
```

There are two important things to note about using data on the client:

-   `WRM.data.claim` can \*only be called once for a single data key\*. The clientside web-resource manager (WRM) releases the data object for garbage collection after the first time it's claimed. If you want to access the data multiple times from your JS code, it's up to you to store it in your own variable. This behaviour was chosen to support use cases involving large data blobs. For example, a data provider may return a collection of JIRA issues to render client-side. This web-resource manager should not hold onto this collection internally after it's first claimed.
-   Within a single `<web-resource>`, `<data>` elements will always be rendered onto the page before `<resource>` elements such as JavaScript files. This makes it safe to call "`WRM.data.claim`" on a `<data>` element from a JavaScript resource in the same `<web-resource>`.
































































































