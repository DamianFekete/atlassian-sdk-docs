---
aliases:
- /server/framework/atlassian-sdk/handling-ao-upgrade-tasks-45520507.html
- /server/framework/atlassian-sdk/handling-ao-upgrade-tasks-45520507.md
category: devguide
confluence_id: 45520507
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=45520507
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=45520507
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/handling-ao-upgrade-tasks
new_url: /server/framework/atlassian-sdk/handling-ao-upgrade-tasks
platform: server
product: atlassian-sdk
subcategory: learning
title: Handling AO upgrade tasks
---
# Handling AO upgrade tasks

This guide will help you get familiar with updating your object model using the Active Objects plugin upgrade tasks.

{{% note %}}

Source code of the tutorial available

The code that is used throughout this tutorial is <a href="https://bitbucket.org/serverecosystem/ao-tutorial" class="external-link">hosted on BitBucket</a>. You might want to checkout or even fork this code to help you with the task at hand:

git clone git@bitbucket.org:serverecosystem/ao-tutorial.git

There are tags for each stage in the source repository, e.g. to see the progress at the end of stage 5, do:

git checkout stage5

This tutorial resumes from **stage 4** of the code, as the previous stages have all been covered in the [Getting Started](https://developer.atlassian.com/display/DOCS/Getting+Started+with+Active+Objects) tutorial. It is strongly recommended that you go through this first tutorial if you have done so already.

{{% /note %}}

 

### Adding to the data model

So far our TODO plugin doesn't care about who the user is and even whether the user is actually logged in. We're going to remedy to that right now by:

1.  enforcing the user is logged in before accessing the TODO list (not strictly Active Objects related)
2.  record the TODO items per user

##### Enforcing logged in user

We check whether the user is authenticated in the servlet:

``` java
package com.atlassian.tutorial.ao.todo;

import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
import com.atlassian.sal.api.user.UserManager;

import javax.inject.Inject;
import javax.servlet.ServletException;
import javax.servlet.http.HttpServlet;
import javax.servlet.http.HttpServletRequest;
import javax.servlet.http.HttpServletResponse;
import java.io.IOException;
import java.io.PrintWriter;

import static com.google.common.base.Preconditions.*;

@Scanned
public final class TodoServlet extends HttpServlet
{
    private final TodoService todoService;
    @ComponentImport
    private final UserManager userManager; // (1)

    @Inject
    public TodoServlet(TodoService todoService, UserManager userManager)
    {
        this.todoService = checkNotNull(todoService);
        this.userManager = checkNotNull(userManager);
    }

    @Override
    protected void doGet(HttpServletRequest req, HttpServletResponse res) throws ServletException, IOException
    {
        enforceLoggedIn(req, res); // (2)

        final PrintWriter w = res.getWriter();
        w.printf("<h1>Todos (%s)</h1>", userManager.getRemoteUser().getUsername());

        // the form to post more TODOs
        w.write("<form method=\"post\">");
        w.write("<input type=\"text\" name=\"task\" size=\"25\"/>");
        w.write("&nbsp;&nbsp;");
        w.write("<input type=\"submit\" name=\"submit\" value=\"Add\"/>");
        w.write("</form>");

        w.write("<ol>");

        for (Todo todo : todoService.all())
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
        enforceLoggedIn(req, res); // (2)

        final String description = req.getParameter("task");
        todoService.add(description);
        res.sendRedirect(req.getContextPath() + "/plugins/servlet/todo/list");
    }

    private void enforceLoggedIn(HttpServletRequest req, HttpServletResponse res) throws IOException
    {
        if (userManager.getRemoteUser() == null)  // (3)
        {
            res.sendRedirect(req.getContextPath() + "/plugins/servlet/login");
        }
    }
}
```

1.  We need to inject SAL's user manager, see [SAL's own documentation](https://developer.atlassian.com/display/SAL/Shared+Access+Layer+Documentation) for more information about it,
2.  Enforcing the user is logged in in both the `GET` and `POST` method,
3.  Simply check the username is not `null`, if it is redirect to the login page.

##### Recording TODO items against the current user

We now need to record which user the TODO item belongs to. A simple way to do this is to add a `username` field to the `Todo` class:

``` java
@Preload
public interface Todo extends Entity
{
    void setUserName(String userName);

    String getUserName();

    String getDescription();

    void setDescription(String description);

    boolean isComplete();

    void setComplete(boolean complete);
}
```

And then we also need to update the `TodoService` implementation to properly handle this username:

``` java
package com.atlassian.tutorial.ao.todo;

import com.atlassian.activeobjects.external.ActiveObjects;
import com.atlassian.plugin.spring.scanner.annotation.component.Scanned;
import com.atlassian.plugin.spring.scanner.annotation.imports.ComponentImport;
import com.atlassian.sal.api.user.UserManager;
import net.java.ao.Query;

import javax.inject.Inject;
import javax.inject.Named;
import java.util.List;

import static com.google.common.base.Preconditions.checkNotNull;
import static com.google.common.collect.Lists.newArrayList;

@Scanned
@Named
public class TodoServiceImpl implements TodoService
{
    @ComponentImport
    private final ActiveObjects ao;
    @ComponentImport
    private final UserManager userManager; // (1)

    @Inject
    public TodoServiceImpl(ActiveObjects ao, UserManager userManager)
    {
        this.ao = checkNotNull(ao);
        this.userManager = checkNotNull(userManager);
    }

    @Override
    public Todo add(String description)
    {
        final Todo todo = ao.create(Todo.class);
        todo.setDescription(description);
        todo.setComplete(false);
        todo.setUserName(currentUserName()); // (2)
        todo.save();
        return todo;
    }

    @Override
    public List<Todo> all()
    {
        return newArrayList(ao.find(Todo.class, Query.select().where("USER_NAME = ?", currentUserName()))); // (3)
    }

    private String currentUserName() {
        return userManager.getRemoteUser().getUsername();
    }

}
```

1.  We get SAL's `UserManager` injected as we use it to get the current user,
2.  Setting the user name when adding a TODO item,
3.  Finding the TODO items for the current user only.

That's it. Active Objects will take care of adding the missing column for us. Let's see it in action, but first let's add some SQL logging to the Refapp so that we can easily check the column is actually added.

Since **stage 4** we already have a `log4j.properties` file, in the `src/test/resources` directory. Let's configure the `maven-refapp-plugin` to also use it.

``` xml
...
  <plugin>
    <groupId>com.atlassian.maven.plugins</groupId>
    <artifactId>maven-refapp-plugin</artifactId>
    <version>${amps.version}</version>
    <extensions>true</extensions>
    <configuration>
      ...
      <log4jProperties>src/test/resources/log4j.properties</log4jProperties>
    </configuration>
  </plugin>
...
```

{{% note %}}

Now that we've changed the data model, the tests we wrote in Stage 4 are no longer up-to-date. You can either choose to update them or skip compiling/running the tests via adding the following to your `pom.xml`

``` xml
<properties>
...
<maven.test.skip>true</maven.test.skip>
</properties>
```

{{% /note %}}{{% tip %}}

Let's check that this works:

-   Run `atlas-mvn package` from the command line, in the `ao-tutorial` directory, this will upgrade the plugin
-   Access the servlet at <a href="http://localhost:5990/refapp/plugins/servlet/todo/list" class="uri external-link">http://localhost:5990/refapp/plugins/servlet/todo/list</a>, you will need to be logged in now, for example as `admin (pwd:admin)`

There are 2 things you should notice when doing this:

1.  the SQL query `ALTER TABLE AO_3F7D93_TODO ADD COLUMN USER_NAME VARCHAR(255)` being logged,
2.  there aren't any TODO items any more, let's fix this in the following

**Note:** for the plugin to correctly be upgraded, you need to make sure that the plugin descriptor (`atlassian-plugin.xml`) key is the same in both plugins.

{{% /tip %}}

So we have one issue, we lost the TODO items we created. Fear not, the data is still there, it's simply that we didn't update the items to be associated with any user. So when logged in as the `admin` user, we don't see any items.

##### Assign migrated TODO items to the admin user

For this we're going to need our first `ActiveObjectsUpgradeTask`. Here is how it looks:

``` java
package com.atlassian.tutorial.ao.todo.upgrade.v1; // (1)

import com.atlassian.activeobjects.external.ActiveObjects;
import com.atlassian.activeobjects.external.ActiveObjectsUpgradeTask;
import com.atlassian.activeobjects.external.ModelVersion;

public final class TodoUpgradeTask001 implements ActiveObjectsUpgradeTask
{
    @Override
    public ModelVersion getModelVersion()
    {
        return ModelVersion.valueOf("1"); // (2)
    }

    @Override
    public void upgrade(ModelVersion currentVersion, ActiveObjects ao) // (3)
    {
        ao.migrate(Todo.class); // (4)

        for (Todo todo : ao.find(Todo.class)) // (5)
        {
            todo.setUserName("admin");
            todo.save();
        }
    }
}
```

1.  We've created a specific package for this upgrade task, and this version of the data model. Also note that the `Todo` class used here is the `com.atlassian.tutorial.ao.todo.upgrade.v1.Todo` class, we copied the model corresponding to that upgrade task into that same package. This code is never to be touched and should remain like so for the whole life of the plugin.
2.  Setting the model version, here `1`. This is used by Active Objects to figure out which upgrade tasks to run and in which order. By default plugins that never defined any upgrade tasks are assigned the version `0`.
3.  The Active Objects component passed a parameter here is the only one you should use for the upgrade task. You should **never** inject your plugin's Active Objects component in **any** upgrade task. This instance is specific to that one upgrade task and will be discarded after the upgrade task has run.
4.  When writing your upgrade task, you must call the `migrate` method yourself to let Active Objects know about the data model you want to work this. This will update the database to match the model. Note that if you omit part of the model objects here, their respective tables in the database will be dropped!
5.  Then we can update our data model as we need.

The last step is to reference this upgrade task in the Active Objects module descriptor:

``` xml
<ao key="ao-module">
  <description>The module configuring the Active Objects service used by this plugin</description>
  <entity>com.atlassian.tutorial.ao.todo.Todo</entity>

  <upgradeTask>com.atlassian.tutorial.ao.todo.upgrade.v1.TodoUpgradeTask001</upgradeTask>
</ao>
```

{{% tip %}}

We've now completed **stage 5** of this tutorial. Let's check that everything is working:

-   Run `atlas-mvn package` from the command line, this will upgrade the plugin to version 1
-   Access the servlet at <a href="http://localhost:5990/refapp/plugins/servlet/todo/list" class="uri external-link">http://localhost:5990/refapp/plugins/servlet/todo/list</a>, you will need to be logged in now:
-   as `admin (pwd:admin)`, you should retrieve all the TODO items you previously entered,
-   as `fred (pwd:fred)`, you shouldn't have any TODO item there yet

{{% note %}}

If you're having issues, you might want to compare with my version of the code.

{{% /note %}}

You now have an Active Objects plugin capable of handling older version of its model.

{{% /tip %}}

Now we're not so happy about our decision to add the username as a field in the `Todo` class. Let's introduce a new `User` object.

### Refactoring the data model.

So what we want to do is:

-   Add a new `User` model class,
-   Remove the `userName` field from the `Todo` class,
-   Add a `User` field to the `Todo` class.

Let's first have a look at the model we want get to:

``` java
package com.atlassian.tutorial.ao.todo;

import net.java.ao.Entity;

public interface User extends Entity
{
    String getName();
    void setName(String name);
}
```

``` java
package com.atlassian.tutorial.ao.todo;

import net.java.ao.Entity;
import net.java.ao.Preload;
import net.java.ao.schema.NotNull;

@Preload
public interface Todo extends Entity
{
    @NotNull
    void setUser(User user);

    @NotNull
    User getUser();

    String getDescription();

    void setDescription(String description);

    boolean isComplete();

    void setComplete(boolean complete);
}
```

In order to get there we're going to need an `ActiveObjectsUpgradeTask`, but also an intermediate model where both the `userName` field and the `User` field are present on the `Todo` class. Let's see what it looks like:

``` java
package com.atlassian.tutorial.ao.todo.upgrade.v2; // (1)

import net.java.ao.Entity;

public interface User extends Entity
{
    String getName();
    void setName(String name);
}
```

1.  See how we've created this model in a specific upgrade package

``` java
package com.atlassian.tutorial.ao.todo.upgrade.v2; // (1)

import net.java.ao.Entity;
import net.java.ao.Preload;

@Preload
public interface Todo extends Entity
{
    void setUserName(String userName); // (2)

    String getUserName();

    void setUser(User user); // (3)

    User getUser();

    String getDescription();

    void setDescription(String description);

    boolean isComplete();

    void setComplete(boolean complete);
}
```

1.  Again, this is a copy of the `Todo` class specific for the upgrade
2.  We still have the `userName` as for the old version of the model
3.  We added the new `User` field as per the new version of the model

And then we have the corresponding upgrade task:

``` java
package com.atlassian.tutorial.ao.todo.upgrade.v2; // (1)

import com.atlassian.activeobjects.external.ActiveObjects;
import com.atlassian.activeobjects.external.ActiveObjectsUpgradeTask;
import com.atlassian.activeobjects.external.ModelVersion;
import com.google.common.collect.ImmutableMap;
import net.java.ao.Query;

public final class TodoUpgradeTask002 implements ActiveObjectsUpgradeTask
{
    @Override
    public ModelVersion getModelVersion()
    {
        return ModelVersion.valueOf("2"); // (2)
    }

    @Override
    public void upgrade(ModelVersion currentVersion, ActiveObjects ao)
    {
        ao.migrate(Todo.class, User.class); // (3)

        Todo[] todos = ao.find(Todo.class); // (4)
        for (Todo todo : todos) {
            todo.setUser(getOrCreateUser(ao, todo.getUserName()));
            todo.save();
        }
    }

    private User getOrCreateUser(ActiveObjects ao, String userName)
    {
        User[] users = ao.find(User.class, Query.select().where("NAME = ?", userName));
        if (users.length == 0) {
            return createUser(ao, userName);
        } else if (users.length == 1) {
            return users[0];
        } else {
            throw new IllegalStateException("There shouldn't be 2 users with the same username! " + userName);
        }
    }

    private User createUser(ActiveObjects ao, String userName)
    {
        return ao.create(User.class, ImmutableMap.<String, Object>of("NAME", userName));
    }
}
```

1.  Again same package,
2.  We increase the version of the model, now it's going to be `2`,
3.  We call migrate with the new model, this will add a new table for the `User` class, and a new field to the `Todo` class (for the `User` reference)
4.  Actually upgrading, setting the `User` to correspond to the `userName`.

Then we simply need to declare the upgrade task in the Active Objects module descriptor:

``` xml
<ao key="ao-module">
  <description>The module configuring the Active Objects service used by this plugin</description>
  <entity>com.atlassian.tutorial.ao.todo.Todo</entity>
  <entity>com.atlassian.tutorial.ao.todo.User</entity>

  <upgradeTask>com.atlassian.tutorial.ao.todo.upgrade.v1.TodoUpgradeTask001</upgradeTask>
  <upgradeTask>com.atlassian.tutorial.ao.todo.upgrade.v2.TodoUpgradeTask002</upgradeTask>
</ao>
```

And we're good to go. Obviously something we've not shown here is how to update the `TodoService` implementation. This is left as an exercise to the reader <img src="https://ecosystem.atlassian.net/wiki/s/1566798676/6452/8afe5ead844f0e54811644803fbbe44093a68efd/_/images/icons/emoticons/wink.png" alt="(wink)" class="confluence-external-resource emoticon-wink" /> . If you're stuck you can look at the source repository.

{{% tip %}}

This complete **stage 6** of this tutorial. Let's check that everything is working as expected:

-   Run `atlas-mvn package` from the command line, check that the upgrade to version 2 occurred:

[INFO] [talledLocalContainer]  INFO - assian.activeobjects.internal.ActiveObjectUpgradeManagerImpl - Starting upgrade of data model, current version is 1
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - CREATE TABLE AO_3F7D93_USER (
[INFO] [talledLocalContainer]     ID INTEGER GENERATED BY DEFAULT AS IDENTITY (START WITH 1) NOT NULL,
[INFO] [talledLocalContainer]     NAME VARCHAR(255),
[INFO] [talledLocalContainer]     PRIMARY KEY(ID)
[INFO] [talledLocalContainer] )
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - ALTER TABLE AO_3F7D93_TODO ADD COLUMN USER_ID INTEGER
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - ALTER TABLE AO_3F7D93_TODO ADD CONSTRAINT fk_ao_3f7d93_todo_user_id FOREIGN KEY (USER_ID) REFERENCES AO_3F7D93_USER(ID)
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - CREATE INDEX index_ao_3f7d93_todo_user_id ON AO_3F7D93_TODO(USER_ID)
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - SELECT * FROM AO_3F7D93_TODO
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - SELECT ID FROM AO_3F7D93_USER WHERE NAME = ?
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - INSERT INTO AO_3F7D93_USER (NAME) VALUES (?)
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - UPDATE AO_3F7D93_TODO SET USER_ID = ? WHERE ID = ?
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - SELECT ID FROM AO_3F7D93_USER WHERE NAME = ?
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - UPDATE AO_3F7D93_TODO SET USER_ID = ? WHERE ID = ?
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - SELECT ID FROM AO_3F7D93_USER WHERE NAME = ?
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - INSERT INTO AO_3F7D93_USER (NAME) VALUES (?)
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - UPDATE AO_3F7D93_TODO SET USER_ID = ? WHERE ID = ?
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - SELECT ID FROM AO_3F7D93_USER WHERE NAME = ?
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - UPDATE AO_3F7D93_TODO SET USER_ID = ? WHERE ID = ?
[INFO] [talledLocalContainer]  INFO - assian.activeobjects.internal.ActiveObjectUpgradeManagerImpl - Finished upgrading, model is up to date at version 2
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - ALTER TABLE AO_3F7D93_TODO DROP COLUMN USER_NAME
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - ALTER TABLE AO_3F7D93_TODO DROP CONSTRAINT fk_ao_3f7d93_todo_user_id
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - ALTER TABLE AO_3F7D93_TODO ALTER COLUMN USER_ID INTEGER NOT NULL
[INFO] [talledLocalContainer] DEBUG -                                              net.java.ao.sql - ALTER TABLE AO_3F7D93_TODO ADD CONSTRAINT fk_ao_3f7d93_todo_user_id FOREIGN KEY (USER_ID) REFERENCES AO_3F7D93_USER(ID)

-   {{% note %}}
If you're having issues, you might want to compare with my version of the code.

{{% /note %}}

{{% /tip %}}































































































































































































































































































































































































































































































































































































































