---
title: Atlassian Plugin Archetypes 2818678
aliases:
    - /server/framework/atlassian-sdk/atlassian-plugin-archetypes-2818678.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818678
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818678
confluence_id: 2818678
platform:
product:
category:
subcategory:
---
# Documentation : Atlassian Plugin Archetypes

{{% warning %}}

These instructions are obsolete if you are using the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/developing-with-the-atlassian-plugin-sdk) (and you should be). We have left them here only as reference for those using very old products which do not support the SDK.

{{% /warning %}}

Atlassian has created Maven 2 archetypes for five of our pluggable products.

-   **JIRA** - you can view the <a href="http://svn.atlassian.com/fisheye/browse/public/atlassian/jira/plugins/jira-plugin-archetype" class="external-link">source code here</a>
-   **Confluence** - you can view the <a href="http://svn.atlassian.com/fisheye/browse/public/atlassian/confluence/plugins/confluence-plugin-archetype" class="external-link">source code here</a>
-   **Bamboo** - you can view the <a href="http://svn.atlassian.com/fisheye/browse/public/atlassian/bamboo/plugins/bamboo-plugin-archetype" class="external-link">source code here</a>
-   **Crowd** - you can view the <a href="http://svn.atlassian.com/fisheye/browse/public/atlassian/crowd/plugins/crowd-plugin-archetype" class="external-link">source code here</a>
-   **Fisheye/Crucible** - you can view the <a href="http://svn.atlassian.com/fisheye/browse/public/atlassian/crucible/plugins/crucible-plugin-archetype" class="external-link">source code here</a>

**See the build status for these archetypes** **<a href="http://bamboo.developer.atlassian.com/browse/ARCH" class="external-link">here</a>.**

## Instructions

You can use a plugin archetype by running one of the Maven commands below. Maven will download all of the required dependencies, set up a project skeleton, and prepare you to run [unit and functional tests](https://developer.atlassian.com/pages/viewpage.action?pageId=2818653). To set up your project template, run the command below, substituting your package name and plugin name where appropriate.

We recommend creating all of your archetypes at the top level of a new, empty directory. Be sure **not** to create a plugin archetype from a directory with an existing pom.xml, as it will try to add the plugin as a sub-module of the project in the current directory (which will fail unless the project has the packaging type "pom").

After creating the template plugin, it's a good idea to run some other command, like 'mvn compile', 'mvn idea:idea', or 'mvn eclipse:eclipse' to force mvn to download all of the project dependencies.

## Atlassian Archetype Catalog

Recent versions of Maven support archetype discovery through catalog files. Catalog files always point to the latest available version of an archetype, and they can also prompt you for required properties through the command line.

    mvn archetype:generate -DarchetypeCatalog=http://svn.atlassian.com/svn/public/atlassian/maven-plugins/archetype-catalog

{{% note %}}

Archetype catalogs require version 2.0-alpha-4 or later of the maven-archetype plugin. If the above commands don't work for you, try adding `-cpu` after `mvn`; this will force Maven to download the most recent version of the plugin.

{{% /note %}}

## Using Archetypes Manually

In general, we recommend using the archetype catalog in most cases, but if you prefer, you can manually create projects fro specific archetypes. Follow the directions for the product you're targeting and the platform you're developing on. Note that you'll need to replace `$MY_PACKAGE` and `$MY_PLUGIN` (or `%MY_PACKAGE%` and `%MY_PLUGIN%`) with the actual package name and plugin ID that you wish to use.

## JIRA

### Unix

    mvn archetype:create \
        -DarchetypeGroupId=com.atlassian.maven.archetypes \
        -DarchetypeArtifactId=jira-plugin-archetype \
        -DarchetypeVersion=15 \
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ \
        -DgroupId=$MY_PACKAGE -DartifactId=$MY_PLUGIN

### Windows

    mvn archetype:create ^
        -DarchetypeGroupId=com.atlassian.maven.archetypes ^
        -DarchetypeArtifactId=jira-plugin-archetype ^
        -DarchetypeVersion=15 ^
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ ^
        -DgroupId=%MY_PACKAGE% -DartifactId=%MY_PLUGIN%

## Confluence

### Unix

    mvn archetype:create \
        -DarchetypeGroupId=com.atlassian.maven.archetypes \
        -DarchetypeArtifactId=confluence-plugin-archetype \
        -DarchetypeVersion=15 \
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ \
        -DgroupId=$MY_PACKAGE -DartifactId=$MY_PLUGIN

### Windows

    mvn archetype:create ^
        -DarchetypeGroupId=com.atlassian.maven.archetypes ^
        -DarchetypeArtifactId=confluence-plugin-archetype ^
        -DarchetypeVersion=15 ^
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ ^
        -DgroupId=%MY_PACKAGE% -DartifactId=%MY_PLUGIN%

## Bamboo

### Unix

    mvn archetype:create \
        -DarchetypeGroupId=com.atlassian.maven.archetypes \
        -DarchetypeArtifactId=bamboo-plugin-archetype \
        -DarchetypeVersion=10 \
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ \
        -DgroupId=$MY_PACKAGE -DartifactId=$MY_PLUGIN

### Windows

    mvn archetype:create ^
        -DarchetypeGroupId=com.atlassian.maven.archetypes ^
        -DarchetypeArtifactId=bamboo-plugin-archetype ^
        -DarchetypeVersion=10 ^
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ ^
        -DgroupId=%MY_PACKAGE% -DartifactId=%MY_PLUGIN%

## Crowd

### Unix

    mvn archetype:create \
        -DarchetypeGroupId=com.atlassian.maven.archetypes \
        -DarchetypeArtifactId=crowd-plugin-archetype \
        -DarchetypeVersion=1-SNAPSHOT \
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ \
        -DgroupId=$MY_PACKAGE -DartifactId=$MY_PLUGIN

### Windows

    mvn archetype:create ^
        -DarchetypeGroupId=com.atlassian.maven.archetypes ^
        -DarchetypeArtifactId=crowd-plugin-archetype ^
        -DarchetypeVersion=1-SNAPSHOT ^
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ ^
        -DgroupId=%MY_PACKAGE% -DartifactId=%MY_PLUGIN%

## Fisheye/Crucible

### Unix

    mvn archetype:create \
        -DarchetypeGroupId=com.atlassian.maven.archetypes \
        -DarchetypeArtifactId=crucible-plugin-archetype \
        -DarchetypeVersion=1-SNAPSHOT \
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ \
        -DgroupId=$MY_PACKAGE -DartifactId=$MY_PLUGIN

### Windows

    mvn archetype:create ^
        -DarchetypeGroupId=com.atlassian.maven.archetypes ^
        -DarchetypeArtifactId=crucible-plugin-archetype ^
        -DarchetypeVersion=1-SNAPSHOT ^
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ ^
        -DgroupId=%MY_PACKAGE% -DartifactId=%MY_PLUGIN%

## Example

For example, if Joe Developer from Acme Corp were writing his first Confluence macro, he would create an empty folder (naming it for example "plugin-project"), enter that directory, and then -- replacing `$MY_PACKAGE` with "com.acme.confluence.plugins", and `$MY_PLUGIN` with "awesome-macro" -- he would run the following command (assuming he's using a Unix command line):

    mvn archetype:create \
        -DarchetypeGroupId=com.atlassian.maven.archetypes \
        -DarchetypeArtifactId=confluence-plugin-archetype \
        -DarchetypeVersion=15 \
        -DremoteRepositories=https://maven.atlassian.com/repository/public/ \
        -DgroupId=com.acme.confluence.plugins -DartifactId=awesome-macro

This would download some 50 small files from the net, create a folder named "awesome-macro" into his "plugin-project" folder, and set up all he needs to work on the plugin.

Please return to [Set up the Atlassian Plugin SDK and Build a Project](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project) for the next steps.

















































































































































































































































































































