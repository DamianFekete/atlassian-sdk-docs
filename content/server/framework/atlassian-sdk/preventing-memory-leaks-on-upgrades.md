---
aliases:
- /server/framework/atlassian-sdk/preventing-memory-leaks-on-upgrades-8947251.html
- /server/framework/atlassian-sdk/preventing-memory-leaks-on-upgrades-8947251.md
category: devguide
confluence_id: 8947251
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8947251
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8947251
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/advanced-plugin-development-faq/preventing-memory-leaks-on-upgrades
new_url: /server/framework/atlassian-sdk/preventing-memory-leaks-on-upgrades
platform: server
product: atlassian-sdk
subcategory: other
title: Preventing memory leaks on upgrades
---
# Preventing memory leaks on upgrades

Whether you need to be able to develop quickly via dynamic plugin installation or want to repeatedly upgrade a plugin on a production instance with no downtime, you will need to know how to prevent memory leaks from forcing a restart.

The core issue behind upgrade-related memory leaks is strong references by classes or objects outside your plugin to classes or objects loaded by your plugin. For example, if a Confluence object had a hard reference to one of your classes, whenever your plugin was upgraded, the plugin's classloader couldn't be garbage collected because there would still exist a strong reference to it via the referred object's class. The following are common causes of these types of memory leaks:

### Lingering Event Registrations

The common pattern for listening for events is to get either `PluginEventManager` or `EventPublisher` injected into your component, then call `eventPublisher.register(this)` so that any local methods with the `@PluginEventListener` or `@EventListener` annotation will be called when events are published. However, this introduces a strong reference to your plugin class, as the event publisher sits outside your plugin down in the host application.

The solution is to implement `org.springframework.beans.factory.DisposableBean` and implement `dispose()`. In this method, you should unregister yourself from the event publisher via `eventPublisher.unregister(this)`.

{{% note %}}

This technique only works if the bean is a component. If you try to register yourself to listen for events when your class is simply an implementation of a extension point, such as an `HttpServlet` or `Macro`, Spring won't know about it in order to call `dispose()` on plugin shutdown. In these cases, move all event listening code into a separate component.

{{% /note %}}

### Forgotten Job Registrations

If your plugin has registered any code to be called regularly via the job engine, ensure that you clean up that job when the plugin is shutdown. This shutdown code should go in a component that implements `DisposableBean` as described above.














































































