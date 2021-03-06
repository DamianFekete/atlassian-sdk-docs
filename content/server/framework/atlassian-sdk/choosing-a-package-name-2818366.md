---
title: Choosing a Package Name 2818366
aliases:
    - /server/framework/atlassian-sdk/choosing-a-package-name-2818366.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818366
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818366
confluence_id: 2818366
platform:
product:
category:
subcategory:
---
# Documentation : Choosing a Package Name

Make sure your package names are unique. You can choose any package name, provided that it does not conflict with any existing package used in the Atlassian application you are developing for, or in any other plugins. Do **not** use `com.atlassian.confluence.plugins.*`. That is confusing to people who try to use the plugin. **Use a real package name** that corresponds to your organisation or project. For example: `org.mycompany.confluence.plugins.*`. The <a href="http://java.sun.com/docs/books/jls/second_edition/html/packages.doc.html#40169" class="external-link">Sun Java documentation</a> has some tips about conventions used to ensure unique package names.
