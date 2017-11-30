---
title: Verifying Your Maven Settings 2818643
aliases:
    - /server/framework/atlassian-sdk/verifying-your-maven-settings-2818643.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818643
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818643
confluence_id: 2818643
platform:
product:
category:
subcategory:
---
# Documentation : Verifying Your Maven Settings

The Maven settings file, `settings.xml`, controls some of the general behavior of Maven. For instance, the file identifies the repositories used to resolve plugin dependencies. It also specifies development environment properties. For example, the `settings.xml` file is where you configure your proxy settings if you need to connect to the Internet through a web proxy.

## settings.xml Location

The file is located in the following directory:

`<atlassian-plugin-sdk-home>/apache-maven/conf `

When installed with the Atlassian SDK, the `settings.xml` is pre-configured with the Atlassian repositories needed to build plugin projects. If you want to include additional repositories in the default profile, you can add them to the file.

## Adding the Atlassian Plugin Repository

We recommend that you use the Maven instance installed with the SDK, which is already configured to rely on the required repositories. However, if for some reason you are attempting to use a `settings.xml` file that was not installed with the Atlassian SDK, you will likely encounter problems resolving dependencies required by the SDK commands. To prevent these problems, add the `pluginGroups` and `profile` elements to your local `settings.xml` file:

``` xml
<pluginRepository>
    <id>atlassian-plugin-sdk</id>
    <url>file://${env.ATLAS_HOME}/repository</url>
     <releases>
        <enabled>true</enabled>
        <checksumPolicy>warn</checksumPolicy>
      </releases>
      <snapshots>
         <enabled>false</enabled>
      </snapshots>
 </pluginRepository>
```





















































































































































































































































