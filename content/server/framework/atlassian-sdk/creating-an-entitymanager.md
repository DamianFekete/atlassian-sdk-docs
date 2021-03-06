---
aliases:
- /server/framework/atlassian-sdk/creating-an-entitymanager-5669141.html
- /server/framework/atlassian-sdk/creating-an-entitymanager-5669141.md
category: devguide
confluence_id: 5669141
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669141
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669141
date: '2017-12-08'
guides: guides
legacy_title: Creating an EntityManager
platform: server
product: atlassian-sdk
subcategory: learning
title: Creating an EntityManager
---
# Creating an EntityManager

The `EntityManager` is the corner stone of Active Objects.

The simplest way to create and configure an entity manager is by using the `net.java.ao.builder.EntityManagerBuilder`:

``` java
EntityManager entityManager = EntityManagerBuilder
                .url(jdbcProperties.url) // the JDBC url for database connection
                .username(jdbcProperties.username) 
                .password(jdbcProperties.passord)
                .auto() // configuring the connection pool, auto detects connection pools on the classpath
                .useWeakCache() // an option to use weak caches
                .build(); // actually builds the entity manager
```

That's all there is to it.

This example is obviously extracted from the the <a href="https://bitbucket.org/activeobjects/ao-dogfood-blog/src/9958325ad566/src/main/java/net/java/ao/blog/BlogApplication.java#cl-92" class="external-link">dog food blog</a>.

{{% tip %}}

When in an Atlassian plugin

There is no need for you to create your own entity manager, this is handled by the Active Objects plugin.

{{% /tip %}}
