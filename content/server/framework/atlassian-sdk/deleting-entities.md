---
aliases:
- /server/framework/atlassian-sdk/deleting-entities-5669149.html
- /server/framework/atlassian-sdk/deleting-entities-5669149.md
category: devguide
confluence_id: 5669149
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669149
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669149
date: '2017-12-08'
guides: guides
legacy_title: Deleting Entities
platform: server
product: atlassian-sdk
subcategory: learning
title: Deleting entities
---
# Deleting entities

When using Active Objects, deleting an entity requires that you have a reference to that entity. Of course we will be using the `EntityManager`. The actual method is `net.java.ao.EntityManager#delete(RawEntity<?>...)`:

``` java
private void deleteBlog(Blog blog) throws SQLException
{
    entityManager.delete(blog);
}
```

Note that the delete method take a vararg argument so it is possible to delete several entities at once.
