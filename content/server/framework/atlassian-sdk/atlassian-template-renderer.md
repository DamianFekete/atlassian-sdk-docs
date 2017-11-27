---
aliases:
- /server/framework/atlassian-sdk/atlassian-template-renderer-5669100.html
- /server/framework/atlassian-sdk/atlassian-template-renderer-5669100.md
category: devguide
confluence_id: 5669100
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669100
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669100
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/atlassian-template-renderer
new_url: /server/framework/atlassian-sdk/atlassian-template-renderer
platform: server
product: atlassian-sdk
subcategory: learning
title: Atlassian Template Renderer
---
# Atlassian Template Renderer

Use the Atlassian Template Renderer (ATR) to render your textual content. ATR is a library that provides an abstraction on top of various template engines, making it easier to use the template engines. For example, instead of having to create a VelocityEngine object and configure it, we provide a factory to do that for you. See the <a href="http://docs.atlassian.com/atlassian-template-renderer-api/" class="external-link">Javadoc</a> for reference information.

The following sections describe how to use the ATR.

## The simple case

In your atlassian-plugin.xml file, specify the `component-import` module as follows:

``` javascript
    <component-import key="velocity-renderer" interface="com.atlassian.templaterenderer.TemplateRenderer" />
```

Now just setup the `TemplateRenderer` component for injection into your component.

When you need to render a template, call the `renderer.render(String templateName, Writer writer)` or `renderer.render(String templateName, Map<String, Object> context, Writer writer)` method.

### A bit more sugar

Let's say you want one of the other components injected into **each** of the template contexts for you to use. You could make sure to have that component injected anywhere you do some rendering and then creating a context map with the component in it. But there's an easier way. Specify the component as a [`template-context-item`](/server/framework/atlassian-sdk/template-context-item-plugin-module).

``` javascript
<template-context-item key="rendererHelperContextItem" component-ref="rendererHelper"
    context-key="helper" name="Renderer Helper Context Item"/>
```

Using this technique, the ATR plugin makes the SAL [I18nResolver](/server/framework/atlassian-sdk/sal-services#%7B%7B%7B%7D-i18n-resolver%7B%7D%7D%7D) and the plugins <a href="http://docs.atlassian.com/atlassian-plugins-webresource/2.2.0/atlassian-plugins-webresource/apidocs/com/atlassian/plugin/webresource/WebResourceManager.html" class="external-link">WebResourceManager</a> automatically available to all templates in this way with the `i18n` and `webResourceManager` context keys.
































































































































































































































































