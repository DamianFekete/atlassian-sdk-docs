---
title: About Plugins and Plugin Modules 2818372
aliases:
    - /server/framework/atlassian-sdk/about-plugins-and-plugin-modules-2818372.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818372
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818372
confluence_id: 2818372
platform:
product:
category:
subcategory:
---
# Documentation : About Plugins and Plugin Modules

External link to <a href="http://www.slate.com/" class="external-link">slate</a>.

The Java classes and the other components you write will depend on your plugin's host Atlassian application, and on the functionality of the plugin. A plugin consists of the following components, all contained within a single JAR file:

-   A plugin descriptor, `atlassian-plugin.xml`, that enables the plugin module in your host application, such as JIRA or Confluence.
-   Java classes encapsulating the plugin logic.
-   Resource files such as string files or templates for displaying the plugin UI, if required by the plugin.

You can create the initial project artifacts using the Atlassian Plugin SDK, as described in the next section.

## Getting started

The [Set up the Atlassian Plugin SDK and Build a Project](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project) tutorial describes how to get started creating Atlassian plugins. In a nutshell, the process for creating plugins is:

1.  Using the Atlassian Plugin SDK, run `atlas-create-APPLICATION-plugin`, where `APPLICATION` is the Atlassian application you are developing your plugin for. For example, run `atlas-create-confluence-plugin` or `atlas-create-jira-plugin`.
2.  Update your POM (Project Object Model definition file) to include some metadata about your plugin and your company or organisation:
    -   Edit the `pom.xml` file in the root directory of your plugin.
    -   Add your company or organisation name and your website to the `<organization>`element:

        ``` javascript
        <organization>
            <name>Example Company</name>
            <url>http://www.example.com/</url>
        </organization>
        ```

    -   Update the `<description>` element to describe what your plugin does.
    -   Check that the version of the Atlassian application specified in the `<properties>` section is the version that you want.
    -   Save the file.

3.  Use the SDK's plugin module generator to add the stubs of the plugin modules that will perform the functions required by your plugin. You will need one or more plugin modules, depending on the requirements of your plugin. There is more information about the available module types lower down on this page.
    -   Open a command window and go to the plugin root directory (where the `pom.xml` is located).
    -   Run `atlas-create-APPLICATION-plugin-module`, where `APPLICATION` is the Atlassian application you are developing your plugin for. For example, run `atlas-create-confluence-plugin-module` or `atlas-create-jira-plugin-module`.
    -   Supply the information about the module as prompted.
4.  The plugin module generator will add the required modules to the plugin descriptor at `src/main/resources/atlassian-plugin.xml`. Edit that file and adjust any settings as you like.
5.  The plugin module generator will also generate the stubs for your plugin modules in the Java code. Edit the plugin code in `src/main/java/`, updating and adding new classes as needed.
6.  Edit the unit and integration tests in `src/test/java/` to test your plugin's functionality. (Read more about [testing](/server/framework/atlassian-sdk/reloading-a-plugin-after-changes-2818373.html).)

## More about plugin modules

A plugin is made up of one or more modules. These modules define the various types of things that you can add to the host application. For example, JIRA has a custom field module type which you can use to add custom fields to JIRA. Confluence has a macro module type, used to define macros in Confluence. You put new modules into your plugin by adding a section to the `atlassian-plugin.xml` for each module and implementing the required classes.

When you add the modules with the SDK, the SDK handles both of these for you. In fact, the best way to learn how to develop plugins is to experiment with the SDK, and inspect what changes it makes when you add various types of modules to your project.

For details of the plugin module types available, refer to the developer documentation for your host application:

-   [Confluence](https://developer.atlassian.com/display/CONFDEV/Confluence+Plugin+Module+Types)
-   [JIRA](https://developer.atlassian.com/display/JIRADEV/About+JIRA+Plugin+Development)
-   [Crowd](https://developer.atlassian.com/display/CROWDDEV/Developing+Plugins+for+Crowd)
-   [Bamboo](https://developer.atlassian.com/display/BAMBOODEV/Bamboo+Plugin+Module+Types)
-   [FishEye/Crucible](https://developer.atlassian.com/display/FECRUDEV/Plugin+Module+Types)

See also information about the [common module types](/server/framework/atlassian-sdk/plugin-modules) available for plugins for any application. For more information about the plugin descriptor, see [Configuring the Plugin Descriptor](/server/framework/atlassian-sdk/configuring-the-plugin-descriptor).

















































































































































































































































































































