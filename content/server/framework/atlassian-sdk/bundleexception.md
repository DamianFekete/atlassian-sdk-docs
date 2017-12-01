---
aliases:
- /server/framework/atlassian-sdk/bundleexception-852121.html
- /server/framework/atlassian-sdk/bundleexception-852121.md
category: devguide
confluence_id: 852121
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852121
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852121
legacy_url: https://developer.atlassian.com/docs/faq/troubleshooting/bundleexception
new_url: /server/framework/atlassian-sdk/bundleexception
platform: server
product: atlassian-sdk
subcategory: faq
title: BundleException
---
# BundleException

### Symptoms -- What Goes Wrong

A plugin fails to load at runtime, and the log contains an `OsgiContainerException` with a `BundleException` as its root cause. For example:

``` bash
2009-10-13 14:23:09,656 [ACTIVE] ExecuteThread: '0' for queue: 'weblogic.kernel.Default (self-tuning)' WARN     [plugin.osgi.factory.OsgiPlugin] Unable to enable plugin 'com.atlassian.gadgets.renderer'
com.atlassian.plugin.osgi.container.OsgiContainerException: Cannot start plugin: com.atlassian.gadgets.renderer
    at com.atlassian.plugin.osgi.factory.OsgiPlugin.enableInternal(OsgiPlugin.java:385)
        ...
Caused by: org.osgi.framework.BundleException: Unresolved constraint in bundle 28: package; (&(package=org.apache.xml.serialize)(version>=2.9.1)(!(version>=3.0.0)))
```

### Cause

When your plugin declares a package import, at runtime it must find another OSGi bundle that exports a compatible version (according to the specified version constraints) of the same package. If such a bundle can't be found, the plugin will fail to load.

### Resolution

First, verify that another bundle does export the package. If you're using the SDK, one way to do this is to look at the Felix web console (available at `plugins/servlet/system/console`), which allows you to explore the bundles available in the system. If another bundle does export the package, verify that the version constraints (shown in the error log) are met by the bundle. If no bundle exports the package, you may need to provide it by packaging it within your plugin and removing the package import.








































































