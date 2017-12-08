---
aliases:
- /server/framework/atlassian-sdk/plugin-descriptor-xml-schema-2818613.html
- /server/framework/atlassian-sdk/plugin-descriptor-xml-schema-2818613.md
category: devguide
confluence_id: 2818613
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818613
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818613
date: '2017-12-08'
legacy_title: Plugin Descriptor XML Schema
platform: server
product: atlassian-sdk
subcategory: other
title: Plugin descriptor XML Schema
---
# Plugin descriptor XML Schema

{{% warning %}}

This page is currently atlassian-staff only until either the ~~underlying plugin system bug is fixed~~ XSD can be generated automatically (it's out of date) or a commitment is made to be manually maintained.

{{% /warning %}}

XML Schema is a W3C-recommended XML dialect for declaring and validating the structure--not just the syntax--of an XML document type. The Maven POMs in your existing plugins are XML files constrained by a schema; the same benefit is now available for the plugin descriptor file, `atlassian-plugin.xml`.

The schema for the plugin descriptor document is available at: <a href="https://bitbucket.org/atlassian/atlassian-xsd/" class="external-link"></a>

<a href="https://bitbucket.org/atlassian/atlassian-xsd/" class="uri external-link">https://bitbucket.org/atlassian/atlassian-xsd/</a>

## Features

Schemas bring several benefits, but there are three essential ones: validation, autocompletion and documentation.

{{% note %}}

Currently supported products

JIRA 4.3+, Confluence 3.5+, Refapp 2.9+.

{{% /note %}}

### Validation

Plugin modules have different data schematics. Some require values for every configurable element. Many plugins require some values but not all, and some plugins don't require any configuration. The schemas are aware of this and will check that you have provided required information.

### Autocompletion/Documentation

Many IDEs are smart enough to use their code suggestion features with schemas. XML-specific editors like <a href="http://www.oxygenxml.com" class="external-link">OxygenXML</a> do this, as well as the major Java IDEs. In addition, the schemas contain embedded documentation. The documentation explains which plugin module corresponds to the XML tag, what its acceptable parameters are, what's required and what's not, and so on. The documentation text comes from the plugin module pages on the development hubs for each supported product (see Confluence, JIRA, and the plugin framework).

Here's how the autocomplete looks in <a href="http://eclipse.org" class="external-link">Eclipse</a> with embedded documentation:

![](/server/framework/atlassian-sdk/images/eclipse-autocomplete.png)

And here's how it looks in <a href="http://jetbrains.com/intellij" class="external-link">Intellij IDEA</a>:

![](/server/framework/atlassian-sdk/images/idea-autocomplete.png)

{{% tip %}}

Documentation window in IDEA

You may need to press **Ctrl-Q** to get the documentation popup window to display.

{{% /tip %}}

## Schemas in new plugins

For currently supported products, all plugins created with atlas-create-&lt;product&gt;-plugin as of SDK version 3.3.1 will automatically include the correct schema declarations. No other work on your part is necessary.

## Schemas in existing plugins

To add schemas to your existing plugins, you need to add the validation syntax yourself.

-   Open your `atlassian-plugin.xml` file in your editor
-   Locate the root element, which should look like:

    ``` xml
    <atlassian-plugin key="your.plugin.key" name="Plugin Name" plugins-version="2">
    ```

-   Add the following attributes inside the root element:

    ``` xml
    <atlassian-plugin key="your.plugin.key" name="Plugin Name" plugins-version="2"
        xmlns="http://www.atlassian.com/schema/plugins"
        xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
        xsi:schemaLocation="http://www.atlassian.com/schema/plugins http://schema.atlassian.com/productName/productName-productVersion.xsd">
    ```

    where `productName` and `productVersion` correspond to the Atlassian product you're using. Only major revisions are necessary, so JIRA 4.3.2 would use only 4.3.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>JIRA</p></th>
<th><p>Confluence</p></th>
<th><p>Refapp</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>jira-4.3</p></td>
<td><p>confluence-3.5</p></td>
<td><p>refapp-2.9</p></td>
</tr>
</tbody>
</table>

## Known issues

Schemas enforce an order on elements that doesn't always correspond to `atlassian-plugin.xml`. As far as the product is concerned, any element and attribute ordering is allowable. For example, all modules take a `<description>` element that provides a human-readable description of the module's purpose. The schemas require that this element come first, but the plugin will still work properly regardless. Feel free to ignore validation warnings about out-of-order elements if you wish.

## Reporting problems

We've made every reasonable effort to ensure that the schemas work properly. If you do find something you can't explain and that should work properly, please email developer-relations@atlassian.com.



















































