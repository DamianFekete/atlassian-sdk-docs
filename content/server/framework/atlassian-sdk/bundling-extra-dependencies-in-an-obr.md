---
aliases:
- /server/framework/atlassian-sdk/bundling-extra-dependencies-in-an-obr-2818612.html
- /server/framework/atlassian-sdk/bundling-extra-dependencies-in-an-obr-2818612.md
category: devguide
confluence_id: 2818612
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818612
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818612
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/advanced-plugin-development-faq/bundling-extra-dependencies-in-an-obr
new_url: /server/framework/atlassian-sdk/bundling-extra-dependencies-in-an-obr
platform: server
product: atlassian-sdk
subcategory: other
title: Bundling extra dependencies in an OBR
---
# Bundling extra dependencies in an OBR

With the ability to create dynamic dependencies on other plugins and libraries with OSGi and the Plugins 2 framework, the challenge becomes making sure that all the other required bundles are actually installed into the application along with your plugin. The Plugin Exchange lets you define 'dependent' plugins, but currently that information isn't used anywhere.

A solution is to use an OSGi Bundle Repository (OBR) file, which is essentially a JAR file containing your plugin, any dependent plugins, and the information required to install them.

## Requirements

### UPM only

Currently, you have to use the Universal Plugin Manager (UPM) to install OBR files. Installing via the older 'Plugins' console or the 'Plugin Repository' from Confluence 3.3 and earlier will not work. From Confluence 3.5 onwards, the UPM is the default and only option for installing plugins via the Administration Console.

### OSGi bundles only

Any library/plugin you want to bundle must be an OSGi bundle in its own right, *with a valid `META-INF/MANIFEST.MF` file defining the OSGi bundle*. This is mainly an issue for any Atlassian-based plugins you might have, which do not generate a `MANIFEST.MF` by default. To do so, you need to declare the `<instructions>` section within the definition for the 'com.atlassian.maven.plugins' plugin for the application you're targeting. More information about this is available [here](/server/framework/atlassian-sdk/managing-dependencies).

## `pom.xml` Configuration

The Atlassian Plugin SDK automatically builds an OBR for your plugin, but actually getting it to work as expected takes a bit more work. There are a few key things required to get your plugin building and installing correctly via the UPM.

### `<properties>`

This step is not strictly required, but it will make it easier to ensure that you are building and deploying the same versions of your dependencies. Here, we simply create a property value for the version number of the bundled dependency.

``` javascript
<properties>
   <my.library.version>1.0</my.library.version>
   ....
</properties>
```

### `<dependencies>`

All libraries you want to have bundled **must** have an entry in the `<dependencies>` section of the `pom.xml`. They should also have a `scope` of 'provided' or 'test', otherwise they will get included directly into the plugin jar instead. Eg:

``` javascript
<dependencies>
    <dependency>
        <groupId>my.company.whatever</groupId>
        <artifactId>my-library</artifactId>
        <version>${my.library.version}</version>
        <scope>provided</scope>
    </dependency>
    ....
</dependencies>
```

### AMPS

There are two things to configure for the AMPS plugin: `<pluginDependencies>` and `<instructions>`.

### `<pluginDependencies>`

Within the `<configuration>` section of your plugin's 'maven-&lt;application&gt;-plugin' definition for AMPS, you need to set the `<pluginDependencies>` details for the dependencies you want bundled.

### `<instructions>`

The package for the dependent plugin **must** be listed in the `<Import-Package>` section of the `<instructions>` for the OSGi bundle. More details about that are [here](/server/framework/atlassian-sdk/managing-dependencies). Some plugins do not technically need to be included for your plugin to build, but if they're not listed here, they won't get installed, since the UPM does dependency checking to ensure it doesn't install libraries that it doesn't need to.

It also seems that on some platforms a spurious 'CONF\_COMM' property is added to the `MANIFEST.MF` when building this way. The fix is to include an empty `<CONF_COMM/>` element in your `<instructions>`.

### Example

In this example we're targeting Confluence, but similar values would be required for any other targeted application.

``` javascript
<build>
        <plugins>
            <plugin>
                <groupId>com.atlassian.maven.plugins</groupId>
                <artifactId>maven-confluence-plugin</artifactId>
                <!-- use the latest version of the SDK -->
                <version>3.2.4</version>
                <extensions>true</extensions>
                <configuration>
                    <productVersion>${atlassian.product.version}</productVersion>
                    <testResourcesVersion>${atlassian.product.data.version}</testResourcesVersion>
                    <!-- Specify what to bundle in the OBR -->
                    <pluginDependencies>
                        <pluginDependency>
                            <groupId>my.company.library</groupId>
                            <artifactId>my-library</artifactId>
                        </pluginDependency>
                    </pluginDependencies>
                    <instructions>
                        <!-- Specify what package to include. Ensure that any packages from OBRs are also listed. -->
                        <Import-Package>
                            my.company.library;version="${my.library.version}",
                            ....
                        </Import-Package>
                        <CONF_COMM/>
                        ....
                    </instructions>
                </configuration>
            </plugin>
            ....
        </plugins>
        ....
</build>
```

## Build

You should now be able to build your OBR successfully. To check that it is including what you expect, look into the `'/target/obr'` directory in your project after running a build.

Once the `.obr` file is built, you should be able to install it via the UPM by manually uploading it from the 'Install' tab.

## Troubleshooting

Actually getting your OBR to install successfully can be tricky. One issue is that the UPM doesn't always report useful error messages in the log about what is causing the problem. Here are a few tips:

1.  **Ensure you can install the dependencies independently.** Install each dependency into the application individually first to ensure that there aren't any problems with specific libraries. The UPM reports more useful errors this way also. Often the problem is missing imports, either due to not being listed in the `<Import-Package>` section of the library, or being missing from the target application, or having a bad version number.
2.  **Check the MANIFEST.MF.** This is for both the set of dependencies, and the plugin you're building. Take a look and make sure it's getting generated as you expect.
3.  **Check the `obr.xml`.** Inside the OBR (and the `'/target/obr'` directory) is the `obr.xml` file, which defines the links between the plugin and its dependencies. Make sure the extra libraries/plugins are mentioned in the &lt;require&gt; sections for your target plugin.
4.  **All dependencies must be in Maven.** You won't be able to build without this, but it's essential any plugins and libraries you use are available in your development Maven repository. However, they do not have to be available to the general public, since one the OBR is built it is self-contained.

## FAQ

### Why do I have to define all my imports manually now?

The default mechanism used by Atlassian Plugins doesn't generate a MANIFEST.MF file, which is currently required for the UPM to know how to install the OBR file. As such, it needs to be defined manually.

### OBR vs. bundling internally and using `<Export-Package>`

You can achieve almost the same effect as an OBR by bundling your dependent libraries in the same way you could for Plugins 1, and then adding an `<Export-Package>` entry for the common libraries. This is not a bad way to go, and allows plugins to share code and classes, but it has a couple of disadvantages.

Firstly, it doesn't work for dependent *plugins*, since they have extra work that is done, as defined in the `atlassian-plugin.xml`, as well as potentially Spring configurations, etc. You can only export/import the classes, not have extra lifecycle stuff happen.

Secondly, it's not upgradable independently. The versions you use are based on what's available in whatever other plugins you have installed.

On the other hand, a potential disadvantage of OBRs is that the extra bundles will remain installed after the plugin is removed, thus consuming extra memory and/or resources.
















































































































































































































































































































































































































