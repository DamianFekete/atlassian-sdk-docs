---
aliases:
- /server/framework/atlassian-sdk/classnotfoundexception-851975.html
- /server/framework/atlassian-sdk/classnotfoundexception-851975.md
category: devguide
confluence_id: 851975
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851975
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851975
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/troubleshooting/classnotfoundexception
new_url: /server/framework/atlassian-sdk/classnotfoundexception
platform: server
product: atlassian-sdk
subcategory: other
title: ClassNotFoundException
---
# ClassNotFoundException

### Symptoms -- What Goes Wrong

During plugin development, you encounter a `java.lang.ClassNotFoundException`.

### Cause

The exceptions are caused by the way classloaders work for plugins. With OSGi, every plugin needs to explicitly import every package it needs, otherwise the plugin's classloader will not have access to the package and will throw this exception.

If you do not specify your own package imports, the plugin framework 'guesses' which ones you need by scanning the class files in your plugin. Your plugin `.jar` file is transformed at startup and placed in the directory `<jira_home>/plugins/.osgi-plugins/transformed-plugins`. The `META-INF/MANIFEST.MF` file in that transformed jar (not the original jar file) is where the package imports are ultimately specified using the header `Import-Package` like this:

``` javascript
Import-Package: com.atlassian.confluence,com.atlassian.confluence.pages,org.apache.velocity
```

or for a more complex plugin:

``` javascript
Import-Package: com.atlassian.core.util.collection;resolution:="option
 al",com.atlassian.jira.config.properties;version="[4.0.1,4.0.1]",com.
 atlassian.jira.issue.fields.option;resolution:="optional",com.atlassi
 an.jira.web.action;resolution:="optional",com.atlassian.plugin.osgi.b
 ridge.external,javax.servlet.http;resolution:="optional",org.apache.l
 og4j;resolution:="optional",webwork.action;resolution:="optional"
```

Note that there is a line length restriction in jar files.

This header comes from the OSGi manifest specification, which defines extra headers that it needs to connect the JAR to other JARs or bundles. If you are familiar with OSGi, you can generate your own `Package-Import` header, along with the other required headers. But most plugin developers will want the framework to handle that for them.

This technique works quite well for most simple plugins, but the more complex the plugin the greater chance of missing a required package.

### Resolution

In short, add an explicit `<Import-Package>` element to the `plugin-info` element in `atlassian-plugin.xml`.

The longer explanation is that the Atlassian Plugin Framework tries to determine which packages your plugin needs in order to generate the OSGi manifest headers for you. If this does not work, you likely need to customise the instruction used to scan your plugin.

You can do this by using the `<bundle-instructions>` element in the `<plugin-info`&gt; element in your plugin's `atlassian-plugin.xml` (not the `pom.xml`).See [Configuring the Plugin Descriptor](/server/framework/atlassian-sdk/configuring-the-plugin-descriptor).

In this example `atlassian-plugin.xml` we force the scanning to include the `com.mylibrary` package, in addition to its usual scanning:

``` javascript
<atlassian-plugin ...>
  <plugin-info>
    <description>${project.description}</description>
    <version>${project.version}</version>
    <bundle-instructions>
      <Import-Package>com.mylibrary,*;resolution:=optional</Import-Package>
    </bundle-instructions>
  </plugin-info>
  ...
</plugin>
```

### More Information

Be sure to mark packages as [optional imports](/server/framework/atlassian-sdk/marking-packages-as-optional-imports) where applicable.

##### RELATED TOPICS

[Marking Packages as Optional Imports](/server/framework/atlassian-sdk/marking-packages-as-optional-imports)
























