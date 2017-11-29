---
title: Dependency Issues During Plugin Initialisation 852094
aliases:
    - /server/framework/atlassian-sdk/dependency-issues-during-plugin-initialisation-852094.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852094
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852094
confluence_id: 852094
platform:
product:
category:
subcategory:
---
# Dependency issues during plugin initialisation

### Symptoms -- What Goes Wrong

Your plugin fails to initialize with an error that suggests a dependency problem, such as missing resources or incompatible classes.  
The exact symptoms can take many forms - here are a few examples:

``` bash
[INFO] [talledLocalContainer] org.springframework.beans.factory.parsing.BeanDefinitionParsingException: Configuration problem: Unable to locate Spring NamespaceHandler for XML schema namespace [http://www.springframework.org/schema/osgi]
[INFO] [talledLocalContainer] Offending resource: URL [bundle://28.0:0/META-INF/spring/atlassian-plugins-component-imports.xml]
```

``` bash
[INFO] [talledLocalContainer] Caused by: org.springframework.beans.FatalBeanException: Class [org.springframework.osgi.config.OsgiNamespaceHandler] for namespace [http://www.springframework.org/schema/osgi] does not implement the [org.springframework.beans.factory.xml.NamespaceHandler] interface
```

``` bash
[INFO] [talledLocalContainer] com.atlassian.util.concurrent.LazyReference$InitializationException: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'com.myplugin.MyFilter': Instantiation of bean failed; nested exception is java.lang.IllegalAccessError: tried to access field org.slf4j.impl.StaticLoggerBinder.SINGLETON from class org.slf4j.LoggerFactory
```

``` bash
[INFO] [talledLocalContainer] 2011-01-05 16:30:20,759 ERROR [http-1990-3] [atlassian.plugin.servlet.DefaultServletModuleManager] getFilter Unable to create filter
[INFO] [talledLocalContainer] com.atlassian.util.concurrent.LazyReference$InitializationException: java.lang.ClassCastException: com.myplugin.MyFilter cannot be cast to javax.servlet.Filter
```

### Cause

The most likely cause is that a resource supplied by the environment in which your plugin is hosted was overridden by a conflicting resource, because the conflicting resource was erroneously bundled in your plugin.

There are a couple of ways you can explore the resources provided by the hosting environment:

-   You can use the [Universal Plugin Manager](https://developer.atlassian.com/display/UPM) which, <a href="http://blogs.atlassian.com/developer/2011/01/announcing_upm_1_dot_3_and_osgi_tab.html" class="external-link">as of version 1.3</a>, displays the packages exported and imported by each bundle loaded in the environment.
-   Similar information can be obtained from the <a href="http://felix.apache.org/site/apache-felix-web-console.html" class="external-link">Apache Felix Web Console</a>, which is available at `http://\[your_app_base_URL\]/plugins/servlet/system/console` if the app was started with the <a href="/pages/createpage.action?spaceKey=PLUGINFRAMEWORK&amp;title=Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project" class="createlink">Plugin SDK</a>.

To see the list of jars bundled with your plugin, run the following from your plugin directory:

``` bash
mvn clean package
ls target/classes/META-INF/lib/
```

As a general rule, the only jars listed in `target/classes/META-INF/lib/` should be those specific to your plugin. For example, if the purpose of your plugin is to integrate a 3rd party app, it is reasonable for your plugin to bundle the API library for that app, because that library isn't supplied by any other part of the environment. On the other hand, it is unlikely that your plugin would need to bundle jars related to Spring Framework, logging or javax.servlet, since those are already provided by the plugin platform, the app or the app server.

### Resolution

To resolve this issue, ensure that all dependencies, except those that are unique to your plugin, have their `scope` element set to `provided` in your plugin's `pom.xml`. For example:

``` xml
    <dependencies>
    ...
        <dependency>
            <groupId>org.springframework.osgi</groupId>
            <artifactId>spring-osgi-core</artifactId>
            <version>3.0.5.RELEASE</version>
            <scope>provided</scope>
        </dependency>
    ...
    </dependencies>
```

Note that the default scope is `compile`, which results in the dependency being bundled with the plugin, so `provided` must be specified explicitly. For more information on dependency scopes in Maven, see the documentation for <a href="http://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html" class="external-link">Maven's dependency mechanism</a>.

### More Information

-   <a href="http://www.atlassian.com/en/about/events/atlascamp/2010/day3/big-modular-plugins" class="external-link">Big Modular Plugins</a> (presentation from AtlasCamp 2010)
-   <a href="http://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html" class="external-link">Maven Dependency Mechanism</a>
-   <a href="http://felix.apache.org/site/apache-felix-web-console.html" class="external-link">Apache Felix Web Console</a>

##### RELATED TOPICS

-   [OSGi, Spring and the Plugin Framework](/server/framework/atlassian-sdk/852146.html)
-   [Plugin Development Platform](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Plugin+Framework)
-   <a href="/pages/createpage.action?spaceKey=PLUGINFRAMEWORK&amp;title=Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project" class="createlink">Atlassian Plugin SDK</a>

























