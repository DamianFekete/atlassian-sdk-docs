---
title: "atlas-create-stash-plugin-module"
platform: server
product: atlassian-sdk
category: devguide
subcategory: index
date: "2018-07-26"
---
# atlas-create-stash-plugin-module

{{% warning %}}
Stash has been rebranded. For versions 4.0 and later it is known as Bitbucket Server. If you wish to create a plugin for a version 4.0 or later, please see [atlas-create-bitbucket-plugin](/server/framework/atlas-create-bitbucket-plugin) for the correct command. 
Stash commands will be deprecated with the next major version release for AMPS. 
{{% /warning %}}

This page describes the shell script `atlas-create-stash-plugin-module`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

NOTE: There is a specific version of this shell script for each Atlassian application. The shell script described on this page is for **Stash**.

## Basic Usage

 `atlas-create-stash-plugin-module [options]` - Prompts you for plugin module type and related details, then creates an example of a Stash plugin module that you can adapt to suit your own plugin's needs. (Runs `mvn stash:create-plugin-module`.) Passes all parameters straight through to Maven.  

The script will automatically add the changes to your `atlassian-plugin.xml` and generate the appropriate Java code.

## Parameters

This shell script is a Maven wrapper script. All parameters are passed straight through to Maven.

## Getting Help

The shell script will display some help text if you enter one of the following as the first argument:

-   -?
-   -h
-   help
-   -help
-   --help

For example:

``` bash
atlas-create-stash-plugin-module -?
atlas-create-stash-plugin-module -help
```

## Examples

Let's assume you want to add a new plugin module to your existing Stash plugin.

1.  Create your plugin (`atlas-create-stash-plugin`) and install it into the application (`atlas-run`) as usual.
2.  Go to the root directory for your plugin (where the `pom.xml` is located).
3.  Run this command:

    ``` bash
    atlas-create-stash-plugin-module
    ```

4.  Follow the prompts to specify the type of plugin module that you want, and further information required to create the basic module. 
For example, let's assume you want to create a **web item**:
    -   The script shows a list of module types. Select the number (for example, **17**) that corresponds to the web item module type.
    -   Enter a plugin module name. The default is 'My Web Item'. I entered 'Charlie Option'.
    -   Specify the [section](/server/bitbucket/reference/web-fragments/). I entered '`header.global.primary`'.
    -   Enter a link URL. I entered '<a href="http://developer.atlassian.com">http://developer.atlassian.com</a>'.
    -   Decide whether you want to do any advanced setup. I entered 'N'.
    -   Decide whether you want to add another plugin module. I entered 'N'.

5.  The script added the required module to my `atlassian-plugin.xml`:

    ``` xml
  <web-item name="Charlie Option" i18n-name-key="charlie-option.name" key="charlie-option" section="header.global.primary" weight="1000">
    <description key="charlie-option.description">The Charlie Option Plugin</description>
    <label key="charlie-option.label"></label>
    <link linkId="charlie-option-link">http://developer.atlassian.com</link>
  </web-item>
    ```

6.  Where relevant, the script will add the Java classes to your plugin's .java file too.

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)
