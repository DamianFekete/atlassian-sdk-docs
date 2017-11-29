---
aliases:
- /server/framework/atlassian-sdk/best-practices-2818374.html
- /server/framework/atlassian-sdk/best-practices-2818374.md
category: devguide
confluence_id: 2818374
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818374
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818374
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/best-practices
new_url: /server/framework/atlassian-sdk/best-practices
platform: server
product: atlassian-sdk
subcategory: learning
title: Best Practices
---
# Best Practices

 

## Use your own package name

Make sure your package names are unique. You can choose any package name, provided that it does not conflict with any existing package used in the Atlassian application you are developing for, or in any other plugins. Do **not** use `com.atlassian.confluence.plugins.*`. That is confusing to people who try to use the plugin. **Use a real package name** that corresponds to your organisation or project. For example: `org.mycompany.confluence.plugins.*`. The <a href="http://java.sun.com/docs/books/jls/second_edition/html/packages.doc.html#40169" class="external-link">Sun Java documentation</a> has some tips about conventions used to ensure unique package names.

## Namespace your CSS and Javascript

We can't promise that our products CSS and Javascript isn't going to change from version to version. For that reason, you are generally best off writing CSS and Javascript that does not depend on the products' at all. One of the best ways to do this is namespace your CSS and Javascript.

In the CSS realm, there is an <a href="http://www.w3.org/TR/css3-namespace/" class="external-link">official namespace proposal</a>, but that's not what I'm talking about as the current browser crop doesn't support these enhancements yet. All I'm really talking about is intelligently naming your selectors so that you don't bleed styles between your plugin and the product itself. For example, rather than having an element like:

``` xml
<table class="table">...</table>
```

you might try

``` xml
<table class="MyPluginName_table">...</table>
```

That will ensure that your CSS rules don't get applied to anyone else's plugins, and you don't inadvertently pick up a style from Confluence's table class that may change in the future.

On the Javascript side, you run an even greater risk of conflicting with the product or with another plugin. For that reason, you should namespace your javascript as outlined in <a href="http://icant.co.uk/articles/seven-rules-of-unobtrusive-javascript/#r6" class="external-link">this tutorial</a>. Our products don't actually follow this rule yet, so it's doubly important for plugins to do so.





















































































































