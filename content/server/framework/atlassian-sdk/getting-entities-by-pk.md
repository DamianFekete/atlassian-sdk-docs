---
aliases:
- /server/framework/atlassian-sdk/getting-entities-by-pk-5669145.html
- /server/framework/atlassian-sdk/getting-entities-by-pk-5669145.md
category: devguide
confluence_id: 5669145
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669145
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669145
date: '2017-12-08'
guides: guides
legacy_title: Getting entities by PK
platform: server
product: atlassian-sdk
subcategory: learning
title: Getting entities by PK
---
# Getting entities by PK

When using Active Objects, getting entities given their primary keys is very simple. Of course we will be using the `EntityManager`. The actual method is `net.java.ao.EntityManager#get(Class<T>, K...)`:

``` java
public Post getPost(int postId)
{
    return entityManager.get(Post.class, postId);
}
```

Note that the `get` method take a vararg argument so it is possible to get several entities at once by passing several primary keys to the method. It will then return an array of entities.

This code is a sample extract from the <a href="https://bitbucket.org/activeobjects/ao-dogfood-blog/src/9958325ad566/src/main/java/net/java/ao/blog/service/AoBlogService.java#cl-73" class="external-link">BlogService implementation of the DogFood blog</a>
