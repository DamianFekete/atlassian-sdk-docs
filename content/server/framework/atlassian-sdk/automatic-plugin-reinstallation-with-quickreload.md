---
aliases:
- /server/framework/atlassian-sdk/automatic-plugin-reinstallation-with-quickreload-38441282.html
- /server/framework/atlassian-sdk/automatic-plugin-reinstallation-with-quickreload-38441282.md
category: devguide
confluence_id: 38441282
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=38441282
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=38441282
date: '2017-12-08'
guides: guides
legacy_title: Automatic Plugin Reinstallation with QuickReload
platform: server
product: atlassian-sdk
subcategory: learning
title: Automatic plugin reinstallation with QuickReload
---
# Automatic plugin reinstallation with QuickReload

## What is QuickReload?

QuickReload is an Atlassian plugin that significantly reduces plugin development iteration time.

It works by watching output directories for P2 .jar files to be created, and then uploads them into the running Atlassian application (for example JIRA or Confluence). 

It aims to provide the smallest possible time between a bit of code being compiled and linked to it being loaded into the host application and run. 

## Using QuickReload

In your pom.xml for the plugin, ensure the following within the configuration tag:

``` xml
<build>
    <plugins>
        <plugin>
            <groupId>com.atlassian.maven.plugins</groupId>
            <artifactId>maven-jira-plugin</artifactId>
            <version>${amps.version}</version>
            <extensions>true</extensions>
            <configuration>
                ...
                <enableQuickReload>true</enableQuickReload>
                <enableFastdev>false</enableFastdev>
                ...
            </configuration>
```

{{% note %}}

FastDev must be disabled, as this clashes with the operation of QuickReload 

{{% /note %}}

Once you've updated your pom as shown above you can start your application.

Whenever you make a change, all you need to do is rebuild your .jar file using the following `command` in a separate terminal window and it will be automatically reloaded into your application.

``` bash
$ atlas-mvn package
```

## How it works

The idea behind quickreload is quite simple.  It uses a file change watching library called <a href="https://bitbucket.org/atlassianlabs/atlassian-watchservice" class="external-link">atlassian-watch-service</a> which is a simple wrapper for the Java 7 file watch APIs or the jwatchservice code that runs on JDK 6.

The service watches to see whether a jar has changed; If a change is detected it examines it to see if it's an Atlassian plugin and if it is it calls on the plugin system to install the updated jar. 

Because the file watching service raises an event to say there was a change when the jar is first created (but not yet populated with files) the code has to wait a short time for the jar to be fully formed. However, the wait time is only about 10-100ms, so it's not a big problem.

The plugin system doesn't care where plugin files are installed from. It can be `<home>/plugins/installed-plugins` or any other directory. So this code uses the `<dir>/target directory` directly as the place to install the plugin from.

There's no copying and no HTTP transfer making it nice and speedy!

## QuickReload Advanced Configuration

### The pom.xml convention

By default you should not have to configure anything for QuickReload to work because it uses a pom.xml strategy on what directories to watch for changes.

-   QR starts from the current running directory
-   QR ascends up directories until it find a pom.xml that has no parent pom.xml
-   QR then descends down from there to find all pom.xml files and tracks their peer &lt;dir&gt;/target directories for changed .jar files

This will allow QuickReload to watch many plugins in a multi module Maven project.

### The quickreload.properties convention

You can drop a quickreload.properties file into the project to tell QuickReload what to explicitly watch along with to the pom.xml convention.

-   QR ascends up directories until it finds a quickreload.properties file
-   QR reads the entries and begins to watch those directories

The directories can be absolute or relative to the quickreload.properties file. Also IF the directory contains a pom.xml and then &lt;dir&gt;/target is assumed as the right place to watch for .jar changes.

The file looks like this

``` bash
    #
    # Add directories to this file, one on each line, and the quick reload support will monitor them
    # and automatically load them as soon as they are compiled and assembled.
    #
    # You can use -Dquickreload.dirs=dir1,dir2,dir3 on the JVM command line to also specify directories
    # to monitor.
    #
    # relative path to plugin
    some/path/test-plugin

    # absolute path to plugin
    /Users/me/src/atlassian/servicedesk/master/plugin
```

#### The quickreload.properties $HOME convention

Finally QuickReload will look for a $HOME/quickreload.properties file as configuration. You could put uber common entries in here but in general the pom.xml convention is the most powerful and the least amount of work to configure.

## Front End Alternate Resource Directories

QuickReload also enables a front end development dev speed enabler called "Alternate Resource Directories". These cause the web plugin system to load your JavaScript/Css/LESS from source directories instead of from a package .jar plugin.

Hence you can edit a .js file say and press refresh in the browser and it changes.

It uses the pom.xml strategy and add &lt;dir&gt;/src/main/resources to the plugin system alternate resource directory loading mechanism for you.

There is no more need to specify -Dplugin.resource.directories as it will be done for you.

Finally you can specify the directories to track on the command line via

``` bash
-Dquickreload.tracked=dir1,dir2,dir3
```

If you really must but in general, it "just works" for Maven projects.

This allows you to have two or more plugins being developed at the same time with jar and resource monitoring in place automatically. Cool right?

You can put properties before a line entry via a : character. Multiple properties can be specified via the ; character

``` bash
prop1=123;prop2=xyz;prop3 : /some/path
```

 

The current properties are :

-   resource - marks the path as a resource entry and it will be placed into the -Dplugin.resource.directories system directory

## Controlling web batching

The Atlassian Web Resource system can batch together files for faster loading. But this means its harder to debug. So there is a atlassian.dev.mode system property to control that.

But its a one time thing that is set at JVM startup right? Not anymore.

Press 'B' when QuickReload is running and you can toggle between speed of web batching being enabled and the debug ability of when web batching is disabled.

## Log Output

The quick reload plugin includes some very obvious entries in the log, to make it quick and easy to pick out from the wall of log text:  

``` bash
    [INFO] [talledLocalContainer] 2014-05-08 18:10:14,332 http-bio-2990-exec-26 INFO anonymous 1090x6739x1 - 0:0:0:0:0:0:0:1 /rest/quickreload/1/install [labs.plugins.quickreload.PluginInstaller]
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       v
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer] Starting Quick Reload - '/Users/bbaker/src/atlassian/plugins/quickreload/test-plugin/target/quickreload-test-plugin-1.3-SNAPSHOT.jar'....
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer] 2014-05-08 18:10:14,335 http-bio-2990-exec-26 INFO anonymous 1090x6739x1 - 0:0:0:0:0:0:0:1 /rest/quickreload/1/install [atlassian.plugin.loaders.ScanningPluginLoader] No plugins found to be installed
    [INFO] [talledLocalContainer] 2014-05-08 18:10:16,752 http-bio-2990-exec-26 INFO anonymous 1090x6739x1 - 0:0:0:0:0:0:0:1 /rest/quickreload/1/install [atlassian.plugin.manager.DefaultPluginManager] Found dependent enabled plugins for uninstalled plugin 'com.atlassian.labs.plugins.quickreload.test': [].  Disabling...
    [INFO] [talledLocalContainer] 2014-05-08 18:10:16,752 http-bio-2990-exec-26 INFO anonymous 1090x6739x1 - 0:0:0:0:0:0:0:1 /rest/quickreload/1/install [atlassian.plugin.manager.DefaultPluginManager] Updating plugin 'com.atlassian.labs.plugins.quickreload.test' to 'com.atlassian.labs.plugins.quickreload.test'
    [INFO] [talledLocalContainer] 2014-05-08 18:10:16,752 http-bio-2990-exec-26 INFO anonymous 1090x6739x1 - 0:0:0:0:0:0:0:1 /rest/quickreload/1/install [atlassian.plugin.manager.DefaultPluginManager] Disabling com.atlassian.labs.plugins.quickreload.test
    [INFO] [talledLocalContainer] 2014-05-08 18:10:16,757 Timer-1 WARN      [plugins.quickreload.test.Launcher]
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer] Quick Reload Test Plugin is going out of existence!!
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer] 2014-05-08 18:10:16,760 http-bio-2990-exec-26 INFO anonymous 1090x6739x1 - 0:0:0:0:0:0:0:1 /rest/quickreload/1/install [atlassian.plugin.loaders.ScanningPluginLoader] Removed plugin com.atlassian.labs.plugins.quickreload.test
    [INFO] [talledLocalContainer] 2014-05-08 18:10:16,777 ThreadPoolAsyncTaskExecutor::Thread 56 WARN anonymous 1090x6739x1 - 0:0:0:0:0:0:0:1 /rest/quickreload/1/install [plugins.quickreload.test.Launcher]
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer] Quick Reload Test Plugin is coming into existence!!
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer] 2014-05-08 18:10:16,785 http-bio-2990-exec-26 INFO anonymous 1090x6739x1 - 0:0:0:0:0:0:0:1 /rest/quickreload/1/install [labs.plugins.quickreload.PluginInstaller]
    [INFO] [talledLocalContainer]                       ^
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]                       |
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer]           A watched plugin never boils!
    [INFO] [talledLocalContainer]
    [INFO] [talledLocalContainer] Quick Reload Finished (2453 ms) - '/Users/bbaker/src/atlassian/plugins/quickreload/test-plugin/target/quickreload-test-plugin-1.3-SNAPSHOT.jar'
```

 

## Security

 

{{% warning %}}

QuickReload should *never be used in a production environment* 

{{% /warning %}}

There isn't any - that's the point. The cost of crypto encoding admin:admin is a significant cost in terms of time for plugin reload, so it doesn't do it.

 

HTML Control Panel

QuickReload has a control panel you can visit to see whats in play.

    http://localhost:2990/jira/plugins/servlet/qr

## REST API

QuickReload has a REST API to help you be a better developer

Visit this to begin discovering it

    http://localhost:2990/jira/rest/qr/1.0/api

Currently you can

-   See all OSGi bundles in the system

        http://localhost:2990/jira/rest/qr/1.0/bundles

-   See a specific OSGI bundle

        http://localhost:2990/jira/rest/qr/1.0/bundles/{bundleId}

-   See all the OSGi services in the system

        http://localhost:2990/jira/rest/qr/1.0/services

-   See all Atlassian Plugins in the system

        http://localhost:2990/jira/rest/qr/1.0/plugins

-   See a specific Atlassian Plugin, including its modules and internal Spring bean context

        http://localhost:2990/jira/rest/qr/1.0/plugins/{pluginKey}

-   See the state of a current state of a plugin, and with POST / DELETE to enable or disable the plugin

        http://localhost:2990/jira/rest/qr/1.0/plugin/enabled/{pluginKey}

-   See the state of a current state of a plugin module, and with POST / DELETE to enable or disable the plugin module

        http://localhost:2990/jira/rest/qr/1.0/plugin/enabled/{moduleKey}

-   View the last 100 events in the application

        http://localhost:2990/jira/rest/qr/1.0/events

-   See the list of QR tracked directories

        http://localhost:2990/jira/rest/qr/1.0/tracked

-   See whether web batching is enabled

        http://localhost:2990/jira/rest/qr/1.0/batching

## Troubleshooting

### java.lang.UnsatisfiedLinkError

If you see this "java.lang.UnsatisfiedLinkError: Native Library" error it means that the quick reload plugin was re-loaded while running but it could not be. It's ironic I know that a reloading plugin can't be cleanly re-loaded but it's more to do with the underlying native file watching library than quick re-load itself.

Java does not like to unload native libraries and the underlying name.pachler.nio.file does not expect to be reloaded. Trust me, you won't see this much. It's seen more in developing this plugin itself or you are running FastDev at the same time as QuickReload



























































































































































