---
title: Sal Code Samples 5242906
aliases:
    - /server/framework/atlassian-sdk/sal-code-samples-5242906.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5242906
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5242906
confluence_id: 5242906
platform:
product:
category:
subcategory:
---
# SAL code samples

## Using PluginSettings

Add this to your atlassian-plugin.xml. It will only work with a version 2 plugin.

**atlassian-plugin.xml**

``` xml
<atlassian-plugin key="your-plugin-key" name="Your plugin name" plugins-version="2">

    <!-- Makes PluginSettingsFactory available to your plugin. -->
    <component-import key="pluginSettingsFactory" interface="com.atlassian.sal.api.pluginsettings.PluginSettingsFactory" />

    <!-- other stuff here -->

</atlassian-plugin>
```

**Example class**

``` javascript

public class Example {

    final PluginSettingsFactory pluginSettingsFactory;

    public Example(PluginSettingsFactory pluginSettingsFactory) {
        this.pluginSettingsFactory = pluginSettingsFactory;
    }

    public void storeSomeInfo(String key, String value) {
        // createGlobalSettings is nice and fast, so there's no need to cache it (it's memoised when necessary).
        pluginSettingsFactory.createGlobalSettings().put("my-plugin-namespace" + key, value);
    }

    public Object getSomeInfo(String key) {
        return pluginSettingsFactory.createGlobalSettings().get("my-plugin-namespace" + key);
    }

    public void storeSomeInfo(String projectKey, String key, String value) {
        // createSettingsForKey is nice and fast, so there's no need to cache it (it's memoised when necessary).
        pluginSettingsFactory.createSettingsForKey(projectKey).put("my-plugin-namespace" + key, value);
    }

    public Object getSomeInfo(String projectKey, String key) {
        return pluginSettingsFactory.createSettingsForKey(projectKey).get("my-plugin-namespace" + key);
    }

    
}
```

























