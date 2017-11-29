---
aliases:
- /server/framework/atlassian-sdk/cannot-start-plugin-2818394.html
- /server/framework/atlassian-sdk/cannot-start-plugin-2818394.md
category: devguide
confluence_id: 2818394
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818394
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818394
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/troubleshooting/cannot-start-plugin
new_url: /server/framework/atlassian-sdk/cannot-start-plugin
platform: server
product: atlassian-sdk
subcategory: other
title: Cannot start plugin
---
# Cannot start plugin

#### Symptom: "Cannot start plugin"

This is a WARNING not an ERROR in the log. The plugin will also be shown as Disabled on the Admin, Plugins screen.

**Cause**: the OSGI plugin does not know anything about a class used when the plugin is started up

**Solution**: correct any typos in the `interface` attribute in the `component-import` element. Also make sure that the component is exported from elsewhere with a `<component>` element.

**Example**:

    2010-02-24 16:18:52,882 main WARN     [plugin.osgi.factory.OsgiPlugin] Unable to enable plugin 'com.example.jira.plugins.example-errors'
    com.atlassian.plugin.osgi.container.OsgiContainerException: Cannot start plugin: com.example.jira.plugins.example-errors
        at com.atlassian.plugin.osgi.factory.OsgiPlugin.enableInternal(OsgiPlugin.java:385)

Note that the error messages do not show the name of the component that the OSGI container failed to import. In this case the problem was

        <component-import key="foo" interface="com.example.does.not.exist"/>


















































