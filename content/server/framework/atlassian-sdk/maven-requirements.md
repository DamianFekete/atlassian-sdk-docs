---
aliases:
- /server/framework/atlassian-sdk/maven-requirements-2818714.html
- /server/framework/atlassian-sdk/maven-requirements-2818714.md
category: devguide
confluence_id: 2818714
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818714
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818714
date: '2017-12-11'
legacy_title: Maven Requirements
platform: server
product: atlassian-sdk
subcategory: other
title: Maven Requirements
---
# Maven Requirements

{{% warning %}}

These instructions are obsolete if you are using the <a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Developing+your+Plugin+using+the+Atlassian+Plugin+SDK&amp;linkCreation=true&amp;fromPageId=2818714" class="createlink">Atlassian Plugin SDK</a> (and you should be). This page is being retained only as reference for those using very old products which do not support the Atlassian Plugin SDK.

{{% /warning %}}

![(info)](/server/framework/atlassian-sdk/images/icons/emoticons/information.png) Maven is included in the Atlassian SDK, as described in the page on <a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Setting+up+your+Plugin+Development+Environment&amp;linkCreation=true&amp;fromPageId=2818714" class="createlink">setting up your plugin development environment</a>. **If you install the SDK, there is no need to install Maven separately.** If for some reason you have decided not to use the Atlassian SDK, you will need to install Maven as described below.

The Atlassian plugin development process depends on <a href="http://maven.apache.org/" class="external-link">Maven</a>. You must have **Maven 2.1.0 or later**.

## What is Maven?

Calling Maven a 'build tool' would be an understatement -- but if you have no experience with Maven yet, start thinking of it as a tool for simplifying your life by building your plugin. Quoting the Maven home page:

> Maven is a software project management and comprehension tool. Based on the concept of a project object model (POM), Maven can manage a project's build, reporting and documentation from a central piece of information.

Maven is particularly useful because it can automatically manage massive dependency trees, especially transitive dependencies where Plugin X depends on Application Y, which depends on Shared Library Z. Using Maven, you should be able to quickly and easily retrieve all the dependencies that your plugin will need, and create a working development environment in just a few steps.

## Installing Maven

If for some reason you have decided not to use the Atlassian SDK, you will need to install Maven.

1.  Download the latest release of <a href="http://maven.apache.org/download.html" class="external-link">Maven 2</a>.
2.  Install Maven, following the instructions for your operating system on the <a href="http://maven.apache.org/download.html" class="external-link">Maven download page</a>.

## Configuring your Maven `settings.xml`

The Atlassian SDK includes a correctly-configured Maven `settings.xml` file. We include the information below for those who have decided not to use the Atlassian SDK, or who wish to add the configurations to an existing `settings.xml` file.

1.  If you do not already have a Maven `.m2` directory, create one now. By default, the directory should be in this location, where `USERNAME`is your username:
    -   For Windows XP: `C:\Documents and Settings\USERNAME\.m2`  
        *Note:* Windows does not like the full stop at the beginning of the directory name, so you will probably have to create the directory via a command prompt, e.g: `mkdir C:\Documents and Settings\USERNAME\.m2`
    -   For Windows Vista: `C:\Users\USERNAME\.m2`  
        *Note:* Windows does not like the full stop at the beginning of the directory name, so you will probably have to create the directory via a command prompt, e.g: `mkdir C:\Users\USERNAME\.m2`
    -   For Mac: `/Users/USERNAME/.m2`
    -   For UNIX/Linux: `/home/USERNAME/.m2`
2.  If you do not already have a Maven `settings.xml` file, create one now by copying our [example settings.xml](/server/framework/atlassian-sdk/example-settings-xml). Put the file in your `.m2` directory.
3.  If you already have a Maven `settings.xml` file, edit it and include the components from our [example settings.xml](/server/framework/atlassian-sdk/example-settings-xml).  
    ![(info)](/server/framework/atlassian-sdk/images/icons/emoticons/information.png) If you look closely at our example settings, you will find two lines containing placeholders for username and password. Don't worry about them yet. You do not need them to get started.

## About Maven Settings, Repositories and Proxies

In order for Maven to find and download all of the necessary dependencies, you need to tell it where everything is stored. This is done via the settings file, `settings.xml`.

Your plugin will depend on many different artifacts: the Atlassian application itself, Atlassian modules and various open-source libraries. All of those artifacts are stored in different Maven repositories scattered around the net. However, to simplify configuration and speed up downloads, Atlassian provides a <a href="http://maven.atlassian.com" class="external-link">Maven proxy</a> that contains *all* of the dependencies for all of our applications. The example settings file contains just one repository entry for this proxy, and saves Maven from having to check several different repositories for each artifact it needs. You can read more about the [repositories that are behind the Maven proxy](/server/framework/atlassian-sdk/atlassian-maven-repositories-2818705.html).

Atlassian will release binary and Javadoc artifacts for all of our product releases and their Atlassian-managed dependencies. We will release source artifacts wherever we can freely do so. Some of our closed-source artifacts will only be available via manual download for source license holders.

We will also release various milestone and snapshot releases during application development, to aid plugin developers in testing their work against upcoming application releases.

You will be able to find all of these artifacts in the <a href="http://maven.atlassian.com" class="external-link">Maven proxy</a>.

## Troubleshooting

Please refer to our [FAQ and troubleshooting page](/server/framework/atlassian-sdk/atlassian-plugin-sdk-faq).





































































































































