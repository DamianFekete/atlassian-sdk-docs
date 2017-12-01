---
aliases:
- /server/framework/atlassian-sdk/creating-a-plugin-skeleton-with-the-atlassian-sdk-2818617.html
- /server/framework/atlassian-sdk/creating-a-plugin-skeleton-with-the-atlassian-sdk-2818617.md
category: devguide
confluence_id: 2818617
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818617
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818617
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/development-cycle/creating-a-plugin-skeleton-with-the-atlassian-sdk
new_url: /server/framework/atlassian-sdk/creating-a-plugin-skeleton-with-the-atlassian-sdk
platform: server
product: atlassian-sdk
subcategory: learning
title: Creating a plugin skeleton with the Atlassian SDK
---
# Creating a plugin skeleton with the Atlassian SDK

Run the following shell script to create your plugin skeleton. The shell script is part of the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk). It will download the directories and files that make up a 'Hello World' plugin for your chosen Atlassian application.

1.  Add a new directory in your file system where you would like to create your plugin.
2.  Open a command window and navigate into the directory where you want to create your plugin.
3.  Run `atlas-create-APPLICATION-plugin`, where `APPLICATION` is the Atlassian application you are developing your plugin for. For example, run `atlas-create-confluence-plugin` or `atlas-create-jira-plugin`.
4.  When prompted, supply the following values:

    {{% note %}}

    Make sure your package names are unique

Make sure your package names are unique. You can choose any package name, provided that it does not conflict with any existing package used in the Atlassian application you are developing for, or in any other plugins. Do **not** use `com.atlassian.confluence.plugins.*`. That is confusing to people who try to use the plugin. **Use a real package name** that corresponds to your organisation or project. For example: `org.mycompany.confluence.plugins.*`. The <a href="http://java.sun.com/docs/books/jls/second_edition/html/packages.doc.html#40169" class="external-link">Sun Java documentation</a> has some tips about conventions used to ensure unique package names.

    {{% /note %}}

    -   '**groupID**' - Enter a value that identifies your company or project. This value will also be used as the default for your package name, but you can change it in the next few steps below. For example:  
        `com.mycompany.confluence.plugins`
    -   '**artifactId**' - This is an identifier for your plugin. Do **not** use spaces in the artifactId. For example:  
        `sarahtest`
    -   '**version**' - This is the version number of your plugin. You can leave it at the default or enter your own version number. For example:  
        `1.0-SNAPSHOT`.
    -   '**package**' - You can enter a specific value or keep the default value, as derived from the groupID that you entered above. For example:  
        `com.mycompany.confluence.plugins`

5.  Press 'Enter' to confirm your selections, or press 'N' if you want to go back and change the values you have supplied.
6.  You should see a `BUILD SUCCESSFUL` message.  
    (Ignore any warnings. It is all good if the build is successful.)

#### Troubleshooting this Step

If this process ends with an error message, please refer to the [FAQ and troubleshooting section](/server/framework/atlassian-sdk/writing-your-first-plugin-faq).

#### About the Plugin Skeleton

The first step when starting a new plugin is to create a skeleton for that plugin. This involves creating plenty of directories and subdirectories, XML files and Java files. This is what the above steps will do for you. We use a Maven <a href="http://maven.apache.org/guides/introduction/introduction-to-archetypes.html" class="external-link">archetype</a>, which is basically a plugin template. We have created plugin templates, or archetypes, for each of our pluggable applications.

When you create your plugin skeleton, Maven will download (a lot of) dependencies from the Internet, set up a project skeleton, and prepare you to run unit and functional tests. It creates a new directory structure that looks something like this (screenshot taken from Eclipse IDE):  
  
![](/server/framework/atlassian-sdk/images/pluginskeletonineclipse.png)

Take a look at the directory where you created your plugin. Note the following files and directories:

-   The `pom.xml` file in the root directory of your plugin. POM stands for <a href="http://maven.apache.org/guides/introduction/introduction-to-the-pom.html" class="external-link">Project Object Model</a> definition file.
-   Directories for your source code files (`src/main`) and test source code files (`src/test`).
-   Directories for your resources (templates, JavaScript, CSS, images, etc).
-   The `it` package for your integration tests.
-   An `atlassian-plugin.xml` [plugin descriptor file](/server/framework/atlassian-sdk/configuring-the-plugin-descriptor) in your `src/main/resources` directory.
-   A [license file](/server/framework/atlassian-sdk/packaging-and-releasing-your-plugin) in the root directory of your plugin.

#### About the `pom.xml`

The <a href="http://maven.apache.org/guides/introduction/introduction-to-the-pom.html" class="external-link">Project Object Model</a>, POM or `pom.xml`, describes everything that Maven needs to know about your plugin: dependencies, source control, authors, tests and deployment locations. The POM is hierarchical, so many properties are inherited.

#### About your Local Maven Repository

You will notice that your Maven `.m2` directory now has a 'repository' sub-directory, for example `$HOME/.m2/repository`, with a lot of new directories and files in it. Maven keeps local copies of every dependency it ever downloads in this local Maven repository.









































































































































































