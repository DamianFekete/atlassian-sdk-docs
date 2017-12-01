---
aliases:
- /server/framework/atlassian-sdk/plugin-modules-that-cannot-be-disabled-852018.html
- /server/framework/atlassian-sdk/plugin-modules-that-cannot-be-disabled-852018.md
category: devguide
confluence_id: 852018
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852018
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852018
legacy_url: https://developer.atlassian.com/docs/faq/plugin-framework-faq/plugin-modules-that-cannot-be-disabled
new_url: /server/framework/atlassian-sdk/plugin-modules-that-cannot-be-disabled
platform: server
product: atlassian-sdk
subcategory: other
title: Plugin modules that cannot be disabled
---
# Plugin modules that cannot be disabled

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p><a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852001">Atlassian Plugin Framework 2.5</a> and later.</p></td>
</tr>
</tbody>
</table>

 

Plugin modules marked with the `@CannotDisable` annotation cannot be disabled dynamically unless the entire plugin is disabled. The `@CannotDisable` annotation is inherited, so any custom `ModuleDescriptor` that subclasses `ModuleDescriptor` types annotated with `@CannotDisable` also cannot be disabled. In [Atlassian Plugin Framework 2.5](https://developer.atlassian.com/pages/viewpage.action?pageId=852001) and later, [component](/server/framework/atlassian-sdk/component-plugin-module) and [component import](/server/framework/atlassian-sdk/component-import-plugin-module) modules and their subclasses cannot be disabled.















































































