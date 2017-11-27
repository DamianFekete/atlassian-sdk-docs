---
aliases:
- /server/framework/atlassian-sdk/working-with-maven-5669840.html
- /server/framework/atlassian-sdk/working-with-maven-5669840.md
category: devguide
confluence_id: 5669840
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669840
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669840
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/working-with-maven
new_url: /server/framework/atlassian-sdk/working-with-maven
platform: server
product: atlassian-sdk
subcategory: learning
title: Working with Maven
---
# Working with Maven

While the SDK conceals many of the complexities of Maven, it is helpful to understand how it is used, particularly when you are troubleshooting or using advance Maven features. This page discusses concepts behind Maven and how it is used with the SDK.

## What is Maven?

Calling Maven a 'build tool' would be an understatement. But if you have no experience with Maven yet, start thinking of it as a tool for simplifying your life by building your plugin. Quoting the Maven home page:

> Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

Maven is particularly useful because it can automatically manage massive dependency trees, especially transitive dependencies where Plugin X depends on Application Y, which depends on Shared Library Z. Using Maven, you should be able to quickly and easily retrieve all the dependencies that your plugin will need, and create a working development environment in just a few steps.

## Maven and the Atlassian Plugins SDK 

Maven is bundled with the Atlassian Plugin SDK, so you do not need to install it manually. Even if you already have Maven on your system, you should use the one bundled with the SDK, since the SDK requires a specific version of Maven. The version bundled with the SDK is already configured for the SDK, so you do not need to specify repositories. The Atlassian Plugin SDK includes a correctly-configured Maven `settings.xml` file.

The Atlassian SDK wraps Maven commands with its own interactive, script-based commands. The SDK commands offer command-line help and auto-completion, easing development tasks. 

## Running Maven Commands

If you already know Maven, you may want to invoke Maven commands directly.  When running Maven commands against your project, make sure that you use the version of Maven bundled with the Atlassian Plugin SDK. This is important if you have a local version of Maven installed, as well as the Atlassian Plugin SDK.

The simplest way is to use the [`atlas-mvn`](https://developer.atlassian.com/display/DOCS/atlas-mvn) wrapper command instead of `mvn`. You can invoke any Maven command by preceding it in the '`atlas-`' prefix.

For example:

 

    atlas-mvn clean

The command performs the same function as the Maven command `mvn clean`, removing build artifacts from the current project.

If you have multiple versions of Maven on your system, you should use the SDK command wrapper to ensure that the correct Maven version is executed. Alternatively, you can put the bundled Maven on your path. (Run atlas-version to discover the location of the SDK's Maven instance binary file.)

For information on the standard SDK command format, see [Working with the SDK](/server/framework/atlassian-sdk/working-with-the-sdk).

##### RELATED PAGES

-   [Verifying Your Maven Settings](/server/framework/atlassian-sdk/verifying-your-maven-settings-2818643.html)
-   [Colour-Coding your Maven Output](/server/framework/atlassian-sdk/colour-coding-your-maven-output-2818644.html)
-   [Using the AMPS Maven Plugin Directly](/server/framework/atlassian-sdk/using-the-amps-maven-plugin-directly-2818721.html)
-   [Atlassian Maven Repositories](/server/framework/atlassian-sdk/atlassian-maven-repositories-2818705.html)
-   [Developing Plugins with Maven 3](/server/framework/atlassian-sdk/developing-plugins-with-maven-3-18252744.html)














































































