---
aliases:
- /server/framework/atlassian-sdk/marking-packages-as-optional-imports-852102.html
- /server/framework/atlassian-sdk/marking-packages-as-optional-imports-852102.md
category: devguide
confluence_id: 852102
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852102
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852102
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/plugin-framework-faq/marking-packages-as-optional-imports
new_url: /server/framework/atlassian-sdk/marking-packages-as-optional-imports
platform: server
product: atlassian-sdk
subcategory: other
title: Marking packages as optional imports
---
# Marking packages as optional imports

Unless you plan to list every single package your plugin needs, be sure to add the `*;resolution:=optional` value to your list of packages, when including bundle instructions in your plugin `atlassian-plugin.xml` XML.

Example:

``` javascript
<plugin ...>
  <plugin-info>
    <bundle-instructions>
      <Import-Package>com.mylibrary,*;resolution:=optional</Import-Package>
    </bundle-instructions>
  </plugin-info>
  ...
</plugin>
```

The `*;resolution:=optional` value instructs the plugin system to continue to scan your classes for packages, but to resolve all packages optionally. This means if you bundle a library that has code that depends on other libraries you do not need, the resolution will not fail.

If, however, you are sure your code only refers to packages you need, you can omit the `;resolution:=optional` string. The advantage here is that you will be notified on installation if required dependencies are missing.

##### RELATED TOPICS

[Creating your Plugin Descriptor](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Creating+your+Plugin+Descriptor)




































