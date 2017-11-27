---
aliases:
- /server/framework/atlassian-sdk/automatic-plugin-reinstallation-with-fastdev-8945760.html
- /server/framework/atlassian-sdk/automatic-plugin-reinstallation-with-fastdev-8945760.md
category: devguide
confluence_id: 8945760
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8945760
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8945760
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/automatic-plugin-reinstallation-with-fastdev
new_url: /server/framework/atlassian-sdk/automatic-plugin-reinstallation-with-fastdev
platform: server
product: atlassian-sdk
subcategory: learning
title: Automatic plugin reinstallation with FastDev
---
# Automatic plugin reinstallation with FastDev

{{% warning %}}

FastDev and atlas-cli have been deprecated. Please use [Automatic Plugin Reinstallation with QuickReload](/server/framework/atlassian-sdk/automatic-plugin-reinstallation-with-quickreload) instead.

{{% /warning %}}

 

There is no need to manually install your plugin into the Atlassian application every time you change the code. Instead, FastDev will automatically reinstall the plugin for you.

FastDev is a plugin for Atlassian applications that speeds up plugin development by scanning plugin directories for changes and automatically reinstalling plugins when necessary.

FastDev is bundled with the Atlassian Plugin SDK 3.6 and later. It is enabled by default. See the [configuration](#configuration) section below for instructions on disabling it.

 

## How it Works

FastDev intercepts plugin servlet requests and checks for a hard refresh. (A hard refresh is triggered by Shift+Reload in most browsers.) If a hard refresh is detected, FastDev scans plugin directories looking for files that have changed since the plugin was installed. If it finds such files, FastDev starts a Maven process to install the plugin.

A hard refresh is detected by checking the values of the `Cache-Control` and `Pragma` headers in the request sent by your browser.

{{% warning %}}

FastDev and atlas-cli have been deprecated. Please use [Automatic Plugin Reinstallation with QuickReload](https://developer.atlassian.com/docs/developer-tools/automatic-plugin-reinstallation-with-quickreload) instead.

{{% /warning %}}

 

To trigger the reinstallation of your plugin:

1.  Make the changes to your plugin module.
2.  Open the Developer Toolbar.  
    <img src="/server/framework/atlassian-sdk/images/fastdev1.png" width="600" />
3.  Press the FastDev icon.  
    <img src="/server/framework/atlassian-sdk/images/fastdev2.png" width="600" />  
    The system rebuilds and reloads your plugin:  
    <img src="/server/framework/atlassian-sdk/images/fastdev3.png" width="600" />

Use live reload to view real-time updates to templates and other resources:

1.  Open the Developer Toolbar.
2.  Press the live reload icon.  
    The  icon starts to revolve indicating it is on.
3.  Edit your project resources.
4.  Save your changes:  
    Back in the host application, your plugin displays any user visible changes you make. 

This screenshot shows FastDev in action, reloading a web item plugin module in JIRA 5.0:

<img src="/server/framework/atlassian-sdk/images/fastdev.png" class="confluence-thumbnail" />

FastDev can also handle reloads for multi-module maven projects that contain multiple plugins. Please refer to the configuration for [multi-module plugins](#multi-module-plugins) below.

## Configuration

FastDev should work out of the box for any single module plugin being run with the Atlassian Maven Plugin Suite (AMPS) or the Atlassian Plugin SDK. There are several configuration options available for more complex plugins or specific needs.

You can set all configuration options in your plugin's `pom.xml` file by adding the specified property to the `systemPropertyVariables` node.

### Adding or Changing Ignored Files

Some changes do not require plugin installation to take effect, such as changes to JavaScript or CSS files. FastDev ignores many of these files by default, but you may wish to add or change these defaults to suit your needs.

You can specify additional files to ignore either by directory, extension, or file name:

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Type</p></th>
<th><p>Property name</p></th>
<th><p>Default(s)</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Directory</p></td>
<td><p>fastdev.no.reload.directories</p></td>
<td><p>.svn</p></td>
</tr>
<tr class="even">
<td><p>Extension</p></td>
<td><p>fastdev.no.reload.extensions</p></td>
<td><p>js, vm, vmd, fm, ftl, html, png, jpeg, gif, css</p></td>
</tr>
<tr class="odd">
<td><p>File</p></td>
<td><p>fastdev.no.reload.files</p></td>
<td><p> </p></td>
</tr>
</tbody>
</table>

``` javascript
<systemPropertyVariables>
    ...
    <fastdev.no.reload.directories>images</fastdev.no.reload.directories>
    <fastdev.no.reload.extensions>coffee</fastdev.no.reload.extensions>
    <fastdev.no.reload.files>${basedir}/src/main/resources/gadget.xml</fastdev.no.reload.files>
</systemPropertyVariables>
```

### Changing the Maven Command

By default, FastDev assumes that Maven can be accessed on the command line as `mvn`. If this is not the case, or if you want FastDev to use a different command, you can configure this option in the POM:

``` javascript
<systemPropertyVariables>
    ...
    <fastdev.mvn.command>mvn2</fastdev.mvn.command>
</systemPropertyVariables>
```

### Multi-Module Plugins

More complex plugins may have more than one plugin module. FastDev can handle reloads for multi-module maven projects that contain multiple plugins, but you need to tell FastDev about any additional plugin root directories:

``` javascript
<systemPropertyVariables>
    ...
    <plugin.root.directories>${basedir}/../myplugin-bundle</plugin.root.directories>
</systemPropertyVariables>
```

Note that FastDev is currently not very smart about dependency management, so if you are attempting to reload multiple plugins that depend on each other, you may run into problems.

### Credentials

By default, FastDev will reinstall plugins using `admin` credentials. If the `admin` user is not permitted to manage plugins in the application instance or has a non-default password, you will need to specify these credentials in the POM:

``` javascript
<systemPropertyVariables>
    ...
    <fastdev.install.username>sysadmin</fastdev.install.username>
    <fastdev.install.password>secret</fastdev.install.password>
</systemPropertyVariables>
```

Both properties are optional; FastDev will use the default unless otherwise specified.

{{% note %}}

These credential properties are supported starting with FastDev 1.9 (bundled with Atlassian Plugin SDK 3.7.1 or later).

{{% /note %}}

### Disabling FastDev

To disable FastDev, set the following property in the `maven-amps-plugin` configuration in your plugin's `pom.xml`:

``` javascript
<plugins>
    ...
    <plugin>
        <groupId>com.atlassian.maven.plugins</groupId>
        <artifactId>maven-amps-plugin</artifactId>
        <configuration>
            ...
            <enableFastdev>false</enableFastdev>
        </configuration>
    </plugin>
</plugins>
```

### Specifying a FastDev release

If you need to use a different FastDev release than the one bundled with the Atlassian Plugin SDK release you are using, you can set the following property in the `maven-amps-plugin` configuration in your plugin's `pom.xml`:

``` javascript
<plugins>
    ...
    <plugin>
        <groupId>com.atlassian.maven.plugins</groupId>
        <artifactId>maven-amps-plugin</artifactId>
        <configuration>
            ...
            <fastdevVersion>1.9</fastdevVersion>
        </configuration>
    </plugin>
</plugins>
```

## Troubleshooting Reloading

-   The dynamic deployment method via FastDev or CLI will work *most* of the time, but not all plugins are eligible for dynamic installation. Specifically, some versions of some applications mark some module types as requiring a restart. If a plugin uses one of the module types that require a restart, the plugin will be installed but not activated until the application is restarted. And occasionally the host application fails to detect new changes. If you suspect this may be happening, just hit `ctrl-c` in the first window and type `atlas-run` again to completely restart the host app with your latest changes included. See the list of [plugin modules that cannot be dynamically reloaded](/server/framework/atlassian-sdk/plugins-that-cannot-be-reloaded-with-fastdev-or-pi).
-   [If you change pom.xml, you may need to restart the atlas-cli](/server/framework/atlassian-sdk/2818364.html).
-   For other errors, please refer to the [FAQ and troubleshooting section](/server/framework/atlassian-sdk/atlassian-plugin-sdk-faq).































































































































































































