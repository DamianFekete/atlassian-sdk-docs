---
aliases:
- /server/framework/atlassian-sdk/enabling-sql-logging-5669194.html
- /server/framework/atlassian-sdk/enabling-sql-logging-5669194.md
category: devguide
confluence_id: 5669194
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669194
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669194
date: '2017-12-08'
guides: guides
legacy_title: Enabling SQL logging
platform: server
product: atlassian-sdk
subcategory: learning
title: Enabling SQL logging
---
# Enabling SQL logging

The Active Objects library uses <a href="http://www.slf4j.org/" class="external-link">SLF4J</a> for logging SQL statements. Namely it defines a logger named **`net.java.ao.sql`**.

When using the library, to enable the SQL logging, simply enable logging of the logger mentioned above in your preferred implementation of the SLF4J api at level **DEBUG**.

When using the plugin, simply configure the logger mentioned above at level **DEBUG** within your application's log administration.
