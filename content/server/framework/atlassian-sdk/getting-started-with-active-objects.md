---
aliases:
- /server/framework/atlassian-sdk/getting-started-with-active-objects-5669135.html
- /server/framework/atlassian-sdk/getting-started-with-active-objects-5669135.md
category: devguide
confluence_id: 5669135
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669135
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669135
date: '2017-12-08'
guides: tutorials
legacy_title: Getting Started with Active Objects
platform: server
product: atlassian-sdk
subcategory: learning
title: Getting started with Active Objects
---
# Getting started with Active Objects

<table>
<colgroup>
<col style="width: 30%" />
<col style="width: 70%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Applicable:</p></td>
<td><p>This tutorial applies to the Atlassian reference application (Refapp).</p></td>
</tr>
<tr class="even">
<td><p>Level of experience:</p></td>
<td><p>This is an intermediate tutorial. You should have completed at least one beginner tutorial before working through this tutorial.</p></td>
</tr>
<tr class="odd">
<td><p>Time estimate:</p></td>
<td><p>It should take you approximately 1 hour to complete this tutorial.</p></td>
</tr>
</tbody>
</table>

### Plugin source

We encourage you to work through this tutorial, and consult the source code when you run into trouble. This tutorial is split up into stages, where each stage is clearly marked in this documentation and we hope it will help you progress easily through this guide. 

The source repository can be found <a href="https://bitbucket.org/serverecosystem/ao-tutorial" class="external-link">here</a>. To clone the repository, issue the following command:

``` bash
git clone git@bitbucket.org:serverecosystem/ao-tutorial.git
```

There are tags corresponding to each stage of the tutorial, e.g. if you wanted to see the progress at the end of stage 3, do:

``` bash
git checkout stage3
```

## Step 1. Creating the plugin

For the purpose of this tutorial we're going to use the [Atlassian Refapp](/server/framework/atlassian-sdk/about-the-atlassian-refapp).

Creating the plugin, once the SDK is installed is as simple as running **`atlas-create-refapp-plugin`**, and answering the questions asked.

{{% note %}}

We're going to use the following values for this guide:

-   roupId: `com.atlassian.tutorial.ao.todo`
-   artifactId: **ao-tutorial**
-   version: **1.0.0-SNAPSHOT**
-   package: **com.atlassian.tutorial.ao.todo**

Note: You may need to use a different folder to the downloaded source to avoid conflict.

{{% /note %}}

{{% note %}}

The following instructions should apply to using Active Objects across Atlassian products, whether in JIRA, Confluence, Bamboo or the Refapp. There are some minor differences between the products, however. For example, the name of the plugin referenced in your `pom.xml` will differ, as it follows the pattern `maven-product-plugin`. See [Getting Started](/server/framework/atlassian-sdk/index) for common information on developing Atlassian plugins and using the SDK, or a particular product development space -- like [JIRA developer documentation](https://developer.atlassian.com/display/JIRADEV), or [Confluence Cloud](https://developer.atlassian.com/display/CONFCLOUD) or [Server](https://developer.atlassian.com/display/CONFDEV) -- for product-specific information, if necessary.

{{% /note %}}

## Step 2. Configuring your project

### Add the maven dependency

You only need to add one dependency to your plugin's `pom.xml` to enable Active Objects:

``` xml
<dependency>
  <groupId>com.atlassian.activeobjects</groupId>
  <artifactId>activeobjects-plugin</artifactId>
  <version>${ao.version}</version>
  <scope>provided</scope>
</dependency>
```

where `ao.version` is the version of Active Objects you're using.  Find a list of all the versions <a href="https://packages.atlassian.com/maven/repository/public/com/atlassian/activeobjects/activeobjects-plugin/" class="external-link">here</a>.

This tutorial was tested with version 1.2.3 of Active Objects.

### Add additional dependencies

You will need the following additional dependency to your `pom.xml`:

``` xml
<!-- Google Collections, useful utilities for manipulating collections -->
<dependency>
  <groupId>com.google.collections</groupId>
  <artifactId>google-collections</artifactId>
  <version>1.0</version>
  <scope>provided</scope>
</dependency>
```

{{% note %}}

Refapp version

Be sure to set the version of the Refapp to **2.9+**. If you're using a Plugin SDK prior to 3.3, it might not be new enough.

{{% /note %}}

## Step 3. Check Your Work

{{% tip %}}

Stage 1

We've now completed **stage 1** of this guide. Here is how to make sure that everything is working as expected:

-   Launch `atlas-run` from the command line, and you should see the following message:
    ``` text
    [INFO] refapp started successfully and available at http://localhost:5990/refapp
    [INFO] Type CTRL-C to exit
    ```
    Don't use `CTRL-C` to kill this instance! We will use `atlas-mvn package` to recompile our plugin and QuickReload will reload it for us, alleviating the need to restart refapp every time we make a change.

-   Go to the following URL <a href="http://localhost:5990/refapp/plugins/servlet/upm" class="uri external-link">localhost:5990/refapp/plugins/servlet/upm</a> (if asked to log in, use admin/admin) and check that all the expected plugins are installed and enabled:
    -   ActiveObjects Plugin - OSGi Bundle
    -   Your plugin, which should appear under *groupId*.*artifactId*

NOTE: If you're having issues, you might want to compare with <a href="https://bitbucket.org/atlassian_tutorial/ao-tutorial/src/85345ac3660e/ao-tutorial-stage1/" class="external-link">my version of the code</a>.

We're now ready to proceed…

{{% /tip %}}

## Step 4. Add the Plugin

First, we need to define the AO module, in the <a href="https://bitbucket.org/serverecosystem/ao-tutorial/src/2d7dad21286ea2f626ad932fc986baf7980fb21c/src/main/resources/atlassian-plugin.xml?at=stage2&amp;fileviewer=file-view-default" class="external-link">plugin descriptor (atlassian-plugin.xml)</a>.

``` xml
<ao key="ao-module">
  <description>The module configuring the Active Objects service used by this plugin</description>
  <entity>com.atlassian.tutorial.ao.todo.Todo</entity>
</ao>
```

## Step 5. Create your first entity

Now we can create that first entity, `com.atlassian.tutorial.ao.todo.Todo` as referenced in the module descriptor. All new entities must be declared in the module descriptor.  
In the Active Objects world, an entity is defined by an interface. Our `Todo` entity looks like this:

``` java
package com.atlassian.tutorial.ao.todo;

import net.java.ao.Entity;

public interface Todo extends Entity
{
    String getDescription();

    void setDescription(String description);

    boolean isComplete();

    void setComplete(boolean complete);
}
```

It defines two fields, a `String` and a `boolean`.

Note that it extends `net.java.ao.Entity`, which defines the primary key as being `ID`. Unless you have a *really* good reason to do otherwise, it is **strongly** advised to do so.

## Step 6. Implement the Todo servlet

Let's add a servlet that actually does something. First we need to define it in the plugin descriptor. For that we update the <a href="http://confluence.atlassian.com/x/GwH3CQ" class="external-link">servlet module</a> already defined for the Example servlet that should still be there.

``` xml
<servlet name="Todo List &amp; Add Servlet" class="com.atlassian.tutorial.ao.todo.TodoServlet" key="todo-list">
  <description>A servlet to add and list todos</description>
  <url-pattern>/todo/list</url-pattern>
</servlet>
```

And we refactor the servlet class so that it looks like this:

``` java
package com.atlassian.tutorial.ao.todo;

import com.atlassian.activeobjects.external.ActiveObjects;
import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;

import static com.google.common.base.Preconditions.*;

@Scanned
public final class TodoServlet extends HttpServlet
{
    @ComponentImport
    private final ActiveObjects ao;

    @Inject
    public TodoServlet(ActiveObjects ao)
    {
        this.ao = checkNotNull(ao);
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException
    {
        res.getWriter().write("Todo servlet, doGet");
        res.getWriter().close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException
    {
        res.getWriter().write("Todo servlet, doPost");
        res.getWriter().close();
    }
}
```

As we've added the component definition in our module, we can constructor inject the servlet with the ActiveObjects service. Note that the `checkNotNull` method here is statically imported from the <a href="http://code.google.com/p/google-collections/" class="external-link">google collections'</a> <a href="http://google-collections.googlecode.com/svn/trunk/javadoc/com/google/common/base/Preconditions.html" class="external-link">Preconditions class</a>.

{{% note %}}

At this stage I've removed the test classes and resources as we'll worry about those later.

{{% /note %}}{{% tip %}}

Let's check that this servlet acutally works:


-   Run `atlas-mvn package` from the command line,
-   Access the servlet at <a href="http://localhost:5990/refapp/plugins/servlet/todo/list" class="uri external-link">localhost:5990/refapp/plugins/servlet/todo/list</a>

It should read *Todo servlet, doGet* on the screen!

{{% /tip %}}

## Step 7. Implement some Methods

### `doGet`

Let's implement `doGet` first.

``` java
    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException
    {
        final PrintWriter w = res.getWriter();
        w.write("<h1>Todos</h1>");

        // the form to post more TODOs
        w.write("<form method=\"post\">");
        w.write("<input type=\"text\" name=\"task\" size=\"25\"/>");
        w.write("&nbsp;&nbsp;");
        w.write("<input type=\"submit\" name=\"submit\" value=\"Add\"/>");
        w.write("</form>");

        w.write("<ol>");

        ao.executeInTransaction(new TransactionCallback<Void>() // (1)
        {
            @Override
            public Void doInTransaction()
            {
                for (Todo todo : ao.find(Todo.class)) // (2)
                {
                    w.printf("<li><%2$s> %s </%2$s></li>", todo.getDescription(), todo.isComplete() ? "strike" : "strong");
                }
                return null;
            }
        });

        w.write("</ol>");
        w.write("<script language='javascript'>document.forms[0].elements[0].focus();</script>");

        w.close();
    }
```

There are a few things going on here. Some very simple HTML is being written to the output, nothing that anyone should fear, so it won't be detailed here. Other things need to be:

1.  All Active Objects interactions must happen in a transaction, this is an example of how to do it. More on that later.
2.  Getting all the todos that have been persisted to the database. This is as simple as that.

### `doPost`

In a similar fashion, this is how the doPost method is implemented:

``` java
    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException
    {
        final String description = req.getParameter("task");
        ao.executeInTransaction(new TransactionCallback<Todo>() // (1)
        {
            @Override
            public Todo doInTransaction()
            {
                final Todo todo = ao.create(Todo.class); // (2)
                todo.setDescription(description); // (3)
                todo.setComplete(false);
                todo.save(); // (4)
                return todo;
            }
        });

        res.sendRedirect(req.getContextPath() + "/plugins/servlet/todo/list");
    }
```

Here again the code is even simpler, as there is no need for any HTML.

1.  Still working in a transaction,
2.  Creating a new Todo entity,
3.  Setting some of its values,
4.  Persisting the entity to the database

`TransactionalCallback` needs to be imported using:

``` java
import com.atlassian.sal.api.transaction.TransactionCallback;
```

We now have enough code to list all the todos from the database and also add todos.

{{% tip %}}

Stage 2

We've now completed **stage 2** of this guide.

-   Run `atlas-mvn package` from the command line and you should be able to access the URL <a href="http://localhost:5990/refapp/plugins/servlet/todo/list" class="uri external-link">localhost:5990/refapp/plugins/servlet/todo/list</a>, there you will be able to:
    -   List Todo items,
    -   and Create new Todo items.

NOTE: If you're having issues, you might want to compare with <a href="https://bitbucket.org/atlassian_tutorial/ao-tutorial/src/85345ac3660e/ao-tutorial-stage2/" class="external-link">my version of the code</a>.

Woohoo! You've got your first Active Objects capable plugin working.

{{% /tip %}}

Before we jump onto removing todos, we will talk about transactions.

## Step 8. Create an AO interaction within a Transaction

NOTE: *Please note, JIRA currently does not support transactions for Active Objects (as of JIRA 6.0).*

As previously stated, every Active Objects interaction must happen within a transaction. Doing so is fairly easy, as per the following code:

``` java
public void someMethod(final ActiveObjects ao)
{
    ao.executeInTransaction(new TransactionCallback<Object>()
    {
        @Override
        public Object doInTransaction()
        {
            // do something with AO
            return null;
        }
    });
}
```

Doing by hand is going to be painful. So there is a declarative alternative, using the <a href="https://studio.atlassian.com/source/browse/AO/trunk/activeobjects-core/src/main/java/com/atlassian/activeobjects/tx/Transactional.java?r=HEAD" class="external-link">@Transactional annotation</a>.

## Step 9.  Introduce the Todo service

These annotations will only work on interfaces, so we won't be able to apply it on our servlet. No need to worry let's introduce the `TodoService`:

``` java
package com.atlassian.tutorial.ao.todo;

import com.atlassian.activeobjects.tx.Transactional;

import java.util.List;

@Transactional
public interface TodoService
{
    Todo add(String description);

    List<Todo> all();
}
```

and its implementation looks like this:

``` java
package com.atlassian.tutorial.ao.todo;

import com.atlassian.activeobjects.external.ActiveObjects;

import java.util.List;

import static com.google.common.base.Preconditions.checkNotNull;
import static com.google.common.collect.Lists.newArrayList;

import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
import javax.inject.Inject;
import javax.inject.Named;

@Scanned
@Named
public class TodoServiceImpl implements TodoService
{
    @ComponentImport
    private final ActiveObjects ao;

    @Inject
    public TodoServiceImpl(ActiveObjects ao)
    {
        this.ao = checkNotNull(ao);
    }

    @Override
    public Todo add(String description)
    {
        final Todo todo = ao.create(Todo.class);
        todo.setDescription(description);
        todo.setComplete(false);
        todo.save();
        return todo;
    }

    @Override
    public List<Todo> all()
    {
        return newArrayList(ao.find(Todo.class));
    }
}
```

## Step 10. Create a Servlet Class to Use the Service

Now is the time to add a servlet class to use the service and make it a bit simpler:

``` java
package com.atlassian.tutorial.ao.todo;

import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

import static com.google.common.base.Preconditions.*;

public final class TodoServlet extends HttpServlet
{
    private final TodoService todoService;

    public TodoServlet(TodoService todoService)
    {
        this.todoService = checkNotNull(todoService);
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException
    {
        final PrintWriter w = res.getWriter();
        w.write("<h1>Todos</h1>");

        // the form to post more TODOs
        w.write("<form method=\"post\">");
        w.write("<input type=\"text\" name=\"task\" size=\"25\"/>");
        w.write("&nbsp;&nbsp;");
        w.write("<input type=\"submit\" name=\"submit\" value=\"Add\"/>");
        w.write("</form>");

        w.write("<ol>");

        for (Todo todo : todoService.all()) // (2)
        {
            w.printf("<li><%2$s> %s </%2$s></li>", todo.getDescription(), todo.isComplete() ? "strike" : "strong");
        }

        w.write("</ol>");
        w.write("<script language='javascript'>document.forms[0].elements[0].focus();</script>");

        w.close();
    }

    @Override
    protected void doPost(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException
    {
        final String description = req.getParameter("task");
        todoService.add(description);
        res.sendRedirect(req.getContextPath() + "/plugins/servlet/todo/list");
    }
}
```

{{% tip %}}

Stage 3

We've now completed **stage 3** of this guide.

-   Run `atlas-mvn package` from the command line and you should be able to access the URL <a href="http://localhost:5990/refapp/plugins/servlet/todo/list" class="uri external-link">localhost:5990/refapp/plugins/servlet/todo/list</a>, there you will be able to:
    -   List Todo items,
    -   and Create new Todo items.

NOTE: If you're having issues, you might want to compare with <a href="https://bitbucket.org/atlassian_tutorial/ao-tutorial/src/85345ac3660e/ao-tutorial-stage3/" class="external-link">my version of the code</a>.

We have the exact same features as in stage 2, but this time we've used declarative transactions to simplify our code.

{{% /tip %}}

## Step 11. Test the Todo service

Now that we've written a bit of code, it's time to do some testing. Active Objects provides a simple framework for integration testing on top of <a href="http://junit.org" class="external-link">JUnit 4.8</a>.

First thing we need to do is add the needed dependencies to the `pom.xml`:

``` xml
<dependency>
  <groupId>com.atlassian.activeobjects</groupId>
  <artifactId>activeobjects-test</artifactId>
  <version>${ao.version}</version>
  <scope>test</scope>
</dependency>
```

where `ao.version` is the version of Active Objects you're using. If you followed this guide carefully it should already be defined. Note the scope of the dependency is correctly set to `test`.

We will need as well a dependency on JUnit, of course, HSQL DB as this is the database we're going to test against, and an slf4j implementation. Here is an example of what you should add to your `pom.xml`:

{{% note %}}

You must use JUnit 4.8 or later

The Active Objects test framework requires JUnit 4.8 or later. If you use an earlier version of JUnit, the tests may fail silently.

For more information, see <a href="https://studio.atlassian.com/browse/AO-334" class="external-link">AO-334</a>.

{{% /note %}}

``` xml
<dependency>
  <groupId>hsqldb</groupId>
  <artifactId>hsqldb</artifactId>
  <version>1.8.0.10</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-simple</artifactId>
  <version>1.6.2</version>
  <scope>test</scope>
</dependency>
```

The JUnit dependency has already been added when the `pom.xml` was generated.

The Plugin SDK is based on maven - no surprise here - so create the standard directory for test sources `src/test/java` if it does not already exist.

Now let's write those tests. We're going to test the `com.atlassian.tutorial.ao.todo.TodoServiceImpl` class.

We create in the test source directory a class named `com.atlassian.tutorial.ao.todo.TodoServiceImplTest` and it should look like this:

``` java
package com.atlassian.tutorial.ao.todo;

import org.junit.After;
import org.junit.Before;
import org.junit.Test;

public class TodoServiceImplTest
{
    @Before
    public void setUp() throws Exception
    {
    }

    @After
    public void tearDown() throws Exception
    {
    }

    @Test
    public void testAdd() throws Exception
    {
    }

    @Test
    public void testAll() throws Exception
    {
    }
}
```

To make sure everything is configured correctly, run the test now using `atlas-unit-test`, it should pass. Awesome, let's tell this test about Active Objects and setup our `TodoServiceImpl` instance:

``` java
package com.atlassian.tutorial.ao.todo;

import com.atlassian.activeobjects.test.TestActiveObjects;
import net.java.ao.EntityManager;
import net.java.ao.test.junit.ActiveObjectsJUnitRunner;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;

import java.util.List;

import static org.junit.Assert.*;

@RunWith(ActiveObjectsJUnitRunner.class) // (1)
public class TodoServiceImplTest
{
    private EntityManager entityManager;  // (2)

    private TodoServiceImpl todoService; // (3)

    @Before
    public void setUp() throws Exception
    {
        assertNotNull(entityManager); // (4)
        todoService = new TodoServiceImpl(new TestActiveObjects(entityManager)); // (5)
    }

    @Test
    public void testAdd() throws Exception
    {

    }

    @Test
    public void testAll() throws Exception
    {

    }
}
```

Here are a few things to note and understand:

1.  we're using the `ActiveObjectsJUnitRunner` to run this test, this will help us access a correctly configured Active Objects instance for testing. It also wraps each tests in a transaction that is rolled-back after each of them. This will leave the test database in the same state for each test.
2.  this is the `EntityManager` that will be automatically injected by the `ActiveObjectsJUnitRunner`. We will be able to use that entity manager to create an `ActiveObjects` instance to use with our service implementation.
3.  the service under test,
4.  here we're just checking that the `EntityManager` is not `null` to make sure we've configured our test correctly,
5.  we instantiate the service with a specific `TestActiveObjects` instance.

Let's run the test again. It passes! Great, let's move on to actually writing some tests.

``` java
package com.atlassian.tutorial.ao.todo;

import com.atlassian.activeobjects.external.ActiveObjects;
import com.atlassian.activeobjects.test.TestActiveObjects;
import net.java.ao.EntityManager;
import net.java.ao.test.junit.ActiveObjectsJUnitRunner;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;

import java.util.List;

import static org.junit.Assert.*;

@RunWith(ActiveObjectsJUnitRunner.class)
public class TodoServiceImplTest
{
    private EntityManager entityManager;

    private ActiveObjects ao; // (1)

    private TodoServiceImpl todoService;

    @Before
    public void setUp() throws Exception
    {
        assertNotNull(entityManager);
        ao = new TestActiveObjects(entityManager);
        todoService = new TodoServiceImpl(ao);
    }

    @Test
    public void testAdd() throws Exception
    {
        final String description = "This is a todo";

        ao.migrate(Todo.class); // (2)

        assertEquals(0, ao.find(Todo.class).length);

        final Todo add = todoService.add(description);
        assertFalse(add.getID() == 0);

        ao.flushAll(); // (3) clear all caches

        final Todo[] todos = ao.find(Todo.class);
        assertEquals(1, todos.length);
        assertEquals(description, todos[0].getDescription());
        assertEquals(false, todos[0].isComplete());
    }

    @Test
    public void testAll() throws Exception
    {
        ao.migrate(Todo.class); // (2)

        assertTrue(todoService.all().isEmpty());

        final Todo todo = ao.create(Todo.class);
        todo.setDescription("Some todo");
        todo.save();

        ao.flushAll(); // (3) clear all caches

        final List<Todo> all = todoService.all();
        assertEquals(1, all.size());
        assertEquals(todo.getID(), all.get(0).getID());
    }
}
```

A few comments:

1.  we've extracted the `ActiveObjects` instance into a field for using in our tests,
2.  before testing we need to tell AO about the `Todo` entity
3.  using `flushAll` can be handy to make sure we're actally testing the DB and not the cache.

The rest of the test should be self explanatory. As always run the tests, which should pass.

## Step 12. Seed the Database with some Test Data

In this test all the *migration* and data is treated within each test. What if we wanted to seed the database with some data to simplify our tests? Well, let's do this:

``` java
package com.atlassian.tutorial.ao.todo;

import com.atlassian.activeobjects.external.ActiveObjects;
import com.atlassian.activeobjects.test.TestActiveObjects;
import net.java.ao.EntityManager;
import net.java.ao.test.jdbc.Data;
import net.java.ao.test.jdbc.DatabaseUpdater;
import net.java.ao.test.junit.ActiveObjectsJUnitRunner;
import org.junit.Before;
import org.junit.Test;
import org.junit.runner.RunWith;

import java.util.List;

import static org.junit.Assert.*;

@RunWith(ActiveObjectsJUnitRunner.class)
@Data(TodoServiceImplTest.TodoServiceImplTestDatabaseUpdater.class) // (1)
public class TodoServiceImplTest
{
    private static final String TODO_DESC = "This is a todo";

    private EntityManager entityManager;

    private ActiveObjects ao;

    private TodoServiceImpl todoService;

    @Before
    public void setUp() throws Exception
    {
        assertNotNull(entityManager);
        ao = new TestActiveObjects(entityManager);
        todoService = new TodoServiceImpl(ao);
    }

    @Test
    public void testAdd() throws Exception
    {
        final String description = TODO_DESC + "#1";

        assertEquals(1, ao.find(Todo.class).length);

        final Todo add = todoService.add(description);
        assertFalse(add.getID() == 0);

        ao.flushAll(); // clear all caches

        final Todo[] todos = ao.find(Todo.class);
        assertEquals(2, todos.length);
        assertEquals(add.getID(), todos[1].getID());
        assertEquals(description, todos[1].getDescription());
        assertEquals(false, todos[1].isComplete());
    }

    @Test
    public void testAll() throws Exception
    {
        assertEquals(1, todoService.all().size());

        final Todo todo = ao.create(Todo.class);
        todo.setDescription("Some todo");
        todo.save();

        ao.flushAll(); // clear all caches

        final List<Todo> all = todoService.all();
        assertEquals(2, all.size());
        assertEquals(todo.getID(), all.get(1).getID());
    }

    // (2)
    public static class TodoServiceImplTestDatabaseUpdater implements DatabaseUpdater
    {
        @Override
        public void update(EntityManager em) throws Exception
        {
            em.migrate(Todo.class);

            final Todo todo = em.create(Todo.class);
            todo.setDescription(TODO_DESC);
            todo.save();
        }
    }
}
```

Here it is. We've introduce the `@Data` annotation of the Active Objects test framework:

1.  We define the annotation which takes a class parameter.
2.  We define the class used to deal with test data before the tests are run. A typical usage of this class is to `migrate` entities under test and then add some data that tests can use.

### **Configuring the database**

For now we haven't worried about the database used for testing at all. This was all taken care of by the Active Objects testing framework. Indeed by default it will use an in-memory <a href="http://hsqldb.org/" class="external-link">HSQL DB</a>. But we will want to test against other databases.

This is what the <a href="https://bitbucket.org/activeobjects/ao/src/11cc3c865152/activeobjects-test/src/main/java/net/java/ao/test/jdbc/Jdbc.java?at=master" class="external-link">@Jdbc</a> annotation is used for. Annotate your test class with this, it requires a single class parameter that implements <a href="http://java.net/projects/activeobjects/sources/svn/content/trunk/activeobjects-test/src/main/java/net/java/ao/test/jdbc/JdbcConfiguration.java?rev=1194" class="external-link">JdbcConfiguration</a>.

You can now test against any database of your choice with some simple configuration. I suggest you have a look in the <a href="https://bitbucket.org/activeobjects/ao/src/11cc3c865152/activeobjects-test/src/main/java/net/java/ao/test/jdbc/?at=master" class="external-link">net.java.ao.test.jdbc</a> package as it contains multiple implementations of this interface that might be useful. Note the <a href="https://bitbucket.org/activeobjects/ao/src/11cc3c8651525335fadcf0b2403616edfbc681a0/activeobjects-test/src/main/java/net/java/ao/test/jdbc/DynamicJdbcConfiguration.java?at=master" class="external-link">DynamicJdbcConfiguration</a> which will let you change the database simply by setting a system property.

### **Name converters**

Active Objects defines a way to configure the strategy for naming database identifiers given an `Entity` class (e.g. tables and column names) using the <a href="https://bitbucket.org/activeobjects/ao/src/11cc3c8651525335fadcf0b2403616edfbc681a0/activeobjects-test/src/main/java/net/java/ao/test/converters/NameConverters.java?at=master" class="external-link">@NameConverters</a>annotation. The default configuration for testing is equivalent to that used when deployed in an Atlassian product except that the table name hash is always `000000`.

{{% note %}}

The strategy for converting table names and column names is explained in the [Active Objects FAQ](/server/framework/atlassian-sdk/active-objects-faq).

{{% /note %}}

## Step 13. Adding some logging (Optional)

In order to see what SQL queries are being issued, let's add some better logging. We'll be using `log4j` to replace the `slf4j-simple` logger. In `pom.xml`, remove the dependency on `slf4j-simple` and replace with the following:

``` xml
<dependency>
  <groupId>org.slf4j</groupId>
  <artifactId>slf4j-log4j12</artifactId>
  <version>1.6.2</version>
  <scope>test</scope>
</dependency>
<dependency>
  <groupId>log4j</groupId>
  <artifactId>log4j</artifactId>
  <version>1.2.16</version>
  <scope>test</scope>
</dependency>
```

Now we simply need to configure `log4j` for the test we wrote. Let's add a `log4j.properties` configuration file to the `src/test/resources` directory.

We want it to look like this:

``` java
log4j.rootLogger = INFO, console

log4j.appender.console = org.apache.log4j.ConsoleAppender
log4j.appender.console.layout = org.apache.log4j.PatternLayout
log4j.appender.console.layout.ConversionPattern = %5p - %60.60c - %m%n

# (1)
log4j.logger.net.java.ao.sql = DEBUG, console 
log4j.additivity.net.java.ao.sql = false
```

1.  This is the logger configuration to show the SQL queries run by Active Objects.

Now when running the tests, you should see the executed SQL statements:

``` text
DEBUG -                                              net.java.ao.sql - CREATE TABLE PUBLIC.AO_000000_TODO (
    COMPLETE BOOLEAN,
    DESCRIPTION VARCHAR(255),
    ID INTEGER GENERATED BY DEFAULT AS IDENTITY (START WITH 1) NOT NULL,
    PRIMARY KEY(ID)
)
DEBUG -                                              net.java.ao.sql - INSERT INTO AO_000000_TODO (ID) VALUES (NULL)
DEBUG -                                              net.java.ao.sql - UPDATE PUBLIC.AO_000000_TODO SET DESCRIPTION = ? WHERE ID = ?
DEBUG -                                              net.java.ao.sql - SELECT * FROM PUBLIC.AO_000000_TODO
DEBUG -                                              net.java.ao.sql - INSERT INTO AO_000000_TODO (ID) VALUES (NULL)
DEBUG -                                              net.java.ao.sql - UPDATE PUBLIC.AO_000000_TODO SET DESCRIPTION = ?,COMPLETE = ? WHERE ID = ?
DEBUG -                                              net.java.ao.sql - SELECT * FROM PUBLIC.AO_000000_TODO
```

{{% tip %}}

Stage 4

We've now completed **stage 4** of this guide.

-   Your plugin should work exactly the same as in **Stage 3**,
-   But now it is tested and your `TodoServiceImplTest` should pass.

NOTE: If you're having issues, you might want to compare with <a href="https://bitbucket.org/atlassian_tutorial/ao-tutorial/src/8ff99e91f5a4/ao-tutorial-stage4/" class="external-link">my version of the code</a>.

You'll notice that there are other stages to the source code. This is because [Handling AO Upgrade Tasks](/server/framework/atlassian-sdk/handling-ao-upgrade-tasks) follows on from this tutorial.

{{% /tip %}}

### References

-   The <a href="https://bitbucket.org/serverecosystem/ao-tutorial" class="external-link">source for this tutorial</a>
-   <a href="http://java.net/projects/activeobjects" class="external-link">Active Objects on java.net</a>
-   [Active Objects Plugin Module](/server/framework/atlassian-sdk/active-objects-plugin-module)
-   [Active Objects FAQ](/server/framework/atlassian-sdk/active-objects-faq)
