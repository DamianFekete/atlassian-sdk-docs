---
aliases:
- /server/framework/atlassian-sdk/ao-0.18.x-upgrade-guide-8946975.html
- /server/framework/atlassian-sdk/ao-0.18.x-upgrade-guide-8946975.md
category: devguide
confluence_id: 8946975
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8946975
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8946975
date: '2017-12-08'
guides: guides
legacy_title: AO 0.18.x Upgrade Guide
platform: server
product: atlassian-sdk
subcategory: learning
title: AO 0.18.x upgrade guide
---
# AO 0.18.x upgrade guide

{{% note %}}

Important information you should know


-   Active Objects 0.18.4 is the first AO version in this series that you should use. Previous versions had bugs that cause problems.
-   You can upgrade AO in JIRA 5 RC2 to do your testing. See [How to upgrade AO to 0.18.x in JIRA 5](/server/framework/atlassian-sdk/how-to-upgrade-ao-to-0-18-x-in-jira-5) (including Activity Streams upgrade).  
    AO 0.18.x is included in JIRA 5 RC3+ and the upgrade is longer be necessary.

{{% /note %}}

First of all, thank you for all of your help, your testing, and your feedback over the last several months. Because you have been willing to give the Developer Preview of AO a try, we're going to be able to provide a rock-solid data storage layer in the Atlassian Platform.

As you and we have continued to push this new technology forward, we've discovered some limitations in the way the underlying Java.net AO library was implemented. It didn't take as much care as needed to ensure that your data was 100% compatible with all of our supported database, or that we could move data from one database to another (i.e, through a backup/restore) with complete safety. Your bug reports and our testing helped uncover those problems.

Even though it's late in the development process, these kinds of bugs are serious. So we set out to eliminate them before we declare AO a stable part of the Atlassian Platform. We undertook a significant refactoring of the AO library two weeks ago. The first thing we did was increase the AO library's test suite by 400%, focusing especially on data type mappings, import/export, and migrations. That showed us some gaps, and we've spent the the time since slowly eliminating those gaps. These changes we made will necessitate some refactoring of your plugins, and that's what this guide is about. We understand that this will cause some additional work for you late in your dev process, and for that we apologize. However, in the long term, we believe these changes will significantly reduce the number of support problems for customers, so we can all spend more time building value and less time handling support.

### Type Changes

In order to ensure that your data will work no matter what database the user might have, we have limited AO to supported a certain list of SQL types. As such, if you're using a type not on the list below, you will need to refactor.

Also note that the table below denotes which types can be used as primary keys. An error will be thrown if you try to use an invalid primary key type.

<table style="width:100%;">
<colgroup>
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
<col style="width: 11%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Java Type</p></th>
<th><p>JDBC Type</p></th>
<th><p>HSQL</p></th>
<th><p>MySQL</p></th>
<th><p>Postgres</p></th>
<th><p>Oracle</p></th>
<th><p>SQL Server</p></th>
<th><p>Primary Key</p></th>
<th><p>Notes</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Boolean</p></td>
<td><p>BOOLEAN</p></td>
<td><p>BOOLEAN</p></td>
<td><p>BOOLEAN</p></td>
<td><p>BOOLEAN</p></td>
<td><p>NUMBER (1)</p></td>
<td><p>BIT</p></td>
<td><p>No</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>Integer</p></td>
<td><p>INTEGER</p></td>
<td><p>INTEGER</p></td>
<td><p>INTEGER</p></td>
<td><p>INTEGER</p></td>
<td><p>NUMBER (11)</p></td>
<td><p>INTEGER</p></td>
<td><p>Yes</p></td>
<td><p><strong>1</strong></p></td>
</tr>
<tr class="odd">
<td><p>Long</p></td>
<td><p>BIGINT</p></td>
<td><p>BIGINT</p></td>
<td><p>BIGINT</p></td>
<td><p>BIGINT</p></td>
<td><p>NUMBER (20)</p></td>
<td><p>BIGINT</p></td>
<td><p>Yes</p></td>
<td><p><strong>2</strong></p></td>
</tr>
<tr class="even">
<td><p>Double</p></td>
<td><p>DOUBLE</p></td>
<td><p>DOUBLE</p></td>
<td><p>DOUBLE</p></td>
<td><p>DOUBLE PRECISION</p></td>
<td><p>DOUBLE PRECISION</p></td>
<td><p>FLOAT</p></td>
<td><p>No</p></td>
<td><p> </p></td>
</tr>
<tr class="odd">
<td><p>java.util.Date</p></td>
<td><p>TIMESTAMP</p></td>
<td><p>DATETIME</p></td>
<td><p>DATETIME</p></td>
<td><p>TIMESTAMP</p></td>
<td><p>TIMESTAMP</p></td>
<td><p>DATETIME</p></td>
<td><p>No</p></td>
<td><p><strong>3</strong></p></td>
</tr>
<tr class="even">
<td><p>String</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>Yes</p></td>
<td><p><strong>4</strong></p></td>
</tr>
<tr class="odd">
<td><p>String (clob)</p></td>
<td><p>CLOB</p></td>
<td><p>LONG-VARCHAR</p></td>
<td><p>TEXT</p></td>
<td><p>TEXT</p></td>
<td><p>CLOB</p></td>
<td><p>NTEXT</p></td>
<td><p>No</p></td>
<td><p><strong>5</strong></p></td>
</tr>
<tr class="even">
<td><p>URL</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>Yes</p></td>
<td><p><strong>6</strong></p></td>
</tr>
<tr class="odd">
<td><p>URI</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>Yes</p></td>
<td><p><strong>7</strong></p></td>
</tr>
<tr class="even">
<td><p>Enum</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>VARCHAR</p></td>
<td><p>Yes</p></td>
<td><p><strong>8</strong></p></td>
</tr>
<tr class="odd">
<td><p>InputStream, byte[]</p></td>
<td><p>BLOB</p></td>
<td><p>BINARY</p></td>
<td><p>BLOB</p></td>
<td><p>BYTEA</p></td>
<td><p>BLOB</p></td>
<td><p>IMAGE</p></td>
<td><p>No</p></td>
<td><p> </p></td>
</tr>
<tr class="even">
<td><p>RawEntity&lt;?&gt;</p></td>
<td><p>varies</p></td>
<td><p>...</p></td>
<td><p>...</p></td>
<td><p>...</p></td>
<td><p>...</p></td>
<td><p>...</p></td>
<td><p> </p></td>
<td><p><strong>9</strong></p></td>
</tr>
</tbody>
</table>

#### Notes referred to in the table above

<table>
<colgroup>
<col style="width: 10%" />
<col style="width: 90%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p><strong>1.</strong></p></td>
<td><p>Postgres will use SERIAL when an Integer is used as an auto-incremented primary key, default in AO.</p></td>
</tr>
<tr class="even">
<td><p><strong>2.</strong></p></td>
<td><p>Postgres will use BIGSERIAL when an Integer is used as an auto-incremented primary key.</p></td>
</tr>
<tr class="odd">
<td><p><strong>3.</strong></p></td>
<td><p>Note that this is <strong><code>java.util.Date</code></strong> and not <code>java.sql.Date</code></p></td>
</tr>
<tr class="even">
<td><p><strong>4.</strong></p></td>
<td><p>Default max length is 255 and <strong>string cannot be empty</strong> (but can be null)</p></td>
</tr>
<tr class="odd">
<td><p><strong>5.</strong></p></td>
<td><p>Use <code>@StringLength</code> annotation</p></td>
</tr>
<tr class="even">
<td><p><strong>6.</strong></p></td>
<td><p>Default max length is 767</p></td>
</tr>
<tr class="odd">
<td><p><strong>7.</strong></p></td>
<td><p>Default max length is 767</p></td>
</tr>
<tr class="even">
<td><p><strong>8.</strong></p></td>
<td><p>Default max length is 255</p></td>
</tr>
<tr class="odd">
<td><p><strong>9.</strong></p></td>
<td><p>Dtored as whatever type the entity's primary key is</p></td>
</tr>
</tbody>
</table>

#### More notes

-   Enums used to be Integers but are now Strings.
-   Clobs are now defined via the `@StringLength` annotation.

#### Removed Types

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Removed Type</p></th>
<th><p>Refactor To</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>Character</p></td>
<td><p>String</p></td>
</tr>
<tr class="even">
<td><p>Calendar</p></td>
<td><p>Date</p></td>
</tr>
<tr class="odd">
<td><p>Timestamp</p></td>
<td><p>Date</p></td>
</tr>
<tr class="even">
<td><p>Float</p></td>
<td><p>Double</p></td>
</tr>
<tr class="odd">
<td><p>Real</p></td>
<td><p>Double</p></td>
</tr>
<tr class="even">
<td><p>SmallInt</p></td>
<td><p>Integer</p></td>
</tr>
<tr class="odd">
<td><p>GenericType</p></td>
<td><p>N/A</p></td>
</tr>
</tbody>
</table>

### Added `@StringLength`

This annotation can be used to override the default maximum string length for String, URL, URI, and Enum fields.

This is also the mechanism used to switch between VARCHAR and CLOB.

**examples:**

Not Annotated = VARCHAR(255)  
@StringLength(500) = VARCHAR(500)  
@StringLength(StringLength.UNLIMITED) = CLOB

Note that you cannot set a specific maximum length that is greater than 767. That is the greatest length that is always allowed for VARCHARs in all the supported databases (specifically, this limit is from MySQL).

### Removed Database Functions as `@Default` values

AO used to let you specify a databse function as the value for the `@Default` annotation. This was to enable using CURRENT\_DATE as a default value.

Due to the fact that database functions are implemented differently (if at all) and the fact that DATETIME does not support functions in most databases, **we have removed support for this**.

You can still use a string literal as a default value. e.g., `@Default("2011-11-11 12:34:56")`

### Removed `@OnUpdate` annotation

This annotation was used to set a value on a column everytime the entity was updated.

Essentially, the only thing that this was used for was to auto-update a timestamp field.

Since we no longer support database functions we removed this feature.

### New Reserved Words

In this new version, certain Oracle reserved keywords are no longer available to use for your table and column names. This applies to any database you're working against as obviously we(you) need to support all databases.

The reserved words are **BLOB, CLOB, NUMBER, ROWID, TIMESTAMP, VARCHAR2.**

The reason for doing this is that in order to support auto-increment IDs in Oracle we need to use triggers. Oracle has issues with triggers containing table or column names that also are keywords in some cases.

Note, this shouldn't affect your table names since AO prefixes table names of each plugin like this: `AO_XXXXXX_`, but it could affect your column names. So if you have columns named with one of those six words, you'll need to refactor.

We don't think these six words are likely to have been used, but if you find that you're affected by this change, please contact us and we'll try to find you a smooth transition.

### New Column Name Length Restriction

No database column name can have a length over 30 characters (the maximum length supported by Oracle). The AO plugin will validate table and column names at startup, when the AO module is first loaded.

### Removed `@SQLType`

The AO type system has gone through a major refactoring and now has a one-to-one mapping between Java and Database Types.

Due to this, we have removed the `@SQLType` annotation completely.

### Type system is now immutable

Previously, the type system was mutable and allowed plugins to add new type mappings. The new type system is immutable and plugins can no longer add types.

If you were relying on this "feature", you need to do some refactoring an only use the built-in supported types.

### Removed Test name converters in version 0.18.5

From version **0.18.5**, the test name converters are no longer available. The AO lib uses the correct strategy by default so no need to set any name converters when testing anymore.
