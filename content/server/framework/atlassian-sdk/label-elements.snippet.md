---
aliases:
- /server/framework/atlassian-sdk/-label-elements-852103.html
- /server/framework/atlassian-sdk/-label-elements-852103.md
category: devguide
confluence_id: 852103
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852103
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852103
date: '2017-12-08'
legacy_title: _Label Elements
platform: server
product: atlassian-sdk
subcategory: other
title: _Label Elements
---
# \_Label Elements

Label elements may contain optional parameters, as shown below:

``` xml
<label key="common.concepts.create.new.issue">
    <param name="param0">$helper.project.name</param>
</label>
```

-   The parameters allow you to insert values into the label using Java's <a href="http://java.sun.com/j2se/1.4.2/docs/api/java/text/MessageFormat.html" class="external-link">MessageFormat</a> syntax.
-   Parameter names must start with `param` and will be mapped in *alphabetical order* to the substitutions in the format string. I.e. param0 is {0}, param1 is {1}, param2 is {2}, etc.
-   Parameter values are rendered using Velocity, allowing you to include dynamic content.
