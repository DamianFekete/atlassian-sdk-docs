---
aliases:
- /server/framework/atlassian-sdk/onetoone-relationship-5669151.html
- /server/framework/atlassian-sdk/onetoone-relationship-5669151.md
category: devguide
confluence_id: 5669151
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669151
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669151
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/developing-your-plugin-with-active-objects/the-active-objects-library/onetoone-relationship
new_url: /server/framework/atlassian-sdk/onetoone-relationship
platform: server
product: atlassian-sdk
subcategory: learning
title: OneToOne relationship
---
# OneToOne relationship

In Active Objects a one to one relationship is defined thanks to the `net.java.ao.OneToOne` annotation.

In the DogFood blog there is such a relationship defined between the `Blog` and its `BlogConfiguration`:

**Blog.java**

``` java
public interface Blog extends Entity
{
    ...
    @OneToOne
    BlogConfiguration getConfiguration();
    ...
}
```

And here is how this is defined in the `BlogConfiguration`:

**BlogConfiguration.java**

``` java
public interface BlogConfiguration extends Entity
{
    void setBlog(Blog blog);
    Blog getBlog();
    ...
}
```

Then setting the relation ship is as simple as:

``` java
final BlogConfiguration configuration = entityManager.create(BlogConfiguration.class);
...
configuration.setBlog(blog); // setting the blog here
configuration.save();
```

 

### New attributes on entity annotations in Active Objects 0.22.1

The <a href="https://developer.atlassian.com/display/DOCS/OneToOne+Relationship" class="external-link">OneToOne</a>, <a href="https://developer.atlassian.com/display/DOCS/OneToMany+Relationship" class="external-link">OneToMany</a> and <a href="https://developer.atlassian.com/display/DOCS/ManyToMany+Relationship" class="external-link">ManyToMany</a> annotations are used to define relationships in Active Objects. If you have used one of these to annotate a method as one end of a relationship, you can now set an attribute(s) that specifies the method on the remote end of the relationship. In versions prior to 0.22.1, Active Objects would attempt to infer the method by the type, which did not work in all situations.

-   **OneToOne and OneToMany annotations**: New "**reverse**" attribute. Set this to the name of the corresponding getter on the remote interface.

If you do not set these attributes, Active Objects will revert to inferring the method by type. However, in a future upgrade, specifying these attributes will be required.

*Note, the Active Objects plugin was upgraded to 0.22.1 in JIRA 6.1.*















































































































































































































































