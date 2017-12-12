---
aliases:
- /server/framework/atlassian-sdk/creating-entities-5669143.html
- /server/framework/atlassian-sdk/creating-entities-5669143.md
category: devguide
confluence_id: 5669143
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669143
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669143
date: '2017-12-08'
guides: guides
legacy_title: Creating Entities
platform: server
product: atlassian-sdk
subcategory: learning
title: Creating entities
---
# Creating entities

## Defining an entity

In Active Objects an entity is defined by an interface that extends the `net.java.ao.RawEntity<T>` interface. Here `T` defines the type of the primary key used for the entity.

In most cases, and this is advised to do so, your interfaces will extends `net.java.ao.Entity` instead of extending directly `net.java.ao.RawEntity<T>`. This interface defines for you the primary key as an `Integer`.

`Entity` is defined as follow:

``` java
public interface Entity extends RawEntity<Integer>
{
    @AutoIncrement
    @NotNull
    @PrimaryKey("ID")
    public int getID();
}
```

Annotations here are self explanatory, but for good measure:

-   `@NotNull` means that this member cannot be persisted as `null`,
-   `@PrimaryKey` defines this member as the primary key of the entity, with the (column) name `ID`,
-   `@AutoIncrement` tells that the primary key is an auto generated integer.

Here is a simple example of an entity that extends this class. This code is an extract from the <a href="https://bitbucket.org/activeobjects/ao-dogfood-blog/src/9958325ad566/src/main/java/net/java/ao/blog/db/Blog.java" class="external-link">dogfood blog</a>:

``` java
public interface Blog extends Entity
{
    public String getName();
    public void setName(String name);
}
```

Active Objects will take care of naming the table and column names according to the name of the interface and methods.

## Creating an entity

Once an entity is defined, creating and persisting an object represented by that entity is very simple, given an `EntityManager`:

``` java
private Blog createBlog() throws SQLException
{
    final Blog blog = entityManager.create(Blog.class); 
    blog.setName("Active Objects Dog Food Blog");
    blog.save();
    return blog;
}
```

This code can be found in the <a href="https://bitbucket.org/activeobjects/ao-dogfood-blog/src/9958325ad566/src/main/java/net/java/ao/blog/service/AoBlogService.java#cl-125" class="external-link">BlogService implementation of the DogFood blog</a>

## Creating an entity with "not null"-constraints

The previous way of creating an entity works only as long as there are no "not null"-constraints on fields other than the primary key. Consider the case of someone adding a field to the sample entity:

``` java
public interface Blog extends Entity
{
    public String getName();
    public void setName(String name);

    @NotNull
    public String getAuthor();
    public void setAuthor(String author);
}
```

Now, calling `entityManager.create(Blog.class);` will not work, since the `author` field needs to be provided. The `create` call accepts parameters as well, so the code would look like this:

``` java
private Blog createBlog() throws SQLException
{     
    return entityManager.create(
        Blog.class, 
        new DBParam("NAME", "Active Objects Dog Food Blog"),
        new DBParam("AUTHOR", "Dog Blogger")
    );
}
```

The column names are used here, so they must conform to the [Column names](/server/framework/atlassian-sdk/column-names) convention.








































































































































































































































































































































