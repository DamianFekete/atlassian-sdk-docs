---
aliases:
- /server/framework/atlassian-sdk/sal-services-5242921.html
- /server/framework/atlassian-sdk/sal-services-5242921.md
category: devguide
confluence_id: 5242921
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5242921
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5242921
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/shared-access-layer/sal-services
new_url: /server/framework/atlassian-sdk/sal-services
platform: server
product: atlassian-sdk
subcategory: learning
title: SAL services
---
# SAL services

Below is a list of the services provided by the Atlassian [Shared Access Layer](https://developer.atlassian.com/display/SAL/Shared+Access+Layer+Documentation). You will find more developer help in the <a href="http://docs.atlassian.com/sal-api/" class="external-link">Javadoc</a>.

## Service Descriptions and Examples

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api`

#### `ApplicationProperties`

Exposes key application settings such as the base URL, application name, build information and version number.

Example -- Obtaining base url of the application:

``` javascript
public class DefaultStudioInfo
{
private final ApplicationProperties applicationProperties;

public DefaultStudioInfo(final ApplicationProperties applicationProperties)
{
this.applicationProperties = applicationProperties;
}

public String getCurrentAppBaseUrl()
{
return applicationProperties.getBaseUrl();
}
}
```

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.auth`

#### `AuthenticationController`

Allows the host application to communicate about when authentication should be performed and users allowed to login.

#### `AuthenticationListener`

Allows the underlying framework to take some actions on authentication events.

#### `Authenticator`

Marker interface for classes that can authenticate requests.

#### `LoginUriProvider`

Provides the URI to redirect users to so that they can log in before they can authorise consumer requests to access their data.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.component`

#### `ComponentLocator`

Gives access to the application's component container instances.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.executor`

#### `ThreadLocalDelegateExecutorFactory`

Factory to create Executor instances that delegate to a specific Executor and ensure the executed code runs in the same thread local context.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.license`

#### `LicenseHandler`

Handles setting and retrieving the application's license.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.lifecycle`

#### `LifecycleAware`

Marks a class that wants to execute code on certain application-level lifecycle stages.

#### `LifecycleManager`

Interface to be used to trigger lifecycle events. Handles lifecycle events by calling LifecycleAware methods on registered beans.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.message`

#### `I18nResolver`

Resolves an internationalisation key or key/argument pair to its internationalised message.

#### `LocaleResolver`

Used to retrieve the user's locale, based on the remote users preferences, or the preferred locale as specified in the request or finally defaulting to the system locale if no preferred locale is set.

#### `Message`

Encapsulates a message before it has been resolved via an I18N resolver.

#### `MessageCollection`

A collection of messages that have not been resolved.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.net`

#### `Request`

Represents a request to retrieve data. To execute a request call `Request#execute(ResponseHandler)`.

#### `RequestFactory`

Provides a factory for making HTTP requests with optional authentication.

Example -- Running remote search:

``` javascript
public class RemoteSearcher
{
private final String url;
private static final String SEARCH_PLUGIN_PATH = "/plugins/servlet/studio/search";
private final RequestFactory<?> requestFactory;

public RemoteSearcher(final String url, final RequestFactory<?> requestFactory)
{
this.url = url;
this.requestFactory = requestFactory;
}

public SearchResults search(final String remoteUser, final String query)
{
final String fullUrl = url + SEARCH_PLUGIN_PATH + "?query=" + URIUtil.encodeWithinQuery(query);

final Request<?> request = requestFactory.createRequest(MethodType.GET, fullUrl);
request.addTrustedTokenAuthentication(); // this takes username from ThreadLocal
try
{
// parse the response
final String responseString = request.execute();
return (SearchResults) XStreamUtils.fromXML(responseString);
}
catch (final ResponseException e)
{
throw new RuntimeException("Search for " + query + " on " + fullUrl + " failed.", e);
}
}
}
```

#### `Response`

Represents the response when calling `Request#execute(ResponseHandler)`.

#### `ResponseException`

Exception thrown by `Request#execute(ResponseHandler)` and `Request#handle(ResponseHandler)`.

#### `ResponseHandler`

Callback interface used by `Request#execute(ResponseHandler)` method. Implementation of this interface performs actual handling of the response.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.net.auth`

#### `Authenticator`

Marker interface for an authenticator.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.pluginsettings`

#### `PluginSettings`

Provides access to settings globally or per project/space/repository.

Example -- Saving and retrieving custom settings per project:

``` javascript
public class CustomProjectSettings
{
private final PluginSettingsFactory pluginSettingsFactory;
private final String projectKey;

public CustomProjectSettings(final PluginSettingsFactory pluginSettingsFactory, final String projectKey)
{
this.pluginSettingsFactory = pluginSettingsFactory;
this.projectKey = projectKey;
}

public void setValue(final String key, final String value)
{
final PluginSettings settings = pluginSettingsFactory.createSettingsForKey(projectKey);
settings.put(key, value);
}

public Object getValue(final String key)
{
final PluginSettings settings = pluginSettingsFactory.createSettingsForKey(projectKey);
return settings.get(key);
}
}
```

#### `PluginSettingsFactory`

One feature provided by SAL is storage of plugin settings, for global and project-specific settings. You will create a `PluginSettings` object via a `PluginSettingsFactory`, which uses the <a href="http://en.wikipedia.org/wiki/Abstract_factory_pattern" class="external-link">abstract factory pattern</a>. Refer to the developer blog post on <a href="http://blogs.atlassian.com/developer/2009/01/post_1.html" class="external-link">Storing plugin settings with the abstract factory pattern</a>.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.project`

#### `ProjectManager`

Provides a list of projects. A project may represent different things depending on the application. For example, in Confluence it is a space, in Bamboo it is a build plan, and in JIRA it is a project.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.scheduling`

#### `PluginJob`

A job to be executed by the PluginScheduler.

#### `PluginScheduler`

Schedules plugin jobs programmatically.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.search`

#### `ResourceType`

Defines the more information about the search resource (e.g. JIRA, wiki).

#### `SearchMatch`

A single match for a query (e.g. an issue, a wiki page, a commit). The match contains a URL, title and possibly an excerpt. The `resourceType` contains more information about the source of this `searchMatch`.

#### `SearchProvider`

Executes search queries. Allows for simple string based searches in an application.

#### `SearchResults`

Provides searchresults for a query.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.search.parameter`

#### `SearchParameter`

Allows you to specify additional properties for a search as string value pairs. For example this could specify a `fixforversion=3.12` in JIRA, or `application=crucible` in FishEye.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.search.query`

#### `SearchQuery`

Utility to help with creating a query string.

#### `SearchQueryParser`

Parses a search query.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.transaction`

#### `TransactionCallback`

A simple callback that needs to be provided with an action to run in the `doInTransaction` method. It is assumed that if anything goes wrong, `doInTransaction` will throw a `RuntimeException` and the calling `transactionTemplate` will roll back the transaction.

#### `TransactionTemplate`

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.timezone`

#### `TimeZoneManager`

Available since SAL 2.6.  
Provides timezone information about the users and about the application.

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.upgrade`

#### `PluginUpgradeManager`

Provides a plugin upgrade framework that will recognise `PluginUpgradeTask` tasks and run them on startup.

#### `PluginUpgradeTask`

### ![](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.user`

#### `UserManager`

Provides simplified access to users across various applications, and performs user authentication checks.

#### `UserResolutionException`

## Services Available per Application

The matrix below shows the services available to each version of the Atlassian applications that support the Shared Access Layer. The applications are listed horizontally across the top and the SAL versions are listed vertically on the left.

-   Version numbers in brackets indicate a future application release expected to support the relevant SAL services.
-   YES shows that the SAL service is available to the relevant version of the application.
-   NO means that the service is not available to the relevant version of the application.

<table style="width:100%;">
<colgroup>
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
</colgroup>
<thead>
<tr class="header">
<th><p>SAL Service</p></th>
<th><p>JIRA<br />
3.13</p></th>
<th><p>(JIRA<br />
4.0)</p></th>
<th><p>Confluence<br />
3.0</p></th>
<th><p>FishEye/<br />
Crucible<br />
1.6.5</p></th>
<th><p>FishEye/<br />
Crucible<br />
2.0</p></th>
<th><p>Crowd<br />
2.0</p></th>
<th><p>Bamboo<br />
2.3</p></th>
<th><p>RefImpl</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>ApplicationProperties</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.auth</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>AuthenticationController</strong></p></td>
<td><p>NO</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
<td><p>NO</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
</tr>
<tr class="odd">
<td><p><strong>AuthenticationListener</strong></p></td>
<td><p>NO</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
<td><p>NO</p></td>
<td><p>NO<br />
 </p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
</tr>
<tr class="even">
<td><p>Authenticator </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>LoginUriProvider</strong></p></td>
<td><p>NO</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
<td><p>NO</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.component</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>ComponentLocator</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.executor</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>ThreadLocalDelegateExecutorFactory</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.license</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>LicenseHandler</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.lifecycle</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>LifecycleAware</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>LifecycleManager</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.message</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>I18nResolver</strong></p></td>
<td><p>YES</p></td>
<td><p>?</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p><strong>LocaleResolver</strong></p></td>
<td><p>YES</p></td>
<td><p>?</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p>Message</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>MessageCollection</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.net</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Request</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>RequestFactory</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>?</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p>Response</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>ResponseException</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>ResponseHandler</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.net.auth</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>Authenticator</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.pluginsettings</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>PluginSettings</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>PluginSettingsFactory</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.project</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>ProjectManager</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.scheduling</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>PluginJob</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>PluginScheduler</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.search</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>ResourceType</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>SearchMatch</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>SearchProvider</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p>SearchResults</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.search.parameter</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>SearchParameter</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.search.query</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>SearchQuery</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>SearchQueryParser</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>NO</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.transaction</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>TransactionCallback</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>TransactionTemplate </strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.upgrade</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><strong>PluginUpgradeManager</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="odd">
<td><p>PluginUpgradeTask</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.user</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p><strong>UserManager</strong></p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
<td><p>YES</p></td>
</tr>
<tr class="even">
<td><p>UserResolutionException</p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

##### RELATED TOPICS

<a href="http://docs.atlassian.com/sal-api/" class="external-link">Javadoc</a>  
[About SAL Development](/server/framework/atlassian-sdk/about-sal-development)















































































































































































































































