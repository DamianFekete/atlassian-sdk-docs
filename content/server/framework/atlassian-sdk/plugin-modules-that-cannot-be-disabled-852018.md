---
title: Plugin Modules That Cannot Be Disabled 852018
aliases:
    - /server/framework/atlassian-sdk/plugin-modules-that-cannot-be-disabled-852018.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852018
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852018
confluence_id: 852018
platform:
product:
category:
subcategory:
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

 

Plugin modules marked with the `@CannotDisable` annotation cannot be disabled dynamically unless the entire plugin is disabled. The `@CannotDisable` annotation is inherited, so any custom `ModuleDescriptor` that subclasses `ModuleDescriptor` types annotated with `@CannotDisable` also cannot be disabled. In [Atlassian Plugin Framework 2.5](https://developer.atlassian.com/pages/viewpage.action?pageId=852001) and later, [component](/server/framework/atlassian-sdk/component-plugin-module-852118.html) and [component import](/server/framework/atlassian-sdk/component-import-plugin-module-852117.html) modules and their subclasses cannot be disabled.

























