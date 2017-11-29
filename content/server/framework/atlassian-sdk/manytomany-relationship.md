---
aliases:
- /server/framework/atlassian-sdk/manytomany-relationship-5669155.html
- /server/framework/atlassian-sdk/manytomany-relationship-5669155.md
category: devguide
confluence_id: 5669155
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669155
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669155
learning: patterns
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/developing-your-plugin-with-active-objects/the-active-objects-library/manytomany-relationship
new_url: /server/framework/atlassian-sdk/manytomany-relationship
platform: server
product: atlassian-sdk
subcategory: learning
title: ManyToMany relationship
---
# ManyToMany relationship

In ActiveObjects many to many relationships are defined thanks to the `net.java.ao.ManyToMany` annotation. It also requires another entity that links both sides of the many to many relationship.

Let's have a look at an example of such relation ship in the <a href="https://bitbucket.org/activeobjects/ao-dogfood-blog" class="external-link">DogFood blog</a>. The relationship is defined between posts (of type `Post`) and labels (of type `Label`).

**Post.java**

``` java
public interface Post extends Entity
{
    ...
    @ManyToMany(value = PostToLabel.class)
    public Label[] getLabels();
    ...
}
```

**Label.java**

``` java
public interface Label extends Entity
{
    ...
    @ManyToMany(value = PostToLabel.class)
    public Post[] getPosts();
}
```

Note how posts and labels both reference each other, but no *setter* exists. Also the `@ManyToMany` annotation defines a third `Entity` of type `PostToLabel`:

**PostToLabel**

``` java
public interface PostToLabel extends Entity
{
    public void setPost(Post post);
    public Post getPost();

    public void setLabel(Label label);
    public Label getLabel();
}
```

There is no annotation here. However this class clearly defines a relationship between a `Post` and a `Label`.

Actually associating a post to a label and persisting this association is as simple as:

``` java
private void associatePostToLabel(Post post, Label label) throws SQLException
{
    final PostToLabel postToLabel = entityManager.create(PostToLabel.class);
    postToLabel.setPost(post);
    postToLabel.setLabel(label);
    postToLabel.save();
}
```

You can see this code in the <a href="https://bitbucket.org/activeobjects/ao-dogfood-blog/src/ddf99719cef6/src/main/java/net/java/ao/blog/service/AoBlogService.java#cl-70" class="external-link"><code>BlogService</code> of the DogFood blog</a>.

### New attributes on entity annotations in Active Objects 0.22.1

The <a href="https://developer.atlassian.com/display/DOCS/OneToOne+Relationship" class="external-link">OneToOne</a>, <a href="https://developer.atlassian.com/display/DOCS/OneToMany+Relationship" class="external-link">OneToMany</a> and <a href="https://developer.atlassian.com/display/DOCS/ManyToMany+Relationship" class="external-link">ManyToMany</a> annotations are used to define relationships in Active Objects. If you have used one of these to annotate a method as one end of a relationship, you can now set an attribute(s) that specifies the method on the remote end of the relationship. In versions prior to 0.22.1, Active Objects would attempt to infer the method by the type, which did not work in all situations.

-   **ManyToMany annotation**: New "**reverse**" and "**through**" attributes. Set the "reverse" attribute to the name of the corresponding getter on the intermediate interface. Set the "through" attribute to the name of the getter on the intermediate interface that refers to the remote interface.

If you do not set these attributes, Active Objects will revert to inferring the method by type. However, in a future upgrade, specifying these attributes will be required.

*Note, the Active Objects plugin was upgraded to 0.22.1 in JIRA 6.1.*









































































































































































































































































































