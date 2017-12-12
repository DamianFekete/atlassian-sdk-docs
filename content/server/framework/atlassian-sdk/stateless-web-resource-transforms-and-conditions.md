---
aliases:
- /server/framework/atlassian-sdk/stateless-web-resource-transforms-and-conditions-28313151.html
- /server/framework/atlassian-sdk/stateless-web-resource-transforms-and-conditions-28313151.md
category: devguide
confluence_id: 28313151
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=28313151
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=28313151
date: '2017-12-08'
guides: guides
legacy_title: Stateless web-resource transforms and conditions
platform: server
product: atlassian-sdk
subcategory: learning
title: Stateless web-resource transforms and conditions
---
# Stateless web-resource transforms and conditions

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p>Atlassian Plugin Framework 3.0 and later.</p></td>
</tr>
</tbody>
</table>

JIRA and Confluence are moving to a 'stateless' delivery of JavaScript and CSS resources. Beginning with JIRA 7 and Confluence 6,** transforms and conditions should not assume that they have access to the cookie or current user** when serving CSS or JavaScript resources.

To achieve this, we have created new APIs for web-resource transforms and conditions. This page describes how to update your transforms and conditions to these new APIs.

 

## The core problem

Delivering web-resource batches (CSS + JavaScript) to a page is a two-stage process:

1.  **page-render-time**: when rendering the HTML page, calculate and render the URLs for CSS `<link>` and JavaScript `<script>` tags.
2.  **resource-serve-time:** when serving those CSS + JavaScript resources, calculate the required resources in those batches and send them to the client.

At resource-serve-time, we process web-resource conditions and transforms. Previously, these conditions and transforms have had access to the user's cookie -- for example, the i18n transform (that renders internationalised strings in JavaScript resources) can look at the cookie on the incoming request and determine that user's locale.

Under the new APIs, **all the information required by the transformer or condition must be encoded in the URL**. Do not assume that you will have a current user at resource-serve-time. To achieve this, we have deprecated the old web-resource transform and condition APIs and created new APIs:

-   for transforms, `com.atlassian.plugin.webresource.transformer.WebResourceTransformer` has been deprecated in favour of `com.atlassian.plugin.webresource.transformer.WebResourceTransformerFactory`.
-   for conditions, the use of `com.atlassian.plugin.web.Condition` in web-resources has been deprecated in favour of `com.atlassian.plugin.webresource.condition.UrlReadingCondition`. (Note that the Condition class itself is not deprecated, as it is still relevant for web-fragments as opposed to web-resources.)

These APIs appear in `atlassian-plugins-webresources `version 3.0.

## How do I fix offending transforms?

There are two cases to fix here:

### Transforms that do compilation

Examples include LESS and i18n transformation.

To fix these, convert from `WebResourceTransformer` to <a href="https://bitbucket.org/atlassian/atlassian-plugins-webresource/src/10b622b03d78cf858c78bbafb69353100cef41b6/atlassian-plugins-webresource/src/main/java/com/atlassian/plugin/webresource/transformer/WebResourceTransformerFactory.java?at=master" class="external-link">WebResourceTransformerFactory </a>(which produces `UrlReadingWebResourceTransformers`). This enables you to contribute to the URL at page-render-time and read from that URL at resource-serve-time.

Taking the i18n transform as an example:

-   the old i18n transform reads the user's locale at resource-serve-time
-   the new i18n transform
    -   <a href="https://bitbucket.org/atlassian/atlassian-plugins-webresource/commits/f785b45696b81ab056efc860a36a03e9e192dce3?at=issue/PLUGWEB-99-add-i18n-transform#Latlassian-plugins-webresource-plugin/src/main/java/com/atlassian/webresource/plugin/i18n/JsI18nTransformer.javaT63" class="external-link">add the user's locale to the resource URL's querystring</a> at page-render-time
    -   reads the locale from the querystring at resource-serve-time

Note that fixing the transform can be hard, as it may not be the transform class that is actually doing the cookie lookup; it may be something deeper in the dependency-injection hierarchy. For this reason, it is better to convert to the data API if possible (see below).

### Transforms that do variable injection

For a long time, there was no good way of inserting JSON data into a page. One solution people used was to use transforms to inject data into JavaScript as it is being served -- for example, the ContextPathTransformer. Now, there is a much better way -- deliver JSON data via the [Stateless web-resource transforms and conditions](/server/framework/atlassian-sdk/stateless-web-resource-transforms-and-conditions).

To see this in action, see the new ContextPathProvider. This consists of three parts:

-   the <a href="https://bitbucket.org/atlassian/atlassian-plugins-webresource/src/f785b45696b81ab056efc860a36a03e9e192dce3/atlassian-plugins-webresource-plugin/src/main/java/com/atlassian/webresource/plugin/data/ContextPathProvider.java?at=issue%2FPLUGWEB-99-add-i18n-transform" class="external-link">ContextPathProvider</a> implementation, that returns the JSON data,
-   a <a href="https://bitbucket.org/atlassian/atlassian-plugins-webresource/src/f785b45696b81ab056efc860a36a03e9e192dce3/atlassian-plugins-webresource-plugin/src/main/resources/atlassian-plugin.xml?at=issue%2FPLUGWEB-99-add-i18n-transform#cl-14" class="external-link">web-resource declaration</a> that puts this data provider in a context, and
-   some <a href="https://bitbucket.org/atlassian/atlassian-plugins-webresource/src/f785b45696b81ab056efc860a36a03e9e192dce3/atlassian-plugins-webresource-plugin/src/main/resources/js/data/context-path.js?at=issue%2FPLUGWEB-99-add-i18n-transform" class="external-link">JavaScript</a> to wrap the data.

## How do I fix offending conditions?

When looking at conditions, the first thing to consider is:

> *Do you really need a condition here? What would be the cost of delivering the JavaScript / CSS resource? It makes little difference to performance if we serve a 1 or 2 extra KB.*

 

If you do need to convert it, the most common solution is to convert your conditions to a <a href="https://bitbucket.org/atlassian/atlassian-plugins-webresource/src/f785b45696b81ab056efc860a36a03e9e192dce3/atlassian-plugins-webresource/src/main/java/com/atlassian/plugin/webresource/condition/UrlReadingCondition.java?at=issue%2FPLUGWEB-99-add-i18n-transform" class="external-link">UrlReadingCondition</a>.

Note one potential issue:

-   UrlReadingConditions are **included in the batch**. This fixes a long-standing bug where resources with conditions are delivered as separate resources, breaking web-resource dependency order (and making dependency different between dev and prod mode). However, there is a strong chance that your code (especially CSS) was written knowing that this bug existed. You should test to ensure that this change in batch ordering has not affected your plugin.

## Dual compatibility

If your plugin targets products using old versions of webresources but you want to make use of the transform2 / condition2, use the following techniques to be compatible:

### Transforms

Keep your transform1 implementation untouched and add a transform2 declaration with `alias-key` = the key of the transform1.

The transform lookup algorithm for a key `my-key` is as follows:

-   Look for a transform2 with `key = my-key`
-   If not found, look for a transform2 with `alias-key = my-key`
-   If not found, look for a transforms1 with `key = my-key`

``` xml
<!-- in the plugin declaring the transform -->
<web-resource-transformer key="jsI18n" name="JavaScript I18n Transformer" class="com.atlassian.aui.javascript.JsI18nTransformer" />
<url-reading-web-resource-transformer key="jsI18n-2" alias-key="jsI18n" name="JavaScript I18n Transformer" class="com.atlassian.aui.javascript.UrlReadingJsI18nTransformer" />
```

``` xml
<!-- in a plugin using the transform -->
<web-resource key="my-resource">
  <transformation extension="js">
    <transformer key="jsI18n" />
  </transformation>
  ...
```

`In an old product, the <url-reading-web-resource-transformer>` will be ignored.

### Conditions

Add a `class2` attribute to your `<condition>` declaration:

``` xml
<web-resource key="my-resource">
  <condition
    class="com.atlassian.jira.plugin.webfragment.conditions.BooleanSystemPropertyCondition"
    class2="com.atlassian.jira.plugin.webfragment.conditions.UrlReadingBooleanSystemPropertyCondition">
    <param name="property">jira.dev.mode</param>
  </condition>
</web-resource>
```

In an old product, `class2` will be ignored.

In a new product, for a `web-resource` only (ie not a `web-item` / `web-panel` etc), the contract is to look for `class2` if it exists, otherwise use `class`.

Note that `class` can be either a condition1 or a condition2 - in particular if you're implementing something for condition2 only, `class` can be a condition2.

































































































































































































































































































































































