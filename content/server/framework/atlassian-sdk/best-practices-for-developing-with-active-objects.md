---
aliases:
- /server/framework/atlassian-sdk/best-practices-for-developing-with-active-objects-8946892.html
- /server/framework/atlassian-sdk/best-practices-for-developing-with-active-objects-8946892.md
category: devguide
confluence_id: 8946892
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8946892
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8946892
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/developing-your-plugin-with-active-objects/best-practices-for-developing-with-active-objects
new_url: /server/framework/atlassian-sdk/best-practices-for-developing-with-active-objects
platform: server
product: atlassian-sdk
subcategory: learning
title: Best practices for developing with Active Objects
---
# Best practices for developing with Active Objects

This page contains some guidelines for best practices when developing a plugin that uses the Atlassian [Active Objects](https://developer.atlassian.com/display/AO/Active+Objects) (AO) plugin to store and retrieve data. The information takes the form of a quick reference sheet with links to pages containing further information.

**BLOB data**

Currently, the Atlassian Active Object framework does not support binary large objects (BLOBs). Plugins that work with BLOBs fail. Until there is full support, do not write AO plugins that manipulate BLOBs.

**Specify table names in annotations**

Use the `@Table` annotation to specify your table names so that you can freely rename the entity interface. For example, `@Table("MyEntity")`. See [Upgrading your plugin and handling data model updates](/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates).

**Do not remove column names from Java code on upgrade**

 When upgrading your plugin to a new version, do not remove columns unless you are aware of the consequences. Active Objects will make the database match the entity interface in the Java code. It alters tables to match the current interface. Removing columns will result in data loss. For that reason, we recommend that you do not delete tables or columns, only add them. See [Upgrading your plugin and handling data model updates](/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates). 

If your plugin needs a different table structure after the upgrade, your upgrade task should:

-   Define a new table.
-   Copy the data into the new structure.
-   Move the old interface to an upgrade task "attic". For example, put the old Java code into a package with a name like 'old' or 'archive'. It is safer never to remove this code, because you do not know which old version of your plugin people are upgrading from. They may need the archived code in order for the upgrade task to run.

**Take care when renaming entities**

The Active Objects framework does not know about renaming. So if you change the name of an entity, it will remove the other entity and create a new one. All the data in the entity will be lost. See [Upgrading your plugin and handling data model updates](/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates).

**When changing data type, migrate the data as part of the upgrade process**

When migrating from one data type to another, the recommended approach is not to use an in-place type conversion. Instead, create a new column and migrate the data during the upgrade process. See [Upgrading your plugin and handling data model updates](/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates).

**Column names are case-sensitive**

If you need to specify the raw column names in create or find operations, letter case is important. See [Column names](/server/framework/atlassian-sdk/column-names).

**Column names should be in quotes**

 Active Objects doesn't automatically add quotes to column names in ORDER BY clauses. Depending on which database you are using, this may cause errors. For instance, this works on HSQLDB (the SDK default), but it does not work in PostgreSQL.

To avoid errors, we recommend that you always put column names within quotes in your ORDER BY statements, such as:

ORDER BY "COLUMN\_NAME"

**Use 'stream' rather than 'find' or 'get' methods for large amounts of data**

 When reading a large amount of data, do not use the 'find' of 'get' methods. Instead, use the 'stream' methods. See this blog post: <a href="http://blogs.atlassian.com/2011/09/activeobjects_streaming_api/" class="external-link">ActiveObjects streaming API</a>.

The 'find' and 'get' methods read everything into memory as editable AO objects, which is very memory intensive. The 'stream' methods return read-only objects, which are cheaper to create, and give them to you one-by-one.

**Delete all related data in the right order**

When deleting object graphs, or data from related tables, you will need to delete them in the right order. Make sure you delete the children before the parents. AO does not support cascading.

**Use lazy initialisation with synchronisation**

The Active Objects framework cannot be used during plugin startup. The easiest way to get around this is to perform any initialisation tasks only during the first HTTP request. As ActiveObjects service is not thread-safe during first call, it is also important to ensure other HTTP request threads are blocked while initialisation is being performed.

## Community-Authored Guidelines

**Operators must be space-delimited in WHERE clauses**

When using an operator in a `WHERE` clause (such as the equals ("=") operator or the greater than ("&gt;") operator, spaces must be used to separate the operator from its operands. In other words, the following code is incorrect:

Wrong

``` java
Query.select().where("FOO='bar'");
```

While this code is correct:

Right

``` java
Query.select().where("FOO = 'bar'");
```

**Column names in WHERE clauses must be in upper case**

Mixed or lower-case column names in the `WHERE` clause will cause errors when running on PostgreSQL.

**Boolean literals in WHERE clauses**

Do not embed the boolean literal string `TRUE` or `FALSE` in a WHERE clause using Active Objects. This may cause incompatibilities with Microsoft SQL Server, such as the following error:

``` java
java.sql.SQLException: Invalid column name 'TRUE'.
```

Instead, use a substitution variable and supply the value `Boolean.TRUE` or `Boolean.FALSE`, like so: 

``` java
Query.select().where("SOME_COLUMN IS ?", Boolean.TRUE);
```

See <a href="https://answers.atlassian.com/questions/216174/active-objects-mssql-boolean-issue" class="external-link">this question</a> on Atlassian Answers for more detail.

##### RELATED TOPICS

[Active Objects](https://developer.atlassian.com/display/AO/Active+Objects)





















































































































































































































































































































