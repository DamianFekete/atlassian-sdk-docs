---
aliases:
- /server/framework/atlassian-sdk/developing-your-plugin-with-active-objects-5669137.html
- /server/framework/atlassian-sdk/developing-your-plugin-with-active-objects-5669137.md
category: devguide
confluence_id: 5669137
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669137
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669137
date: '2017-12-08'
guides: guides
legacy_title: Developing your plugin with Active Objects
platform: server
product: atlassian-sdk
subcategory: learning
title: Developing your plugin with Active Objects
---
# Developing your plugin with Active Objects

Here you will find all the documentation you need to develop your Active Objects plugin. This documentation is composed of two main parts:

-   [The library](/server/framework/atlassian-sdk/the-active-objects-library), which describes how one would use the Active Objects library to persist, retrieve and manipulate data from a given database. This part should be independent of any usage of Active Objects within the plugin system.
-   [The plugin](https://developer.atlassian.com/display/AO/Configuring+the+Plugin), which describes how one uses Active Objects in an Atlassian plugin. Principles learnt in the previous section should apply to plugins as well. There might be additional constraints when running within the plugin framework that will be clearly identified here.

For the impatient, there is **[getting started](/server/framework/atlassian-sdk/getting-started-with-active-objects)** information that you can follow to **create your first Active Objects plugin**. It should give you the basics for writing your own plugin and then coming back to the rest of the documentation you should be able to augment the functionality of your plugin easily.

Of course, there is also an [Active Objects FAQ](/server/framework/atlassian-sdk/active-objects-faq) with simple and straight to the point answers to the most commonly asked questions. Questions there will refer to other parts of the documentation for more comprehensive information about the topic at hand.

{{% note %}}

BLOBs and Active Object plugins

Currently, Atlassian's Active Object framework does not support binary large objects (BLOBs). Plugins that work with BLOBs fail. Until there is full support, do not write AO plugins that manipulate BLOBs.

{{% /note %}}

Here is a table of content of the documentation you can find:

-   [The Active Objects Library](/server/framework/atlassian-sdk/the-active-objects-library) -- Using the Active Objects library
    -   [Creating an EntityManager](/server/framework/atlassian-sdk/creating-an-entitymanager)
    -   [Creating Entities](/server/framework/atlassian-sdk/creating-entities)
    -   [Deleting Entities](/server/framework/atlassian-sdk/deleting-entities)
    -   [Finding Entities](/server/framework/atlassian-sdk/finding-entities)
    -   [Getting entities by PK](/server/framework/atlassian-sdk/getting-entities-by-pk)
    -   [ManyToMany Relationship](/server/framework/atlassian-sdk/manytomany-relationship)
    -   [OneToMany Relationship](/server/framework/atlassian-sdk/onetomany-relationship)
    -   [OneToOne Relationship](/server/framework/atlassian-sdk/onetoone-relationship)
    -   [Testing](/server/framework/atlassian-sdk/testing)
-   [Active Objects FAQ](/server/framework/atlassian-sdk/active-objects-faq) -- This page should answer the most commonly asked question about developing a plugin using Active Objects
    -   [Table names](/server/framework/atlassian-sdk/table-names) -- How are database tables named?
    -   [Column names](/server/framework/atlassian-sdk/column-names) -- How are database columns named?
    -   [Enabling SQL logging](/server/framework/atlassian-sdk/enabling-sql-logging) -- How do I enable/disable SQL logging for Active Objects, the library and the plugin?
-   [Testing a plugin that uses Active Objects](/server/framework/atlassian-sdk/testing-a-plugin-that-uses-active-objects)
-   [Configuring the Plugin](/server/framework/atlassian-sdk/configuring-the-plugin)
    -   [Configuring your project](/server/framework/atlassian-sdk/configuring-your-project)
    -   [Adding the maven dependency](/server/framework/atlassian-sdk/adding-the-maven-dependency)
    -   [Active Objects Plugin Module](/server/framework/atlassian-sdk/active-objects-plugin-module) -- The Active Objects plugin module allows you to use the Active Objects service to persist data using the Active Objects library http://activeobjects.java.net.
-   [Upgrading your plugin and handling data model updates](/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates) -- Sometimes your data model will evolve. This page will describe how to handle upgrades for various use cases of model changes.
-   [Best practices for developing with Active Objects](/server/framework/atlassian-sdk/best-practices-for-developing-with-active-objects)
