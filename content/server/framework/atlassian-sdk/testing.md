---
aliases:
- /server/framework/atlassian-sdk/testing-5669157.html
- /server/framework/atlassian-sdk/testing-5669157.md
category: devguide
confluence_id: 5669157
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669157
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669157
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: Testing 5669157
---
# Testing

Active Objects integrates with JUnit to make your entity testing easy.

The first thing to do is add a dependency to your project. When using <a href="http://maven.apache.org" class="external-link">Maven</a>, this means:

**Testing dependencies**

``` xml
<dependency>
  <groupId>junit</groupId>
  <artifactId>junit</artifactId>
  <version>4.8.1</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>net.java.dev.activeobjects</groupId>
  <artifactId>activeobjects-test</artifactId>
  <version>${ao.version}</version>
  <scope>test</scope>
</dependency>
```

Tests of Active Objects entities look like the following, taken from the <a href="https://bitbucket.org/activeobjects/ao-dogfood-blog/src/0ef36bfaf6c3/src/test/java/net/java/ao/blog/service/AoBlogServiceTest.java" class="external-link">DogFood blog</a>:

**Testing Active Objects**

``` java
@RunWith(ActiveObjectsJUnitRunner.class) // (1)
@Data(AoBlogServiceTest.AoBlogServiceTestDatabaseUpdater.class) // (2)
@Jdbc(DerbyEmbedded.class) // (3)
@NameConverters // (4)
public final class AoBlogServiceTest
{
    private EntityManager entityManager; // (5)

    private AoBlogService blogService;

    @Before
    public void setUp() throws Exception
    {
        blogService = new AoBlogService(entityManager);
    }

    @Test
    public void getBlogCreatesOneIfNecessary() throws Exception // (6)
    {
        assertEquals(0, entityManager.find(Blog.class).length); // no blogs
        assertNotNull(blogService.getBlog());
    }

    public static final class AoBlogServiceTestDatabaseUpdater implements DatabaseUpdater // (2)
    {
        @Override
        public void update(EntityManager entityManager) throws Exception
        {
            entityManager.migrate(Blog.class, Post.class, Comment.class, Label.class, PostToLabel.class);
        }
    }
}
```

1.  Using the `ActiveObjectsJUnitRunner` makes testing ActiveObjects entities easy.
2.  Specifying a `DatabaseUpdater` through the `@Data` annotation. It is implemented here as a static inner class (`AoBlogServiceTestDatabaseUpdater`). Its update method allows you to prepare the database for tests. It is called only once per class (or per set of classes with the same `DatabaseUpdater`).
3.  Specifying the database to use for testing, here an embedded Derby database. A convenient class to re-use for Maven users is the `net.java.ao.test.jdbc.DynamicJdbcConfiguration`, which will determine the database in use according to a System property. Combined with Maven profiles, it makes it easy to test against any database.
4.  Active Objects uses name converters to translate entity names and properties to table and column names. This `@NameConverters` annotation allows setting the converter used for tests. Here the defaults are used. Note that the annotation can be omitted.
5.  The `EntityManager` is injected by the `ActiveObjectsJUnitRunner`, which allows instantiating the class under test with a properly configured entity manager.
6.  A simple test. Note that all test methods are wrapped in a transaction that is rolled back after the method has been run. This will leave the database in the exact same state before each test, whatever happens within the individual test.

{{% tip %}}

When in an Atlassian plugin

Add another dependency to your test dependencies:

``` xml
<dependency>
  <groupId>com.atlassian.activeobjects</groupId>
  <artifactId>activeobjects-test</artifactId>
  <version>${ao.version}</version>
  <scope>test</scope>
</dependency>
```

This way it is possible to wrap the injected `EntityManager` in a `com.atlassian.activeobjects.test.TestActiveObjects` for testing the service of the plugin.

Another important point is to set proper name converters, as the Active Objects plugin is opinionated about this and tests should be run in the production condition. Configure your name converter this way:

``` java
@NameConverters(table = com.atlassian.activeobjects.test.TestActiveObjectsTableNameConverter
                field = com.atlassian.activeobjects.test.TestActiveObjectsFieldNameConverter)
```

**Note:** this is available from version 0.14.1 of the Active Objects plugin. It is possible to use version 0.14.1 of the test library even if the application is running an earlier version of the plugin.

{{% /tip %}}














































































































































































































































