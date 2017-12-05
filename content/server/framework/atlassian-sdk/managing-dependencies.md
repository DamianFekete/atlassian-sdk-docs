---
aliases:
- /server/framework/atlassian-sdk/managing-dependencies-2818370.html
- /server/framework/atlassian-sdk/managing-dependencies-2818370.md
category: devguide
confluence_id: 2818370
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818370
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818370
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: Managing Dependencies 2818370
---
# Managing dependencies

This page describes how you can use libraries provided by the Atlassian framework or from third-parties in your plugin. It describes background concepts you'll need to understand.

You declare dependencies in the POM file. This page describes when you should use 'provided' in your dependency declarations (meaning the library is provided by the Atlassian application framework), and when you should use 'compile' (meaning, the library should be compiled with your plugin).

 

## About Plugins, bundles and OSGi

An Atlassian plugin is an OSGi bundle. This implies a lot of things, but there are two fundamentals you must understand:

-   **Classloader isolation**: A new classloader is created for each plugin at startup, and it's used to load your plugin's classes. This is not the same as the system classloader, nor can you access any class the system knows about through it. This provides several benefits: different plugins can use different versions of the same library simultaneously, for example. However, it also means that several assumptions you may have made about how class loading works in Java are no longer valid. This page will explain how to do what you want without needing to understand every detail of the system.
-   **Runtime dependencies**: At plugin start, the plugin system will ask your plugin for the dependencies it requires to run and then attempt to locate them somewhere in the available OSGi publicly-visible packages. If they can't be found, the plugin will not start and you will see an error message, usually a `NoClassDefFoundError`. If they are found, the plugin classloader is created and told where to load the libraries and versions requested - and ONLY those libraries.

You will follow the same process every time you decide to use another piece of code in your plugin:

-   "Where will I get the artifacts to compile my code against?" Answering this question will tell you what you need to add as `<dependencies>` in your `pom.xml`.
-   "Where will my code find these artifacts at runtime?" Answering this question will tell you which manifest instructions you need to specify in your `pom.xml` (inside the AMPS configuration section).

In most cases, you either need something from the Atlassian product or you want to use something you package inside your plugin, like a third-party library.

There are a few other complications which we'll discuss below.

## Specifying manifest instructions

Manifest instructions tell the plugin system what Java packages - and, optionally, which version of those packages - your plugin needs to have available in its classloader at runtime.

When you compile a plugin project, the SDK can automatically generate the OSGi manifest for your plugin based on the dependencies it detects. However, for most plugins, we suggest specifying such manifest instructions explicitly. The generated manifest makes a useful starting point for the instructions.

You add OSGi manifest instructions to your plugin using the Maven plugin configuration settings in the project POM:

``` xml
<project>
  <build>
    <plugins>
      <plugin>
        <groupId>com.atlassian.maven.plugins</groupId>
        <artifactId>maven-***-plugin</artifactId> <!-- *** is the name of the application (product) you're using -->
        <version>3.2.3</version>
        <extensions>true</extensions>
        <configuration>
          <productVersion>${product.version}</productVersion>
          <instructions>
            <!-- OSGi instructions go here -->
          </instructions>
        </configuration>
      </plugin>
    </plugins>
  </build>
</project>
```

You specify the bundling instructions in the custom `instruction` element. The SDK uses the <a href="http://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html" class="external-link">Apache Felix Maven plugin (BND)</a> behind the scenes to handle this, so the instructions explained here are passed to BND at package time and used to create the OSGi manifest.

{{% note %}}

What other configuration options are available?

See [Using the AMPS Maven Plugin Directly](https://developer.atlassian.com/display/DOCS/Using+the+AMPS+Maven+Plugin+Directly) for details.

{{% /note %}}

You specify bundling instructions in the format:

``` bash
package-name(wildcard);version="<major>.<minor>.<maintenance>"
```

Use commas to separate multiple instructions.

Here's a real-world example:

``` bash
com.atlassian.confluence.events.event.space;version="[3.4,4.0)"
com.atlassian.confluence.search.lucene.*;version="[3.4,4.0)"
com.atlassian.confluence.json*;version="[3.4,4.0)"
```

**Specifying package names**

There are three different ways of specifying the package name:

-   **com.atlassian.confluence.events.event.space**: Imports every class in the `com.atlassian.confluence.events.event.space` package.
-   **com.atlassian.confluence.search.lucene.\***: Imports every class in **subpackages** of `com.atlassian.confluence.search.lucene` while **not** importing any classes `com.atlassian.confluence.search.lucene` itself
-   **com.atlassian.confluence.json\***: Imports every class in `com.atlassian.confluence.json` **and** all classes in all subpackages of `com.atlassian.confluence.json`

**Specifying versions**

There are several ways to specify which version of a package to import:

-   **version="0.0"**: Matches any version found. This is used when your code requires the package but doesn't care which version of the code is used.
-   **version="1.4"**: Matches any version equal to the version specified *or any later version*. Any package versioned as 1.4, 1.5, 2.0, or 9.0 will satisfy this specification
-   **version="(2.0,2.8\]"**: Matches any version in the range from 2.0 (exclusive) to 2.8 (inclusive). Either end of a range can be exclusive or inclusive.

In the Confluence example above, the version specification `[3.4,4.0)` translates to:

*For the preceding package, import any version from 3.4 inclusive to 4.0 exclusive; that is, any version from 3.4 itself to any version less than 4.0.*

{{% tip %}}

Use ranges wherever possible

The ranges in the above example allow the code to work with any future 3.x version of Confluence (assuming the APIs being used don't break in one of those releases). In general, set your upper bound to the next major version (exclusive) - whatever "major version" means for that library.

{{% /tip %}}

## Using Container-provided Packages

Each OSGi system has a special bundle called the **system bundle**, which functions similarly to the system classloader in vanilla Java applications. Atlassian products export the following through the system bundle:

-   The usual Java runtime libraries (everything in the `java.*` / `javax.*` namespaces)
-   Everything in the product itself that we think a plugin author might want to use (most of the product's core classes and any proprietary libraries we use, which means most of `com.atlassian.*`
-   Several open source libraries the product uses (things like the Apache Commons libraries `org.apache.commons.*`, Google Collections `com.google.collect.*`, etc.)

How do you know what's provided by the Atlassian product container? When running in development mode, the UPM presents an OSGi browser that lists the bundles in the application. See [Using the OSGi Browser](/server/framework/atlassian-sdk/using-the-osgi-browser) for more information.

All plugins can use packages exported by the system bundle; in fact, the plugin system inspects your code at runtime, sees what code you want to use from the system bundle, and automatically adds the necessary directives. This works in simple cases, and it's good enough to start with, but we strongly recommend that you specify exactly what you need as part of the polishing-before-release process.

{{% warning %}}

Adding JAR files to WEB-INF/lib

In the past, you could add a JAR file to the `WEB-INF/lib` directory and make it available to all plugins, as well as the product itself. **This no longer works**, as the plugin system doesn't know about any code in the product beyond what it's been told to use; placing random JARs in `WEB-INF/lib` or class files in `WEB-INF/classes` will **not** make them available in the system bundle.

{{% /warning %}}

To use a package from the system bundle in your plugin, do the following:

-   Add the library to your `pom.xml` under the `<dependencies>` block.

``` xml
<project>
  ...
  <dependencies>
    <dependency>
      <!--
        we're using Confluence in this example;
        this is taken directly from the plugin
        generated when you run the command
        atlas-create-confluence-plugin.
       -->
      <groupId>com.atlassian.confluence</groupId>
      <artifactId>confluence</artifactId>
      <version>${confluence.version}</version>
      <scope>provided</scope>    <!-- important! -->
    </dependency>
  </dependencies>
  ...
</project>
```

Adding a `<dependency>` tells the SDK that your code will use this artifact, but specifying `<scope>provided</scope>` refines that to mean "these classes will be provided at runtime by the product". The SDK will then use these classes when compiling your plugin, but it won't actually put Confluence itself inside your plugin when it is built.

{{% note %}}

If you don't specify a scope in your dependency declaration, the scope defaults to 'compile'. Compiling a package that is provided by the container can result in runtime conflicts.

{{% /note %}}

Similarly, if you were writing a <a href="/pages/createpage.action?spaceKey=PLUGINFRAMEWORK&amp;title=Servlet+Modules" class="createlink">servlet plugin</a>, you'd need to tell the SDK where to find the servlet API classes to compile against, but you wouldn't want to actually include the servlet APIs in your plugin. To do that, you'd add this to your `pom.xml`:

``` xml
<project>
  ...
  <dependencies>
    <dependency>
      <groupId>javax.servlet</groupId>
      <artifactId>servlet-api</artifactId>
      <version>2.4</version>
      <scope>provided</scope>    <!-- important! -->
    </dependency>
  </dependencies>
  ...
</project>
```

-   Add import instructions for the packages you're using

Having taken care of the compile time side, we turn our focus to runtime. We need to tell the plugin system what packages to make available to our classloader. This is done with the `<Import-Package>` instruction.

Assume your plugin requires classes from Confluence's JSON support, space events, and Lucene mechanisms. To import these Confluence packages at runtime, use the following:

``` xml
<configuration>
  ...
  <instructions>
    <Import-Package>
      com.atlassian.confluence.events.event.space;version="[3.4,4.0)",
      com.atlassian.confluence.search.lucene.*;version="[3.4,4.0)",
      com.atlassian.confluence.json*;version="[3.4,4.0)"
    </Import-Package>
  </instructions>
</configuration>
```

For packages that are compiled with your plugin, you can choose to export the bundle, using the `Export-Package` declaration. This makes it available to other plugins in the system.

## Using third-party code

To use third-party code in your plugin, you need to add a `<dependency>` just like above, but with an important change:

``` xml
<project>
  ...
  <dependencies>
    <dependency>
      <groupId>com.mycompany.awesome.stuff</groupId>
      <artifactId>awesome-utils</artifactId>
      <version>1.0.4</version>
      <scope>compile</scope>    <!-- important! -->
    </dependency>
  </dependencies>
  ...
</project>
```

By specifying `<scope>compile</scope>`, you tell the SDK that the `awesome-utils` library is needed at compile time and runtime. The SDK will **bundle** the `awesome-utils` library into your plugin, and the plugin system will make it available in the plugin classloader when the plugin is started.

## Troubleshooting Dependency Issues

If not specified otherwise, dependencies in the POM use 'compile' scope by default. This causes the package to be compiled with the plugin.

It's important to understand that if the Atlassian application framework provides the same package, compile scope may lead to class loading conflicts at runtime. Specifically, the conflict occurs if the classes from the library are passed by API to the application or to another plugin.

In general, when developing plugins, you should be aware of what packages the container provides, and use 'provided' scope for such cases when possible. Provided scope minimizes the size of your plugin distribution, and it allows it to benefit from the advantages of OSGi-based modularity.

The easiest way to see what libraries are available in the framework is by checking the [OSGi Browser](/server/framework/atlassian-sdk/using-the-osgi-browser) in the add-on administration console.

In the console, note the entry called "System Bundle". It contains most of the core bundles available to your add-on. Click it to view the packages and versions of packages it exports.

For packages provided by the product framework, you can either:

-   Specify a particular package import statement in your plugin explicitly (in the POM or plugin descriptor), or
-   Allow the SDK to generate them for you

In the latter case, the SDK adds the statements to the OSGi manifest in the compiled plugin archive. By default, the auto-generated OSGi Import-Package directive does not specify a version for the package. As a result, the framework will pick the highest available version from the host application (or from any other plugin that exports a higher version).

The manifest statement applies to runtime bundle associations for packages that are not bundled with the add-on. The compile-time dependency statements in the POM do not affect this behavior. Instead, dependency declarations in the POM (if they specify a package version), affect:

1.  The version the compiler looks at when compiling your code, and
2.  The version that is embedded if you use a compile scope.

To avoid problems that may result from a future version of the package, you may choose to explicitly declare the OSGi dependency by adding the import package instructions to the maven-amps-plugin or maven-*product*-plugin section of the POM, as described in [Using Container-provided Packages](#using-container-provided-packages), or to the plugin descriptor file.

For more general information and strategies for declaring dependencies, component imports, and more, see [Converting from Version 1 to Version 2 (OSGi) Plugins](/server/framework/atlassian-sdk/converting-from-version-1-to-version-2-osgi-plugins).

##### RELATED TOPICS

<a href="/pages/createpage.action?spaceKey=PLUGINFRAMEWORK&amp;title=OSGi%2C+Spring+and+the+Plugin+Framework" class="createlink">OSGi, Spring and the Plugin Framework</a>  
[Going from Plugin to OSGi Bundle](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Going+from+Plugin+to+OSGi+Bundle)  
<a href="http://prezi.com/ybc6itroyt40/big-modular-plugins/" class="external-link">Big Modular Plugins (AtlasCamp 2010 presentation video)<br />
</a>[Using the OSGi Browser](/server/framework/atlassian-sdk/using-the-osgi-browser)













