---
aliases:
- /server/framework/atlassian-sdk/learn-the-development-platform-by-example-16352140.html
- /server/framework/atlassian-sdk/learn-the-development-platform-by-example-16352140.md
category: devguide
confluence_id: 16352140
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16352140
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16352140
date: '2017-12-08'
guides: tutorials
legacy_title: Learn the Development Platform by Example
platform: server
product: atlassian-sdk
subcategory: learning
title: Learn the development platform by example
---
# Learn the development platform by example

This tutorial teaches you about the Atlassian plugin development platform. This tutorial introduces you to tools and APIs you can use to develop plugins for any Atlassian application. You'll create a plugin of your own that works in any Atlassian application. Your plugin will use AUI (Atlassian User Interface) templates for its look and GUI, and be able to store and retrieve data. 

You might notice that Atlassian often uses the terms 'add-on' and 'plugin' in tools and documentation. A plugin is a type of add-on you can develop for use in Atlassian host applications. A plugin is distinctive in that it runs in the same VM as the Atlassian host application.

This tutorial contains the following topics: 

-   [Create a plugin skeleton](/server/framework/atlassian-sdk/create-a-plugin-skeleton)
-   [Convert component to servlet module](/server/framework/atlassian-sdk/convert-component-to-servlet-module)
-   [Run your plugin in the container](/server/framework/atlassian-sdk/run-your-plugin-in-the-container)
-   [Control access with SAL](/server/framework/atlassian-sdk/control-access-with-sal)
-   [Create a GUI with templates and AUI](/server/framework/atlassian-sdk/create-a-gui-with-templates-and-aui)
-   [Store and retrieve plugin data](/server/framework/atlassian-sdk/store-and-retrieve-plugin-data)

## How to work through the tutorial

This tutorial builds on the concepts introduced in [Set Up the Atlassian SDK and Build a Project](https://developer.atlassian.com/display/DOCS/Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project). This tutorial delves deeper into the SDK environment and so to complete this tutorial successfully, you should have already installed the SDK and created a plugin project. 

You should work through this tutorial sequentially since each page builds on the last. At the end of each page is a **Next Steps **heading that tells you where to go next.

**About these instructions**

|                     |               |
|---------------------|---------------|
| Level of experience | BEGINNER      |
| Time estimate       | 2:00          |
| OS and IDE          | ANY SUPPORTED |

**  
**

**Plugin Source**

We encourage you to work through the tutorial. If you'd like to skip ahead or check your work when you're done, you can find the plugin source on Atlassian Bitbucket. Bitbucket serves as a public Git repository containing the tutorial's source code. To clone the repository for this plugin, issue the following command: 

``` bash
git clone https://bitbucket.org/atlassian_tutorial/learn-development-platform-by-example-plugin-tutorial.git
```

Alternatively, you can <a href="https://bitbucket.org/atlassian_tutorial/learn-development-platform-by-example-plugin-tutorial/get/master.zip" class="external-link">download the source code</a> for this plugin project.

## [Start the tutorial &gt;&gt;](/server/framework/atlassian-sdk/create-a-plugin-skeleton) 

##

















































