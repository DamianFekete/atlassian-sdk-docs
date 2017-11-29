---
aliases:
- /server/framework/atlassian-sdk/column-names-5669191.html
- /server/framework/atlassian-sdk/column-names-5669191.md
category: devguide
confluence_id: 5669191
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669191
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669191
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/developing-your-plugin-with-active-objects/active-objects-faq/column-names
new_url: /server/framework/atlassian-sdk/column-names
platform: server
product: atlassian-sdk
subcategory: learning
title: Column names
---
# Column names

How are database columns named?Let's take the example of an entity which class name is `MyObject` with a method `getSomeAttribute`. This field will have a column named **SOME\_ATTRIBUTE**. The naming convention is simply that we take the name of the field according to Java Beans convention, separated with `_` and all upper case.

Foreign key columns follow the same convention, but end with `_ID`. Using the same example of SomeAttribute, the column name would be **SOME\_ATTRIBUTE\_ID**.

You can also specify the column name you'd like to use through either the `net.java.ao.Accessor` or `net.java.ao.Mutator` annotation. Note that the value defined in the annotation will still be processed in the same way a method name would be processed.  
So if you set the value as `SomeAttribute`, the column will be named **SOME\_ATTRIBUTE**.

# Constraints

Column names (once transformed) can not be more than 30 characters long. This is an Oracle restriction that is take in account whatever database one works with to provide consistency across all supported databases.

Further more (transformed) column names cannot use any of the following reserved words: **BLOB**, **CLOB**, **NUMBER**, **ROWID**, **TIMESTAMP**, **VARCHAR2**.

This also applies to trigger names and sequence names, which are used by Oracle 11g to emulate autoincrement for primary keys (ids) for Active Objects.








