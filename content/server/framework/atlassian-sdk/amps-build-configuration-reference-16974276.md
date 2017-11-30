---
aliases:
- /server/framework/atlassian-sdk/amps-build-configuration-reference-16974276.html
- /server/framework/atlassian-sdk/amps-build-configuration-reference-16974276.md
category: devguide
confluence_id: 16974276
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16974276
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16974276
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/about-amps-build-options/amps-build-configuration-reference
new_url: /server/framework/atlassian-sdk/amps-build-configuration-reference
platform: server
product: atlassian-sdk
subcategory: learning
title: AMPS build configuration reference
---
# AMPS build configuration reference

This page describes build configuration settings you can use with AMPS. AMPS, which stands for the Atlassian Maven Plugin Suite, is built into the Atlassian Plugins SDK. It defines Maven archetypes and goals specifically for creating Atlassian product plugins.

You can use the following configuration parameters with AMPS. Values to use for a given parameter may vary depending on the host application.

### cliPort

Specifies the port that the embedded Maven CLI plugin should open for interactive shell commands. The default value is `4330`.

### compressResources

Specifies whether web resources in your plugin (eg. JavaScript) are automatically minified as part of the build process. The default value is `true`.

### containerId

Specifies the <a href="http://cargo.codehaus.org/" class="external-link">Cargo</a> container that should be used when starting and hosting the product. The default value is `tomcat6x` (for Tomcat 6.0.20).

{{% note %}}

While the underlying Cargo system can support many different containers, Atlassian only supports Tomcat installations. Check the supported platforms page of the version of the Atlassian application you are developing against to discover which versions are supported. For example, for the latest version of JIRA, see <a href="https://confluence.atlassian.com/display/JIRA/Supported+Platforms" class="external-link">the JIRA supported platforms</a> page. For Confluence 5.0, see the <a href="https://confluence.atlassian.com/display/CONF50/Supported+Platforms" class="external-link">Confluence 5.0 supported platforms</a> page.

{{% /note %}}

### dataSources

It is possible to declare JNDI datasources for the product, but this is not available as a direct child of &lt;configuration&gt;. It is available as a child of a `<product>` in the `<products>` tag. See [Declaring JNDI Datasources in AMPS](/server/framework/atlassian-sdk/declaring-jndi-datasources-in-amps) for examples.

### httpPort

Specifies the port that the container should listen on. The default value varies by product. See the table [here](https://developer.atlassian.com/display/DOCS/Working+with+the+SDK).

### contextPath

Specifies the context path at which the product should be deployed. The default value varies by product; see the table [here](https://developer.atlassian.com/display/DOCS/Working+with+the+SDK).

### jvmArgs

Specifies arguments to the forked Java VM that will host the container. The default value is blank.

### log4jProperties

Specifies a custom log4j.properties file to be used by the product, replacing the one shipped inside the product. Generally, there is no reason to do this, but it can be useful for debugging sometimes.

### productDataPath

Specifies a path on the local filesystem to a custom product data archive. This allows you to start the product prepopulated with data of your choice. For more details, see the [atlas-create-home-zip](https://developer.atlassian.com/display/DOCS/atlas-create-home-zip) SDK command.

If you need to also make changes to the webapp directory, see [overriding the application's webapp when developing your plugin](https://developer.atlassian.com/display/DOCS/Overriding+the+application%27s+webapp+when+developing+your+plugin).

### productDataVersion

Specifies the version of the test data resources the product will use at startup. The test data includes a developer license valid for three hours, a default product home directory, and a simple, pre-provisioned, in-memory or on-disk data store (usually provided via HSQL). These files are supplied by Atlassian with the product. The default value is defined for each product in the com.atlassian.<a href="http://ampsatlassian-amps-parent" class="external-link">amps:atlassian-amps-parent</a> POM version that corresponds to the current SDK version.

If you'd like to override the default data with data from your own product installation, see the productDataPath parameter.

### productVersion

Specifies the version of the product that should be run. This value must correspond to the version number of a set of Maven artifacts available from the [Atlassian Maven repositories](https://developer.atlassian.com/display/DOCS/Atlassian+Maven+Repositories). The default value is defined for each product in the `com.atlassian.amps:atlassian-amps-parent` POM version that corresponds to the current SDK version.

### server

Specifies the hostname of the machine on which the container should be started. The default value is `localhost`.

### systemPropertyVariables

Specifies system properties that should be set in the forked Java VM that will host the container. The default values are blank. For example:

 

``` xml
 <configuration>
  <systemPropertyVariables>
    <property1Name>property1Value</property1Name>
    <property2Name>property2Value</property2Name>
  </systemPropertyVariables>
</configuration>
```

 

### enableFastdev

Specifies whether to enable the [FastDev](https://developer.atlassian.com/display/DOCS/Automatic+Plugin+Reinstallation+with+FastDev) plugin. The default value is `true`.

You can set this parameter to `false` to disable FastDev when running or debugging your plugin.

### fastdevVersion

Specifies the version of FastDev to load when running or debugging your plugin, overriding the default version specified by AMPS.

### pluginArtifacts

Specifies other Atlassian plugins that your plugin depends on to work properly. These plugin artifacts will be installed into the product along with your plugin.

All plugins specified here must be installed in a repository your Maven installation can access through `settings.xml`.

Example:

 

``` xml
<configuration>
  <pluginArtifacts>
    <pluginArtifact>
      <groupId>com.mycompany.atlassian.plugins</groupId>
      <artifactId>our-business-services-plugin</artifactId>
      <version>1.0.3</version>
    </pluginArtifact>
  </pluginArtifacts>
</configuration>
```

 

### libArtifacts

Specifies arbitrary Java libraries that your plugin depends on to work properly. These libraries will be installed alongside the product's core libraries in `WEB-INF/lib`.

All libraries specified here must be installed in a repository your Maven installation can access through `settings.xml`.

Accessing these libraries from your plugin is a product-specific process, and usually you won't want to do this anyway, as this defeats the purpose of the plugin system. This feature is only useful for legacy code or very old plugins that you're not able to upgrade to version 2 of the plugin system.

To depend on a third-party library, add it to the `<dependencies>` in your plugin POM, which protects you from changes out of your control.

Example:

 

``` xml
 <configuration>
  <libArtifacts>
    <libArtifact>
      <groupId>com.mycompany.ancient.plugins</groupId>
      <artifactId>our-business-services-plugin</artifactId>
      <version>1.0.3</version>
    </libArtifact>
  </libArtifacts>
</configuration>
```

 

### bundledArtifacts

Specifies other Atlassian plugins that your plugin depends on to work properly. These plugin artifacts will be treated as bundled by the product, meaning they can be disabled but not removed. The product will always make a bundled plugin available at startup, even if it was removed previously. By contrast, plugin artifacts can be removed after installation at any time, and they will stay gone until they are manually reinstalled.

All plugins specified here must be installed in a repository your Maven installation can access through `settings.xml`.

Unless you're working with a forked version of a plugin normally bundled in the product, you will not need to use this.

To depend on another second- or third-party plugin, add it to the `<pluginArtifacts>` above.

Example:

 

``` xml
 <configuration>
  <bundledArtifacts>
    <bundledArtifact>
      <groupId>com.mycompany.atlassian.plugins</groupId>
      <artifactId>our-forked-bundled-product-plugin</artifactId>
      <version>4.1-mycompany-fork</version>
    </bundledArtifact>
  </bundledArtifacts>
</configuration>
```

 

### pluginDependencies

Specifies other plugins or OSGi bundles that will be bundled into an OBR archive. OBRs can be installed via the UPM, and the UPM will automatically install any dependencies that are packaged in the OBR which are not installed yet.

All dependencies specified here must be defined in the standard &lt;dependencies&gt; section of the `pom.xml`, and should be set to a &lt;scope&gt; of either 'test' or 'provided'.

Example:

 

``` xml
 <configuration>
  <pluginDependencies>
    <pluginDependency>
      <groupId>com.mycompany.atlassian.plugins</groupId>
      <artifactId>our-osgi-bundle</artifactId>
    </pluginDependency>
  </pluginDependencies>
</configuration>
```

 

For more information about dependencies, see [Managing Plugin Dependencies](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Managing+Plugin+Dependencies).

### installPlugin

Specifies whether to install the current plugin when the product is started. The default value is `true`.

You can set this flag to `false` to start a product without being in a plugin working directory. This is useful for quickly starting a product with a specific configuration for testing or experimentation. For example, the command:

    atlas-mvn confluence:run -DproductVersion=3.4 -Dinstall.plugin=false

Starts Confluence 3.4 with the default test data.

### output

Specifies a file to pipe the container's output to. The container output includes the startup logs, messages sent to `System.out` and `System.err` while the product is running, and SDK-specific messages. By default, container output is sent to the standard output stream.

This is useful for comparing your plugin's log output (and possible error messages) between different products or different versions of the same product. It's also useful when <a href="https://studio.atlassian.com/browse/AMPS" class="external-link">reporting bugs with the SDK</a>.

### jvmDebugPort

Specifies the port on which the product should listen for a debugger connection. The default value is `5005`.

### jvmDebugSuspend

Specifies whether the product, when started in debug mode, should wait for a debugger to connect before proceeding with startup. The default value is `false`.

### skipTests

Specifies whether testing should be skipped in this invocation. The default value is `false`.

### functionalTestPattern

Specifies the pattern to use for finding integration tests to run. The default value is `\it/**/*Test.java` (relative to src/test/java). If any `<testGroup>` elements are specified, this value will be ignored.

### products

Defines a product that can be referenced in a `testGroup`. Test groups allow you to run a subset of tests on a specific product configuration; for example, if your plugin is designed for JIRA and Confluence, you can have a test group with JIRA-specific tests, another group with Confluence-specific tests, and a third with tests common to both configurations.

See [Create and Run Traditional Integration Tests](/server/framework/atlassian-sdk/create-and-run-traditional-integration-tests) for examples of the `products` element configuration.

### testGroup

Defines a test group to run on one or more `<product>` configurations.

See [Create and Run Traditional Integration Tests](/server/framework/atlassian-sdk/create-and-run-traditional-integration-tests) for examples of using the `testGroup` element.

### testGroups

Specifies which test groups should be run in this invocation. Test groups should be referenced by ID and separated by commas. The default is for all test groups to run.

Example:

    atlas-mvn crowd:integration-test -DtestGroups=loginTests,authTests,cookieTests

See [Create and Run Traditional Integration Tests](/server/framework/atlassian-sdk/create-and-run-traditional-integration-tests) for examples of defining test groups.

### parallel

Starts up the Atlassian applications in parallel mode. This may be useful if you use test groups in your plugin configuration to launch multiple products at start up, a possible scenario if your plugin is intended to work with more than one type of Atlassian application.

By enabling the parallel option in the POM or by specifying it at the command line, you direct the SDK to initialize the applications simultaneously rather than sequentially. This can speed the start up of the test group on fast computers.

By default, the parallel option is off. To enable it, specify it at the command line by passing the `-Dparallel` switch to the Plugins SDK start up command, or by setting the `parallel` element in the POM to `true`, as follows:

    <configuration>
       <parallel>true</parallel>
    ...
    </configuration>

This option has no effect on Studio-Crowd, FishEye or Studio-FeCru.

For more information about test groups, see [Create and Run Traditional Integration Tests](/server/framework/atlassian-sdk/create-and-run-traditional-integration-tests).

### noWebapp

Specifies whether the product(s) required by `<products>` should actually be started, or if the tests should run blind and assume that the needed products are already running. The default value is `false`, which starts all required `<product>` instances.

This can be valuable if you are debugging integration tests and the product's state is not relevant to the tests being debugged; this will save you the wait of a product starting and stopping before you can see the test results.

Example:

    atlas-mvn jira:integration-test -DtestGroups=jiraTests,pluginTests -Dno.webapp=true

### instructions

Specifies OSGi bundling instructions, interpreted by the Maven <a href="http://felix.apache.org/site/apache-felix-maven-bundle-plugin-bnd.html" class="external-link">BND plugin</a> and used to generate the OSGi manifest inside the plugin JAR. BND instructions give you complete control over the expression of your plugin's runtime dependencies, including package name and version; they communicate to the plugin system (and the product) exactly what is required for your plugin to operate correctly.

This configuration is essential when creating plugins designed to operate in more than one product, but is usually unnecessary in other cases.

### testInstructions

Serves a similar purpose to 'instructions' described above, except the test instructions would be used to generate the OSGi manifest inside the plugin's test JAR i.e. JAR built from the `test` source tree, typically including integration tests.

### skipManifestValidation

Specifies whether the SDK should attempt to validate the OSGi manifest (whether explicitly specified by the user or auto-generated). The default value is `false`.

This can be useful when debugging an OSGi validation problem or forcing the plugin to load in the container to see which bundles can not be located. However, in most cases the warnings suppressed by this flag indicate actual problems that need to be fixed before the plugin can be successfully installed.

##### RELATED TOPICS

<a href="https://developer.atlassian.com/display/DOCS/Create+and+Run+Traditional+Integration+Tests" class="diff-block-context">Create and Run Traditional Integration Tests</a>

[Declaring JNDI Datasources in AMPS](/server/framework/atlassian-sdk/amps-build-configuration-reference)


























































































































