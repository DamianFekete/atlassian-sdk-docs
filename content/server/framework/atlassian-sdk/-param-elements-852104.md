---
title: Param Elements 852104
aliases:
    - /server/framework/atlassian-sdk/-param-elements-852104.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852104
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852104
confluence_id: 852104
platform:
product:
category:
subcategory:
---
# Documentation : \_Param Elements

Param elements represent a map of key/value pairs, where each entry corresponds to the param elements attribute: `name` and `value` respectively.

``` xml
<param name="key" value="value" />
```

The value can be retrieved from within the Velocity view with the following code, where $item is a `WebItemModuleDescriptor`:

``` xml
$item.webParams.get("key") <!-- retrieve the value -->
$item.webParams.getRenderedParam("key", $user, $helper) <!-- retrieve the Velocity rendered value -->
```

If the `value` attribute is not specified, the value will be set to the body of the element. I.e. the following two param elements are equivalent:

``` xml
<param name="isPopupLink" value="true" />
<param name="isPopupLink">true</param>
```
















































































































































































































































































































