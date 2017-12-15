---
aliases:
- /server/framework/atlassian-sdk/configuration-of-instructions-in-atlassian-plugins-38449742.html
- /server/framework/atlassian-sdk/configuration-of-instructions-in-atlassian-plugins-38449742.md
category: devguide
confluence_id: 38449742
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=38449742
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=38449742
date: '2017-12-08'
guides: guides
legacy_title: Configuration of Instructions in Atlassian Plugins
platform: server
product: atlassian-sdk
subcategory: learning
title: Configuration of Instructions in Atlassian Plugins
---
# Configuration of Instructions in Atlassian Plugins

## Default plugin instructions

If you create a new plugin with the Atlassian SDK (for instance using `atlas-create-confluence-plugin`), you'll find the following instructions already configured for you:

``` xml
<instructions>
  <Atlassian-Plugin-Key>${atlassian.plugin.key}</Atlassian-Plugin-Key>
  <!-- Add package to export here -->
  <Export-Package>
    com.mycompany.api,
  </Export-Package>
  <!-- Add package import here -->
  <Import-Package>
    org.springframework.osgi.*;resolution:="optional", org.eclipse.gemini.blueprint.*;resolution:="optional", *
  </Import-Package>
  <!-- Ensure plugin is spring powered -->
  <Spring-Context>*</Spring-Context>
</instructions>
```

Here's what these default instructions do:

<table>
<colgroup>
<col style="width: 12%" />
<col style="width: 12%" />
<col style="width: 76%" />
</colgroup>
<thead>
<tr class="header">
<th>Tag</th>
<th>Default Value</th>
<th>Purpose</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Atlassian-Plugin-Key</td>
<td>Maven group and artifact</td>
<td>Marks your plugin as providing its own Spring configuration, rather than one being created during the transformation process. This is so-called 'transformerless', and results in significantly faster deployment and startup time of your plugin.</td>
</tr>
<tr class="even">
<td>Export-Package</td>
<td>Your API package</td>
<td>Tells the underlying OSGi framework to expose these classes outside your plugin. Without it, you would get <code>ClassNotFoundExceptions</code> when other plugins attempted to load your API classes.</td>
</tr>
<tr class="odd">
<td>Import-Package</td>
<td><p>Optional backend frameworks</p>
<p>Catch-all wildcard</p></td>
<td><p>In order to provide Spring functionality in an OSGi container, we use a third party framework. Originally this was Spring DM, but in the latest Atlassian Plugins version we migrated to its successor, Gemini Blueprints. Marking both as 'optional' means your plugin can find the classes it needs it both new and old Atlassian products. The final asterisk is a catch-all to ensure your plugin can access all the classes it needs, and is resolved at build time by utility called '<a href="https://github.com/bndtools/bnd" class="external-link">bnd</a>'.</p>
<p>If you remove the optional imports, <code style="background-color: transparent;">bnd</code> would instead generate mandatory imports for both Spring OSGi frameworks, meaning your plugin would fail to resolve and start in both newer and older products.</p></td>
</tr>
<tr class="even">
<td>Spring-Context</td>
<td>Catch-all wildcard</td>
<td>This is simply a safety measure to ensure your Spring context is loaded, even if there are no XML files in your <code>META-INF/spring</code> directory.</td>
</tr>
</tbody>
</table>

## References

-   <a href="http://www.eclipse.org/gemini/blueprint/documentation/reference/1.0.2.RELEASE/html/app-deploy.html" class="external-link">Spring OSGi bundles in Blueprints</a>
-   <a href="https://bitbucket.org/atlassian/atlassian-spring-scanner/src" class="external-link">Spring Scanner</a>
-   <a href="https://www.youtube.com/watch?v=bEYoAFc42b4" class="external-link">Plugins 2</a>
