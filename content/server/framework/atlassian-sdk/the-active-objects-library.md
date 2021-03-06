---
aliases:
- /server/framework/atlassian-sdk/the-active-objects-library-5669139.html
- /server/framework/atlassian-sdk/the-active-objects-library-5669139.md
category: devguide
confluence_id: 5669139
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669139
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669139
date: '2017-12-08'
guides: guides
legacy_title: The Active Objects Library
platform: server
product: atlassian-sdk
subcategory: learning
title: The Active Objects library
---
# The Active Objects library

This documentation relates to the Active Objects library outside the scope of the Atlassian plugin framework. Everything documented under this page hierarchy should also apply to using Active Objects within your Atlassian plugin. See the [plugin](https://developer.atlassian.com/display/AO/Configuring+the+Plugin) section for usage of Active Objects that are specific to plugins.

When relevant pages will reference documentation in the [plugin](https://developer.atlassian.com/display/AO/Configuring+the+Plugin) section. Also there might be from time to time inline tips relevant when using Active Objects within a plugin. They will be shown as below:

{{% tip %}}

When in an Atlassian plugin

*Here will be a tip when using a particular feature of Active Objects within an Atlassian plugin.*

{{% /tip %}}

Here is the content of this documentation:

-   [Creating an EntityManager](/server/framework/atlassian-sdk/creating-an-entitymanager)
-   [Creating Entities](/server/framework/atlassian-sdk/creating-entities)
-   [Deleting Entities](/server/framework/atlassian-sdk/deleting-entities)
-   [Finding Entities](/server/framework/atlassian-sdk/finding-entities)
-   [Getting entities by PK](/server/framework/atlassian-sdk/getting-entities-by-pk)
-   [ManyToMany Relationship](/server/framework/atlassian-sdk/manytomany-relationship)
-   [OneToMany Relationship](/server/framework/atlassian-sdk/onetomany-relationship)
-   [OneToOne Relationship](/server/framework/atlassian-sdk/onetoone-relationship)
-   [Testing](/server/framework/atlassian-sdk/testing)

### Some code…

A lot of the documentation in this section references the DogFood blog. It is a very simple blog webapp developed with Active Objects.

I suggest you clone and check out the code available on BitBucket:

-   **<a href="https://bitbucket.org/activeobjects/ao-dogfood-blog" class="uri external-link">bitbucket.org/activeobjects/ao-dogfood-blog</a>**

### References

-   <a href="http://java.net/projects/activeobjects" class="uri external-link">java.net/projects/activeobjects</a>, this is the Active Objects project on `java.net`. The library is also documented there to some extent.
-   <a href="https://bitbucket.org/activeobjects/" class="uri external-link">bitbucket.org/activeobjects/</a>, this is the Active Objects account on BitBucket. A migration of the whole project (i.e. the library) is in the works and ultimately we see all of Active Objects (the library) resources be available there.
