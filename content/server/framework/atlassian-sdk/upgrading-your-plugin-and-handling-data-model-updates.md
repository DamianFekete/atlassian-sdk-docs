---
aliases:
- /server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates-5669184.html
- /server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates-5669184.md
category: devguide
confluence_id: 5669184
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669184
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669184
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/developing-your-plugin-with-active-objects/upgrading-your-plugin-and-handling-data-model-updates
new_url: /server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates
platform: server
product: atlassian-sdk
subcategory: learning
title: Upgrading your plugin and handling data model updates
---
# Upgrading your plugin and handling data model updates

Sometimes your data model will evolve. This page will describe how to handle upgrades for various use cases of model changes.{{% note %}}

The current upgrade framework of the Active Objects plugin is not final yet and there might be some changes and adjustment before AO goes to version 1.0. We will however strive to make any change as simple as possible and with as little impact as possible.  
Any <a href="https://studio.atlassian.com/browse/AO" class="external-link">feedback you might have</a> using this framework is more than welcome.

{{% /note %}}

 

## General usage

### Module definition

You need to define your upgrade tasks in the module definition within the plugin descriptor. Use the `upgradeTask` element:

**Module definition example**

``` javascript
<atlassian-plugin name="Hello World" key="example.plugin.helloworld" plugins-version="2">
  <plugin-info>
    <description>A basic Active Objects module test</description>
    <vendor name="Atlassian Software Systems" url="http://www.atlassian.com"/>
    <version>1.0</version>
  </plugin-info>

  <ao key="ao-module">
    <description>The AO module for this plugin.</description>
    <entity>com.myapp.MyEntity</entity>
    <upgradeTask>com.myapp.upgrades.v1.Version1UpgradeTask</upgradeTask>
  </ao>
</atlassian-plugin>
```

### Upgrade task definition

An upgrade task is defined as an implementation of the **`com.atlassian.activeobjects.external.ActiveObjectsUpgradeTask`** interface.

It defines two methods that should be implemented:

-   `ModelVersion getModelVersion()`: defines the version of the model once this upgrade task will have run
-   `void upgrade(ModelVersion currentVersion, ActiveObjects ao)`: performs the actual upgrade

### Implementing the upgrade

The upgrade method has 2 parameters that are important to understand well:

-   `ModelVersion currentVersion`, this is the current version of the model in the database. This allows for checking whether the upgrade can deal with the current model and take appropriate actions either way.
-   `ActiveObjects ao`, this is a version of a configured `ActiveObjects` service. There are several things to note about this instance:
    -   It is not configured to handle any entities. The `migrate` method should be used to associate it with entities. This can be used to migrate to an intermediate model and perform some data migration (from one table to another for example).
    -   It is not a shared instance. Each upgrade task gets its own `ActiveObjects` instance, in order to be able to handle different entity models/schemas. All those instance are also different to the one actually used by the plugin once the `ao` module has been fully initialised.

Most of the time one upgrade task will be associated with one specific version of the model. So there will be a copy of the entities in a specific package for that version of the model.

{{% warning %}}

Warning

If you are using a version of Active Objects earlier than 0.22.1, data belonging to any entities not listed in the `migrate` method call will be permanently deleted. If you are using Active Objects 0.22.1 or later versions, the data will not be deleted.

{{% /warning %}}

To be able to use that model, in the upgrade method, it is necessary to call the `migrate` method, with the list of entity classes.

Once the model is available, it is very simple to manipulate the model and its data. This is all done using the provided `ActiveObjects` service as you would do in the plugin.

{{% note %}}

Note

Ultimately the Active Objects module when initialised always updates the model/schema to the version defined by the entities declared.  
This means that any upgrade task should prepare the model/schema and data for this last update to happen successfully.

{{% /note %}}

## Common upgrades

### Adding an entity/table

There shouldn't be any upgrade to do when adding an entity/table to an existing model. This is unless you need to populate the new entities with some data.

The Active Objects framework and plugin will take care of adding the table for you.

### Adding a field/column

This is the same as adding an entity/table. Nothing to do!

### Removing an entity/table

**Note:** When upgrading your plugin to a new version, do not remove entities/tables unless you are aware of the consequences. Active Objects will make the database match the entity interface in the Java code. It alters tables to match the current interface. Removing tables and columns will result in data loss. For that reason, we recommend that you do not delete tables or columns, only add them.

With the above note in mind: Removing an entity/table is as simple as removing it from your model. In other words, simply don't declare it in your `ao` module descriptor. The Active Objects framework and plugin will drop the table.

### Removing a field/column

**Note:** When upgrading your plugin to a new version, do not remove columns unless you are aware of the consequences. Active Objects will make the database match the entity interface in the Java code. It alters tables to match the current interface. Removing columns will result in data loss. For that reason, we recommend that you do not delete tables or columns, only add them.

### Renaming an entity/table

The Active Objects framework doesn't know about renaming. If you change the name of an entity, it will remove the other entity and create a new one. All the data in the entity will be lost.

Doing this in practice, you should create an upgrade task, keeping the old entity and creating the new one as a copy with a different name. Then copy the data over.

The Active Objects plugin offers a simpler solution, using the `net.java.ao.schema.Table` annotation:

**Renamed entity**

``` javascript
@Table("MyEntity")
public interface RenamedEntity extends Entity
{
   ...
}
```

In this code sample, the entity was previously named `MyEntity` with its actual table name looking like `AO_XXX_MY_ENTITY`. We've now renamed the entity `RenamedEntity` keeping its table name the same using the `@Table` annotation.

### Renaming a field/column

This behaves the same as for entity/table names. So the same precautions should apply when changing names. You can also rename a field without renaming its column.

**RenamedField**

``` javascript
public interface MyEntity extends Entity
{
   @Mutator("Field")
   public void setNewField(String newField);

   @Accessor("Field")
   public String getNewField();
}
```

In this code sample, the `field` has been renamed `newField`. This is done through the `net.java.ao.Mutator` and `net.java.ao.Accessor` annotations.

### Changing from one data type to another

If a plugin changes the data type of a column, Active Objects will try to automatically migrate that column. However, the recommended approach is **not** to use an in-place type conversion. Instead, create a new column and migrate the data during the upgrade process.

See <a href="https://ecosystem.atlassian.net/browse/AO-273" class="external-link">AO-273</a>.

## Best practices

See [Best practices for developing with Active Objects](/server/framework/atlassian-sdk/best-practices-for-developing-with-active-objects).












































































































































































































































































