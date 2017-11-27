---
aliases:
- /server/framework/atlassian-sdk/852130.html
- /server/framework/atlassian-sdk/852130.md
category: devguide
confluence_id: 852130
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852130
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852130
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/plugin-framework-faq/my-public-component-just-disappeared
new_url: /server/framework/atlassian-sdk/my-public-component-just-disappeared
platform: server
product: atlassian-sdk
subcategory: other
title: My public component just disappeared!
---
# My public component just disappeared!

You may notice that in certain situations, a public component on your plugin disappeared. This is because, under the covers, your public component is actually a Spring bean, registered as an OSGi service via Spring Dynamic Modules. Spring DM, by default, will automatically unregister a service if one of its dependencies goes away.

For example, say you registered a DictionaryService as a public component, and it depended on a MessageService. If the MessageService, for whatever reason, is unregistered, the Dictionary Service will be unregistered automatically. The only way to detect this is to turn on trace logging for `org.springframework.osgi.service.dependency.internal` and you will see something like:

    Exporter [dictionaryService] stopped; transitive OSGi dependency [messageService] is unsatifised

This can also happen if there is a circular dependency between two plugins that consume each others services.




































