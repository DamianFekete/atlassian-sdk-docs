---
aliases:
- /server/framework/atlassian-sdk/atlas-create-home-zip-2818359.html
- /server/framework/atlassian-sdk/atlas-create-home-zip-2818359.md
category: devguide
confluence_id: 2818359
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818359
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818359
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/command-reference/atlas-create-home-zip
new_url: /server/framework/atlassian-sdk/atlas-create-home-zip
platform: server
product: atlassian-sdk
subcategory: learning
title: atlas-create-home-zip
---
# atlas-create-home-zip

This page describes the shell script `atlas-create-home-zip`, part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

NOTE: This command is only available in [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk) version 3.1 and later

 

## Basic Usage

`atlas-create-home-zip` - Creates a test-resources zip of the current application's home directory. This zip file can then be pointed to in the AMPS productDataPath property to auto-populate application data during startup.

## Examples

{{% tip %}}

Don't run the **atlas-clean** command during this process, until you get to the very end. Running **atlas-clean** before you have finished this configuration will delete the files that were created during this process!

{{% /tip %}}

Let's assume you want to prepopulate JIRA with a few projects and issues for testing on every clean startup. First, run the application as you normally would using `atlas-run`. Next, use the JIRA web interface to create your projects and issues. Stop JIRA (CTRL+C). Finally, go to the root directory of your plugin and type:

    atlas-create-home-zip

This will create a file called **generated-test-resources.zip** in the plugins target folder. Copy this file to a known location (such as, `src/test/resources`). Finally add:

    <productDataPath>${basedir}/src/test/resources/generated-test-resources.zip</productDataPath>

to the `<configuration/>` of the `maven-jira-plugin` or `maven-confluence-plugin` in your pom.xml. The completed configuration should look something like this:

**pom.xml**

``` xml
<plugin>
    <groupId>com.atlassian.maven.plugins</groupId>
    <artifactId>maven-confluence-plugin</artifactId>
    <version>${amps.version}</version>
    <extensions>true</extensions>
    <configuration>
        <productVersion>${confluence.version}</productVersion>
        <productDataVersion>${confluence.data.version}</productDataVersion>
        <!-- Add the productDataPath configuration here -->
        <productDataPath>${project.basedir}/src/test/resources/generated-test-resources.zip</productDataPath>
    </configuration>
</plugin>
```

Now every time you start JIRA or Confluence using `atlas-run` or `atlas-debug`, the home directory will be prepopulated using the contents of the generated zip file.






























































































































































































