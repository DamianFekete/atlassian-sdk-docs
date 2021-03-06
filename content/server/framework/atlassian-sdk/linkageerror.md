---
aliases:
- /server/framework/atlassian-sdk/linkageerror-851986.html
- /server/framework/atlassian-sdk/linkageerror-851986.md
category: devguide
confluence_id: 851986
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851986
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851986
date: '2017-12-08'
legacy_title: LinkageError
platform: server
product: atlassian-sdk
subcategory: faq
title: LinkageError
---
# LinkageError

### Symptoms -- What Goes Wrong

The logs contain an exception: `java.lang.LinkageError: Class my/package/MyClass violates loader constraints`.

### Cause

While linkage errors have a number of causes, a common cause for OSGi plugins is when two copies of the same class try to interact through a shared class. Most commonly, this is because the plugin is bundling a dependent JAR in `META-INF/lib`, but that same JAR is also available via the host application in its `WEB-INF/lib`. If the plugin interacts with an object that references the dependency, the plugin's classloader may recognise that the dependency class instance is a different one than the one it knows about and will therefore throw the LinkageError.

For example, let's assume the following scenario:

-   Plugin A bundles its own copy of `commons-fileupload`, but does not export or import any of its packages
-   The host application, Bamboo, has its own copy of `commons-fileupload`.
-   Plugin A also provides a filter that uses `commons-fileupload`, and the filter is set to be run before dispatch.
-   The application, Bamboo, has a WebWork filter that wraps the request with its version of `commons-fileupload`.

When plugin A's filter is executed, its classloader will notice that the request has been wrapped with classes with the same name as its `commons-fileupload` but with different instances. Plugin A's classloader will then throw a LinkageError.

### Resolution

The quick solution is to not bundle any third-party JARs in your plugin. However, if you need to do so, ensure that the packages are exported and imported via your OSGi manifest to ensure your plugin will bind to the packages provided by the host application, if available. This technique is not foolproof, since your exported packages could be slightly newer than the ones provided by the host application, and therefore OSGi will bind you to your own packages instead of the host application's packages. If you are sure that the host application or another plugin does not already provide your dependency, or that there is no chance of your plugin interacting with objects that reference a different version of your dependency, then you can privately bundle dependencies.

### More Information

-   <a href="http://bugs.sun.com/bugdatabase/view_bug.do?bug_id=4972409" class="external-link">Sun Developer Network bug ID 4972409</a> -- the evaluation contains valuable information about the cause of LinkageErrors
-   [Accessing Classes from Another Plugin](/server/framework/atlassian-sdk/accessing-classes-from-another-plugin)

### Applies To

This troubleshooting tip applies to OSGi (version 2) plugins and possibly dynamic legacy Confluence plugins.
