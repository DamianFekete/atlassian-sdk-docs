---
aliases:
- /server/framework/atlassian-sdk/onetomany-relationship-5669153.html
- /server/framework/atlassian-sdk/onetomany-relationship-5669153.md
category: devguide
confluence_id: 5669153
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669153
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669153
date: '2017-12-08'
guides: guides
legacy_title: OneToMany Relationship
platform: server
product: atlassian-sdk
subcategory: learning
title: OneToMany relationship
---
# OneToMany relationship

In ActiveObjects one to many relationships are defined thanks to the `net.java.ao.OneToMany` annotation.

In the DogFood blog there is such a relationship between posts (of type `Post`) and comments (of type `Comment`).

**Post.java**

``` java
public interface Post extends Entity
{
    ...
    @OneToMany
    public Comment[] getComments();
    ...
}
```

**Comment.java**

``` java
public interface Comment extends Entity
{
    ...
    public Post getPost();
    public void setPost(Post post);
    ...
}
```

Adding a `Comment` to a `Post` requires writing this type of code:

**Adding a comment**

``` java
public Comment addComment(Post post, String author, String comment) throws SQLException
{
    final Comment c = entityManager.create(Comment.class);

    c.setPost(post); // setting the relationship

    c.setName(author);
    c.setComment(comment);
    c.save();
    return c;
}
```

### New attributes on entity annotations in Active Objects 0.22.1

The <a href="https://developer.atlassian.com/display/DOCS/OneToOne+Relationship" class="external-link">OneToOne</a>, <a href="https://developer.atlassian.com/display/DOCS/OneToMany+Relationship" class="external-link">OneToMany</a> and <a href="https://developer.atlassian.com/display/DOCS/ManyToMany+Relationship" class="external-link">ManyToMany</a> annotations are used to define relationships in Active Objects. If you have used one of these to annotate a method as one end of a relationship, you can now set an attribute(s) that specifies the method on the remote end of the relationship. In versions prior to 0.22.1, Active Objects would attempt to infer the method by the type, which did not work in all situations.

-   **OneToOne and OneToMany annotations**: New "**reverse**" attribute. Set this to the name of the corresponding getter on the remote interface.

If you do not set these attributes, Active Objects will revert to inferring the method by type. However, in a future upgrade, specifying these attributes will be required.

*Note, the Active Objects plugin was upgraded to 0.22.1 in JIRA 6.1.*
