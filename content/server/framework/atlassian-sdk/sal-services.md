---
aliases:
- /server/framework/atlassian-sdk/sal-services-5242921.html
- /server/framework/atlassian-sdk/sal-services-5242921.md
category: devguide
confluence_id: 5242921
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5242921
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5242921
date: '2017-12-08'
legacy_title: SAL Services
platform: server
product: atlassian-sdk
subcategory: learning
title: SAL services
---
# SAL services

Below is a list of the services provided by the Atlassian [Shared Access Layer](https://developer.atlassian.com/display/SAL/Shared+Access+Layer+Documentation). You will find more developer help in the <a href="http://docs.atlassian.com/sal-api/" class="external-link">Javadoc</a>.

## Service Descriptions and Examples

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api`

#### `ApplicationProperties`

Exposes key application settings such as the base URL, application name, build information and version number.

Example -- Obtaining base url of the application:

``` java
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

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.auth`

#### `AuthenticationController`

Allows the host application to communicate about when authentication should be performed and users allowed to login.

#### `AuthenticationListener`

Allows the underlying framework to take some actions on authentication events.

#### `Authenticator`

Marker interface for classes that can authenticate requests.

#### `LoginUriProvider`

Provides the URI to redirect users to so that they can log in before they can authorise consumer requests to access their data.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.component`

#### `ComponentLocator`

Gives access to the application's component container instances.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.executor`

#### `ThreadLocalDelegateExecutorFactory`

Factory to create Executor instances that delegate to a specific Executor and ensure the executed code runs in the same thread local context.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.license`

#### `LicenseHandler`

Handles setting and retrieving the application's license.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.lifecycle`

#### `LifecycleAware`

Marks a class that wants to execute code on certain application-level lifecycle stages.

#### `LifecycleManager`

Interface to be used to trigger lifecycle events. Handles lifecycle events by calling LifecycleAware methods on registered beans.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.message`

#### `I18nResolver`

Resolves an internationalisation key or key/argument pair to its internationalised message.

#### `LocaleResolver`

Used to retrieve the user's locale, based on the remote users preferences, or the preferred locale as specified in the request or finally defaulting to the system locale if no preferred locale is set.

#### `Message`

Encapsulates a message before it has been resolved via an I18N resolver.

#### `MessageCollection`

A collection of messages that have not been resolved.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.net`

#### `Request`

Represents a request to retrieve data. To execute a request call `Request#execute(ResponseHandler)`.

#### `RequestFactory`

Provides a factory for making HTTP requests with optional authentication.

Example -- Running remote search:

``` java
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

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.net.auth`

#### `Authenticator`

Marker interface for an authenticator.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.pluginsettings`

#### `PluginSettings`

Provides access to settings globally or per project/space/repository.

Example -- Saving and retrieving custom settings per project:

``` java
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

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.project`

#### `ProjectManager`

Provides a list of projects. A project may represent different things depending on the application. For example, in Confluence it is a space, in Bamboo it is a build plan, and in JIRA it is a project.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.scheduling`

#### `PluginJob`

A job to be executed by the PluginScheduler.

#### `PluginScheduler`

Schedules plugin jobs programmatically.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.search`

#### `ResourceType`

Defines the more information about the search resource (e.g. JIRA, wiki).

#### `SearchMatch`

A single match for a query (e.g. an issue, a wiki page, a commit). The match contains a URL, title and possibly an excerpt. The `resourceType` contains more information about the source of this `searchMatch`.

#### `SearchProvider`

Executes search queries. Allows for simple string based searches in an application.

#### `SearchResults`

Provides searchresults for a query.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.search.parameter`

#### `SearchParameter`

Allows you to specify additional properties for a search as string value pairs. For example this could specify a `fixforversion=3.12` in JIRA, or `application=crucible` in FishEye.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.search.query`

#### `SearchQuery`

Utility to help with creating a query string.

#### `SearchQueryParser`

Parses a search query.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.transaction`

#### `TransactionCallback`

A simple callback that needs to be provided with an action to run in the `doInTransaction` method. It is assumed that if anything goes wrong, `doInTransaction` will throw a `RuntimeException` and the calling `transactionTemplate` will roll back the transaction.

#### `TransactionTemplate`

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.timezone`

#### `TimeZoneManager`

Available since SAL 2.6.  
Provides timezone information about the users and about the application.

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.upgrade`

#### `PluginUpgradeManager`

Provides a plugin upgrade framework that will recognise `PluginUpgradeTask` tasks and run them on startup.

#### `PluginUpgradeTask`

### ![Package](/server/framework/atlassian-sdk/images/package2.gif) `com.atlassian.sal.api.user`

#### `UserManager`

Provides simplified access to users across various applications, and performs user authentication checks.

#### `UserResolutionException`

## Services Available per Application

The matrix below shows the services available to each version of the Atlassian applications that support the Shared Access Layer. The applications are listed horizontally across the top and the SAL versions are listed vertically on the left.

-   Version numbers in brackets indicate a future application release expected to support the relevant SAL services.
-   YES shows that the SAL service is available to the relevant version of the application.
-   NO means that the service is not available to the relevant version of the application.

![Package](/server/framework/atlassian-sdk/images/package2.gif) **com.atlassian.sal.api**

|SAL Service           |ApplicationProperties|
|----------------------|---------------------|
|JIRA 3.13             |YES                  |
|(JIRA 4.0)            |YES                  |
|Confluence            |YES                  |
|FishEye/Crucible 1.6.5|YES                  |
|FishEye/Crucible 2.0  |YES                  |
|Crowd 2.0             |YES                  |
|Bamboo 2.3            |YES                  |
|RefImpl               |YES                  |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.auth**

|SAL Service           |ApplicationController, ApplicationListener, LoginUriProvider|Authenticator|
|----------------------|------------------------------------------------------------|-------------|
|JIRA 3.13             |NO                                                          |             |
|(JIRA 4.0)            |NO                                                          |             |
|Confluence            |YES                                                         |             |
|FishEye/Crucible 1.6.5|NO                                                          |             |
|FishEye/Crucible 2.0  |NO                                                          |             |
|Crowd 2.0             |NO                                                          |             |
|Bamboo 2.3            |YES                                                         |             |
|RefImpl               |NO                                                          |             |
 
**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.component**

|SAL Service           |ComponentLocator|
|----------------------|----------------|
|JIRA 3.13             |YES             |
|(JIRA 4.0)            |YES             |                  
|Confluence            |YES             |                  
|FishEye/Crucible 1.6.5|YES             |                  
|FishEye/Crucible 2.0  |YES             |                  
|Crowd 2.0             |YES             |
|Bamboo 2.3            |YES             |
|RefImpl               |YES             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.executor**

|SAL Service           |ThreadLocalDelegateExecutorFactory|
|----------------------|----------------|
|JIRA 3.13             |YES             |
|(JIRA 4.0)            |YES             |                  
|Confluence            |YES             |                  
|FishEye/Crucible 1.6.5|YES             |                  
|FishEye/Crucible 2.0  |YES             |                  
|Crowd 2.0             |NO              |
|Bamboo 2.3            |YES             |
|RefImpl               |YES             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.license**

|SAL Service           |LicenseHandler  |
|----------------------|----------------|
|JIRA 3.13             |YES             |
|(JIRA 4.0)            |YES             |                  
|Confluence            |YES             |                  
|FishEye/Crucible 1.6.5|YES             |                  
|FishEye/Crucible 2.0  |YES             |                  
|Crowd 2.0             |YES             |
|Bamboo 2.3            |NO              |
|RefImpl               |YES             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.lifecycle**

|SAL Service           |LifecycleManager|LifecycleAware|
|----------------------|----------------|-------------|
|JIRA 3.13             |YES             |             |
|(JIRA 4.0)            |YES             |             |
|Confluence            |YES             |             |
|FishEye/Crucible 1.6.5|YES             |             |
|FishEye/Crucible 2.0  |YES             |             |
|Crowd 2.0             |YES             |             |
|Bamboo 2.3            |YES             |             |
|RefImpl               |YES             |             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif)com.atlassian.sal.api.message**

|SAL Service           |I18nResolver, LocaleResolver|Message, MessageCollection|
|----------------------|------------------------------------------------------------|-------------|
|JIRA 3.13             |YES                                                          |             |
|(JIRA 4.0)            |?                                                          |             |
|Confluence            |YES                                                         |             |
|FishEye/Crucible 1.6.5|YES                                                          |             |
|FishEye/Crucible 2.0  |YES                                                          |             |
|Crowd 2.0             |YES                                                          |             |
|Bamboo 2.3            |YES                                                         |             |
|RefImpl               |YES                                                          |             |

**<a href="http://com.atlassian.sal.api.net/" class="external-link"><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.net</a>**

|SAL Service           |RequestFactory|Request, Response, ResponseException, ResponseHandler|
|----------------------|--------------|-----------------------------------------------------|
|JIRA 3.13             |YES           |                                                     |
|(JIRA 4.0)            |YES           |                                                     |
|Confluence            |YES           |                                                     |
|FishEye/Crucible 1.6.5|YES           |                                                     |
|FishEye/Crucible 2.0  |YES           |                                                     |
|Crowd 2.0             |YES           |                                                     |
|Bamboo 2.3            |?             |                                                     |
|RefImpl               |YES           |                                                     |
 

**<a href="http://com.atlassian.sal.api.net/" class="external-link"><img src="/server/framework/atlassian-sdk/images/package2.gif" /> com.atlassian.sal.api.net</a>.auth**

|SAL Service           |Authenticator|
|----------------------|-------------|
|JIRA 3.13             |             |             
|(JIRA 4.0)            |             |      
|Confluence            |             |          
|FishEye/Crucible 1.6.5|             |          
|FishEye/Crucible 2.0  |             |           
|Crowd 2.0             |             |            
|Bamboo 2.3            |             |           
|RefImpl               |             |            
 
**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.pluginsettings**

|SAL Service           |PluginSettingsFactory|PluginSettings|
|----------------------|----------------|-------------|
|JIRA 3.13             |YES             |             |
|(JIRA 4.0)            |YES             |             |
|Confluence            |YES             |             |
|FishEye/Crucible 1.6.5|YES             |             |
|FishEye/Crucible 2.0  |YES             |             |
|Crowd 2.0             |YES             |             |
|Bamboo 2.3            |YES             |             |
|RefImpl               |YES             |             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.project**

|SAL Service           |ProjectManager       |
|----------------------|---------------------|
|JIRA 3.13             |YES                  |
|(JIRA 4.0)            |YES                  |
|Confluence            |YES                  |
|FishEye/Crucible 1.6.5|YES                  |
|FishEye/Crucible 2.0  |YES                  |
|Crowd 2.0             |YES                  |
|Bamboo 2.3            |YES                  |
|RefImpl               |YES                  |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.scheduling**

|SAL Service           |PluginScheduler |PluginJob    |
|----------------------|----------------|-------------|
|JIRA 3.13             |YES             |             |
|(JIRA 4.0)            |YES             |             |
|Confluence            |YES             |             |
|FishEye/Crucible 1.6.5|YES             |             |
|FishEye/Crucible 2.0  |YES             |             |
|Crowd 2.0             |YES             |             |
|Bamboo 2.3            |YES             |             |
|RefImpl               |YES             |             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.search**

|SAL Service           |SearchProvider|ResourceType, SearchMatch, SearchResults             |
|----------------------|--------------|-----------------------------------------------------|
|JIRA 3.13             |YES           |                                                     |
|(JIRA 4.0)            |YES           |                                                     |
|Confluence            |YES           |                                                     |
|FishEye/Crucible 1.6.5|YES           |                                                     |
|FishEye/Crucible 2.0  |YES           |                                                     |
|Crowd 2.0             |YES           |                                                     |
|Bamboo 2.3            |NO            |                                                     |
|RefImpl               |YES           |                                                     |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.search.parameter**

|SAL Service           |SearchParameter|
|----------------------|-------------|
|JIRA 3.13             |             |             
|(JIRA 4.0)            |             |      
|Confluence            |             |          
|FishEye/Crucible 1.6.5|             |          
|FishEye/Crucible 2.0  |             |           
|Crowd 2.0             |             |            
|Bamboo 2.3            |             |           
|RefImpl               |             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.search.query**

|SAL Service           |SearchQueryParser|SearchQuery |
|----------------------|----------------|-------------|
|JIRA 3.13             |YES             |             |
|(JIRA 4.0)            |YES             |             |
|Confluence            |YES             |             |
|FishEye/Crucible 1.6.5|YES             |             |
|FishEye/Crucible 2.0  |YES             |             |
|Crowd 2.0             |YES             |             |
|Bamboo 2.3            |NO              |             |
|RefImpl               |YES             |             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.transaction**

|SAL Service           |TransactionTemplate|TransactionCallback|
|----------------------|----------------|-------------|
|JIRA 3.13             |YES             |             |
|(JIRA 4.0)            |YES             |             |
|Confluence            |YES             |             |
|FishEye/Crucible 1.6.5|YES             |             |
|FishEye/Crucible 2.0  |YES             |             |
|Crowd 2.0             |YES             |             |
|Bamboo 2.3            |YES             |             |
|RefImpl               |YES             |             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif) com.atlassian.sal.api.upgrade**

|SAL Service           |PluginUpgradeManager|PluginUpgradeTask|
|----------------------|----------------|-------------|
|JIRA 3.13             |YES             |             |
|(JIRA 4.0)            |YES             |             |
|Confluence            |YES             |             |
|FishEye/Crucible 1.6.5|YES             |             |
|FishEye/Crucible 2.0  |YES             |             |
|Crowd 2.0             |YES             |             |
|Bamboo 2.3            |YES             |             |
|RefImpl               |YES             |             |

**![Package](/server/framework/atlassian-sdk/images/package2.gif)com.atlassian.sal.api.user**

|SAL Service           |UserManager|UserResolutionException|
|----------------------|----------------|-------------|
|JIRA 3.13             |YES             |             |
|(JIRA 4.0)            |YES             |             |
|Confluence            |YES             |             |
|FishEye/Crucible 1.6.5|YES             |             |
|FishEye/Crucible 2.0  |YES             |             |
|Crowd 2.0             |YES             |             |
|Bamboo 2.3            |YES             |             |
|RefImpl               |YES             |             |

##### RELATED TOPICS

<a href="http://docs.atlassian.com/sal-api/" class="external-link">Javadoc</a>  
[About SAL Development](/server/framework/atlassian-sdk/about-sal-development)
