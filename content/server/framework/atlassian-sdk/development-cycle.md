---
aliases:
- /server/framework/atlassian-sdk/development-cycle-18252617.html
- /server/framework/atlassian-sdk/development-cycle-18252617.md
category: devguide
confluence_id: 18252617
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=18252617
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=18252617
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/development-cycle
new_url: /server/framework/atlassian-sdk/development-cycle
platform: server
product: atlassian-sdk
subcategory: learning
title: Development cycle
---
# Development cycle

In its simplest form, a deployable plugin consists of the following components packaged in a single JAR file:

-   A plugin descriptor, `atlassian-plugin.xml`, that enables the plugin module in your host application, such as JIRA or Confluence.
-   Java classes encapsulating the plugin logic.
-   Resource files such as string files or templates for displaying the plugin UI, if required by the plugin.

Fortunately, you don't have to try to develop these by hand. You can create them using the Atlassian Plugin SDK. Before starting, please make sure that you have set up your development environment and installed the Atlassian Plugin SDK, as described in the [installation guide](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project). Now you can start building your plugin. This page is for you if:

-   You have a working Java development environment
-   You have a working Atlassian Plugin SDK installed and configured

If you don't feel ready to proceed, please check our guide to [starting with the Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

## Steps in the Process

**[![](/server/framework/atlassian-sdk/images/1.png)](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project-2818660.html)[Develop](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project)**: Create your plugin from an archetype (template) and use the awesome Atlassian tools that make plugin development a breeze. Click through to the tutorials on specific plugin types.

![](/server/framework/atlassian-sdk/images/2.png)**[Test](https://developer.atlassian.com/pages/viewpage.action?pageId=2818653)**: Find out how to include automated tests for your plugin. In our quest for quality, we encourage plugin developers to supply unit and functional tests with a significant amount of code coverage.

![](/server/framework/atlassian-sdk/images/3.png)**[Package & Release](/server/framework/atlassian-sdk/packaging-and-releasing-your-plugin)**: Share your killer plugin with the world. Read about licensing, plugin repositories, issue trackers, documentation and how to announce your plugin.

 

## Java in Atlassian applications

Atlassian applications require Java 1.5 or higher.

## The Atlassian plugin system

Atlassian products provide a plugin system which allows developers to extend or alter the product:

-   The plugin system contains an *OSGi container*, and plugins are understood as *bundles* inside that container.
-   A *bundle* is a standard .jar file that contains extra OSGi instructions in the manifest.
-   OSGi insulates bundles from each other, primarily by guaranteeing that each bundle has its own classloader. This buys you several good things, including:
    -   **Predictable class importing**: You know that the library your code is using at runtime is the one you supplied with it
    -   **Talk to other plugins**: Communicate with other plugins; extend them or use their power for your own ends
    -   **Multiple versions**: Have several versions of the same library or plugin active at once; you don't need to upgrade just because someone else does

For more information on the plugin framework, see [its home page](/server/framework/atlassian-sdk/plugin-framework).

## Plugin modules

Each product exposes a number of **plugin modules**; some defined by the plugin framework (and thus common to all Atlassian products) and some defined by the product itself. (For example, all products support a servlet plugin module, which allows developers to write a JEE servlet and have it hosted by the product when the plugin is installed. Confluence alone provides a macro plugin module, which allows developers to create custom wiki markup/XHTML elements that will be rendered at page display time.) It is also possible to create your own plugin modules.

All plugin modules are listed in the [Plugin Module Index](/server/framework/atlassian-sdk/plugin-module-index), which will give you an idea of what is possible with the builtin plugin modules and direct you to detailed instructions on how to write with them.

## Security considerations

It is easy to overlook vulnerabilities in your code if this is the first time you write a plugin. These, in turn, can introduce security vulnerabilities into the product you plug into.

We have created several APIs to be used for securing your plugins. See this AtlasCamp 2010 <a href="http://confluence.atlassian.com/display/ATL/Securing+your+Plugin" class="external-link">presentation</a> for advice on how to use these APIs and practices.

You can find information on our Javadoc [here](/server/framework/atlassian-sdk/atlassian-javadoc).

## Plugin Developer Best Practices

We've collected a page of best practices for plugin developers. Everybody should know these [important tips](/server/framework/atlassian-sdk/best-practices).

## Plugin and Gadget Gotchas

Have a problem you just can't explain? Find some likely solutions [here](/server/framework/atlassian-sdk/troubleshooting).

## Product development hubs

After getting acquainted with cross-product development information here, see product-specific information at the respective product development hub:

-   <https://developer.atlassian.com/display/JIRADEV>
-   <https://developer.atlassian.com/display/CONFCLOUD>
-   <https://developer.atlassian.com/display/BAMBOODEV>
-   <https://developer.atlassian.com/display/FECRUDEV>
-   <https://developer.atlassian.com/display/CROWDDEV>






































































































































































































































