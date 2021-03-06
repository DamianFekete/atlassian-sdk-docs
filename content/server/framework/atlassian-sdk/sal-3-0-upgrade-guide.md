---
aliases:
- /server/framework/atlassian-sdk/sal-3.0-upgrade-guide-35721084.html
- /server/framework/atlassian-sdk/sal-3.0-upgrade-guide-35721084.md
category: devguide
confluence_id: 35721084
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=35721084
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=35721084
date: '2017-12-08'
legacy_title: SAL 3.0 Upgrade Guide
platform: server
product: atlassian-sdk
subcategory: updates
title: SAL 3.0 upgrade guide
---
# SAL 3.0 upgrade guide

## Atlassian Scheduler replaces PluginScheduler

`PluginScheduler` and `PluginJob` (from `com.atlassian.sal.api.scheduling`) are deprecated - clients should use the new Atlassian Scheduler library, as [documented here](https://developer.atlassian.com/display/JIRADEV/Plugin+Guide+to+JIRA+High+Availability+and+Clustering#PluginGuidetoJIRAHighAvailabilityandClustering-Scheduledtasksandbackgroundprocesses).

## `LifecycleAware` gets `onStop()` method

In addition to onStart(), LifecycleAware interface gets a symmetric onStop() method to notify plugins they are being stopped. It's a good place to do tasks just before plugin is disabled when all it's dependencies are still present.

The method is called when:

-   plugin is being disabled
-   plugin framework is shutting down

There is no need to recompile all plugins for the updated interface; onStop() call is made in a way that tolerates plugins compiled against the old interface. However, plugins that compile against the updated interface will need to implement it.

## Atlassian annotations imported

Annotations from <a href="https://bitbucket.org/atlassian/atlassian-annotations/overview" class="external-link">atlassian-annotations</a> library are not packaged with sal-api and needs to be provided in run time.

## `Request` interface changed

### Trusted apps functionality moved to a standalone library

Trusted apps `com.atlassian.sal.api.net.Request` functionality moved into `com.atlassian.sal.api.net.TrustedRequest:`

-   `addTrustedTokenAuthentication()`
-   `addTrustedTokenAuthentication(String username)`

### `Request` and `TrustedRequest` authentication methods get `hostname` parameter

Authentication methods listed below get `hostname` parameter:

-   addBasicAuthentication
-   addTrustedTokenAuthentication

### `setRequestContentType` removed

Use `setRequestBody(String requestBody, String contentType)` instead

## New! TransactionalExecutor

Plugin developers may retrieve a java.sql.Connection from the application and execute DML, albeit with some limitations.

See <a href="https://docs.atlassian.com/sal-api/3.0.0/sal-api/apidocs/com/atlassian/sal/api/rdbms/TransactionalExecutor.html" class="external-link">TransactionalExecutor</a> for an documentation and example.

See <a href="https://bitbucket.org/acourtis/rdbms-plugin-examples" class="uri external-link">bitbucket.org/acourtis/rdbms-plugin-examples</a> for some Hibernate and QueryDSL samples.
