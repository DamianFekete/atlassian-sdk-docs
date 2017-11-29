---
aliases:
- /server/framework/atlassian-sdk/atlas-create-jira-plugin-module-8945854.html
- /server/framework/atlassian-sdk/atlas-create-jira-plugin-module-8945854.md
category: devguide
confluence_id: 8945854
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8945854
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8945854
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference/atlas-create-jira-plugin-module
new_url: /server/framework/atlassian-sdk/atlas-create-jira-plugin-module
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-create-jira-plugin-module
---
# atlas-create-jira-plugin-module

This page describes the shell script `atlas-create-jira-plugin-module`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

NOTE: There is a specific version of this shell script for each Atlassian application. The shell script described on this page is for **JIRA**.

 

## Basic Usage

`atlas-create-jira-plugin-module [options]` - Prompts you for plugin module type and related details, then creates an example of a JIRA plugin module that you can adapt to suit your own plugin's needs. (Runs `mvn jira:create-plugin-module`.) Passes all parameters straight through to Maven.The script will automatically add the changes to your `atlassian-plugin.xml` and generate the appropriate Java code.

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

``` javascript
atlas-create-jira-plugin-module -?
atlas-create-jira-plugin-module -help
```

## Examples

Let's assume you want to add a new plugin module to your existing JIRA plugin.

1.  Create your plugin (`atlas-create-jira-plugin`) and install it into the application (`atlas-run`) as usual.
2.  Go to the root directory for your plugin (where the `pom.xml` is located).
3.  Run this command:

        atlas-create-jira-plugin-module

4.  Follow the prompts to specify the type of plugin module that you want, and further information required to create the basic module. For example, let's assume you want to create a web item.
    -   The script shows a list of module types. Select the number (for example, **24**) that corresponds to the web item module type.
    -   Enter a plugin module name. The default is 'My Web Item'. I entered 'Sarah Option'.
    -   Specify the [section](https://developer.atlassian.com/display/JIRADEV/Web+fragments). I entered '`system.top.navigation.bar`'.
    -   Enter a link URL. I entered '`http://ffeathers.wordpress.com`'.
    -   Decide whether you want to do any advanced setup. I entered 'N'.
    -   Decide whether you want to add another plugin module. I entered 'N'.
5.  The script added the required module to my `atlassian-plugin.xml`:

    ``` xml
    <?xml version="1.0" encoding="UTF-8"?>
     
    <atlassian-plugin key="${project.groupId}.${project.artifactId}" name="${project.name}" plugins-version="2">
      <plugin-info>
        <description>${project.description}</description>
        <version>${project.version}</version>
        <vendor name="${project.organization.name}" url="${project.organization.url}"/>
      </plugin-info>
      <web-item name="Sarah Option" i18n-name-key="sarah-option.name" key="sarah-option" section="system.top.navigation.bar" weight="1000">
        <description key="sarah-option.description">The Sarah Option Plugin</description>
        <label key="sarah-option.label"></label>
        <link linkId="sarah-option-link">http://ffeathers.wordpress.com</link>
      </web-item>
      <resource type="i18n" name="i18n" location="atlassian-plugin"/>
    </atlassian-plugin>
    ```

6.  Where relevant, the script will add the Java classes to your plugin's .java file too.

##### RELATED TOPICS

[Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk)




























































































































































































