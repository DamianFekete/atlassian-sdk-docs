---
title: Velocity in Osgi 851989
aliases:
    - /server/framework/atlassian-sdk/velocity-in-osgi-851989.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851989
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851989
confluence_id: 851989
platform:
product:
category:
subcategory:
---
# Velocity in OSGi

### Symptoms -- What Goes Wrong

When developing with <a href="http://velocity.apache.org/engine/index.html" class="external-link">Velocity</a> in OSGi, you see some errors in the logs:

``` bash
- *** Class 'org.apache.velocity.runtime.directive.Literal' was not found because bundle 15 does not import
'org.apache.velocity.runtime.directive' even though bundle 10 does export it. To resolve this issue, add an import for
'org.apache.velocity.runtime.directive' to bundle 15. ***
```

### Cause

Velocity likes to use reflection to load a few classes. This means anything that generates your OSGi imports automatically will not pick up these classes. This includes the case when you let the Atlassian Plugin Framework generate your OSGi manifest for you.

This may not actually hurt your application, probably because after trying the context classloader, Velocity will try the classloader that originally loaded it, and hence find the libraries. Nevertheless, you may see the above errors in the logs.

### Resolution

To fix this, you will need to manually import the packages these classes are in. If using the Maven Bundle Plugin, add this line to the `<Instructions>`:

``` xml
<Import-Package>org.apache.velocity.runtime,org.apache.velocity.runtime.directive,org.apache.velocity.runtime.resource,org.apache.velocity.util.introspection,*</Import-Package>
```





















































































































































































































































