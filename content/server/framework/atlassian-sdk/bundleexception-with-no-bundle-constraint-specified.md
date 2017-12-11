---
aliases:
- /server/framework/atlassian-sdk/bundleexception-with-no-bundle-constraint-specified-851974.html
- /server/framework/atlassian-sdk/bundleexception-with-no-bundle-constraint-specified-851974.md
category: devguide
confluence_id: 851974
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851974
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851974
date: '2017-12-11'
legacy_title: BundleException with no bundle constraint specified
platform: server
product: atlassian-sdk
subcategory: faq
title: BundleException with no bundle constraint specified
---
# BundleException with no bundle constraint specified

### Symptoms -- What Goes Wrong

A plugin fails to load at runtime, and the log contains an `OsgiContainerException` with a `BundleException` as its root cause. For example:

``` bash
WARNING: Unable to enable plugin 'com.atlassian.myplugin.my-plugin'
com.atlassian.plugin.osgi.container.OsgiContainerException: Cannot start plugin: com.atlassian.myplugin.my-plugin
       at com.atlassian.plugin.osgi.factory.OsgiPlugin.enableInternal(OsgiPlugin.java:385)
       at com.atlassian.plugin.impl.AbstractPlugin.enable(AbstractPlugin.java:212)
       ...
Caused by: org.osgi.framework.BundleException: Unable to resolve due to constraint violation.
       at org.apache.felix.framework.Felix._resolveBundle(Felix.java:1732)
       at org.apache.felix.framework.Felix._startBundle(Felix.java:1588)
       at org.apache.felix.framework.Felix.startBundle(Felix.java:1541)
       at org.apache.felix.framework.BundleImpl.start(BundleImpl.java:371)
```

### Cause

If your plugin is failing to enable with the message "**Unable to resolve due to constraint violation.**" but doesn't specify a particular package or what the constraint violation is, it's possible that the exporter of a package that you are importing is imposing a `uses` constraint directive that your plugin is not satisfying. You may need to add a &lt;Package-Import&gt; to your own plugin to satisfy this directive.

### Resolution

At the moment, determining which bundle imposes a `uses` constraint is primarily guesswork. You will need to look through the `META-INF/manifest.mf` files of bundles from which you are importing packages looking for `uses` directives in the `Export-Package:` section.

For example:

``` bash
Manifest-Version: 1.0
Export-Package: com.pyxis.greenhopper;uses:="javax.xml.bind.annotation";version:="4.3.1"
Import-Package: javax.xml.bind.annotation;version="2.1.0"
```

The `uses:="javax.xml.bind.annotation"` implies that plugins importing both `com.pyxis.greenhopper` and `javax.xml.bind.annotation` *must* import version "2.1.0" of `javax.xml.bind.annotation`. This can be achieved by adding the relevant `<Package-Import>` to your `pom.xml`:

``` xml
<build>
<plugins>
  <plugin>
    <groupId>org.apache.felix</groupId>
    <artifactId>maven-bundle-plugin</artifactId>
    <extensions>true</extensions>
    <configuration>
      <instructions>        
        <Import-Package>          
          javax.xml.bind*;version="2.1.0", <!-- note the specified version String -->
          *
        </Import-Package>        
        <Spring-Context>*;timeout:=60</Spring-Context>
      </instructions>
    </configuration>
  </plugin>
</plugins>
</build>
```

### More Information

See also <a href="http://olegz.wordpress.com/documents-and-articles/osgi-uses/" class="external-link">understanding the OSGi <em>uses</em> directive</a>

































































































































































































































