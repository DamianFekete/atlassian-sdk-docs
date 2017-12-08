---
aliases:
- /server/framework/atlassian-sdk/running-on-websphere-6.1-852007.html
- /server/framework/atlassian-sdk/running-on-websphere-6.1-852007.md
category: devguide
confluence_id: 852007
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852007
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852007
date: '2017-12-08'
legacy_title: Running on WebSphere 6.1
platform: server
product: atlassian-sdk
subcategory: faq
title: Running on WebSphere 6.1
---
# Running on WebSphere 6.1

{{% warning %}}

WebSphere is not a supported platform

Atlassian support does not cover WebSphere. The information below is provided as is, in the hope that it is useful. If you have any input that may be helpful to others, please add comments to the page.

{{% /warning %}}

<a href="http://www-01.ibm.com/software/webservers/appserv/was/" class="external-link">WebSphere</a> 6.1 has a few issues when running applications that use the Atlassian Plugin Framework:

-   WebSphere itself is built on OSGi, but it uses an older version of the specification (4.0) whereas the plugin framework expects 4.1.
-   The WebSphere classloader does not support classloader scanning, a technique used by the plugin framework to discover which packages are available from the host application. Specifically, the classloader does not return results when looking for packages or directories. This capability is required for most scanning techniques.

The solution is to **configure your WebSphere application** with the following settings:

1.  Application classloader policy -- `SINGLE`
2.  Application classloader mode -- `child-first`

By setting the classloader to `child-first` and `SINGLE`, you ensure that the WebSphere OSGi classes do not override the classes needed by the Atlassian Plugin Framework.

The Atlassian Plugin Framework works around the classpath scanning issue, by scanning your JARs in `WEB-INF/lib` and your classes in `WEB-INF/classes` instead. This means that common libraries stored in the application server will not be recognised.

For more information see the <a href="http://publib.boulder.ibm.com/infocenter/iseries/v5r4/index.jsp?topic=/rzatz/51/program/clsadmcns.htm" class="external-link">WebSphere documentation</a>.













































































