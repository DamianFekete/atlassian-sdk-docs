---
aliases:
- /server/framework/atlassian-sdk/faq-2818355.html
- /server/framework/atlassian-sdk/faq-2818355.md
category: devguide
confluence_id: 2818355
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818355
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818355
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq
new_url: /server/framework/atlassian-sdk/faq
platform: server
product: atlassian-sdk
subcategory: other
title: FAQ
---
# FAQ

This page collects the FAQ pages for different developer experience levels and the product development pages. 

## Atlassian Plugin SDK FAQ

-   [Atlassian Plugin SDK ignores customisations for port or context path](https://developer.atlassian.com/display/DOCS/Atlassian+Plugin+SDK+ignores+customisations+for+port+or+context+path)
-   [Errors when Creating an Archetype](https://developer.atlassian.com/display/DOCS/Errors+when+Creating+an+Archetype)
-   [How can I change the version of Java my plugin uses](https://developer.atlassian.com/display/DOCS/How+can+I+change+the+version+of+Java+my+plugin+uses)
-   [Maven Cannot Find Java Mail, Java Activation or JTA](https://developer.atlassian.com/display/DOCS/Maven+Cannot+Find+Java+Mail%2C+Java+Activation+or+JTA)
-   [Maven is Unable to Download the Artifact from Any Repository](https://developer.atlassian.com/display/DOCS/Maven+is+Unable+to+Download+the+Artifact+from+Any+Repository)
-   [Maven Parsing Error Unrecognised HTML Tag](https://developer.atlassian.com/display/DOCS/Maven+Parsing+Error+Unrecognised+HTML+Tag)
-   [Maven Runs Out of Memory](https://developer.atlassian.com/display/DOCS/Maven+Runs+Out+of+Memory)
-   [Maven Warning POM for X is Invalid](https://developer.atlassian.com/display/DOCS/Maven+Warning+POM+for+X+is+Invalid)
-   [Product Fails to Start Within Timeout Period](https://developer.atlassian.com/display/DOCS/Product+Fails+to+Start+Within+Timeout+Period)

## Writing your first plugin FAQ

# Build Failure - Manifest Validation Errors

If you use a vendor name of "Atlassian" in your `atlassian-plugin.xml` file, you may receive errors like this:

    [ERROR] BUILD FAILURE
    [INFO] ------------------------------------------------------------------------
    [INFO] Manifest must contain versions for all imports.  Suggested changes:
    javax.servlet.http;version="2.3",
    com.opensymphony.user;version="1.1.1",
    com.atlassian.plugins.rest.common.security;version="1.0.2",
    com.atlassian.jira.t*;version="4.0",
    net.jcip.annotations;version="1.0",
    javax.xml.bind.annotation;version="2.1"

The vendor should be set to something other than "Atlassian", since we have a number of additional validations triggered by that vendor string. For example:

    <plugin-info>
    <description>A sample plugin showing how to add a REST service to JIRA.</description>
      <version>1.0</version>
      <vendor name="Example Company" url="http://www.example.com" />
      <application-version min="4.0"/>
    </plugin-info>

To **skip the manifest validation**, you can add the following tag to the configuration element in your pom.xml

``` javascript
<skipManifestValidation>true</skipManifestValidation>
```

Note: This is not recommended if you want to make your plugin available to multiple Atlassian applications.

# Cannot Log In to Confluence using Admin Account

If you find that you cannot log in to your test Confluence instance using the admin account, set your plugin to build against Confluence 2.6.1 or later using the `atlassian.product.version` parameter.

# Choosing a Logging Framework

Three logging frameworks are available to plugins:

-   Log4j 1.2.15
-   Commons Logging 1.1.1
-   SLF4J 1.5

We recommend Simple Logging Facade for Java (<a href="http://www.slf4j.org/" class="external-link">SLF4J</a>) as a the primary logging framework.

You should ensure that none of these libraries are bundled with your plugin (in `META-INF/lib`) as this will prevent the host application from logging any of your plugin's log messages.

You can check your plugin's dependencies by using <a href="http://maven.apache.org/plugins/maven-dependency-plugin/tree-mojo.html" class="external-link"><code>mvn dependency:tree</code></a> and then exclude any transitive dependencies in the `pom.xml`:

``` javascript
<exclusions>
   <exclusion>
     <groupId>org.slf4j</groupId>
    <artifactId>slf4j-api</artifactId>
  </exclusion>
  <exclusion>
    <groupId>org.slf4j</groupId>
    <artifactId>slf4j-log4j12</artifactId>
  </exclusion>
</exclusions>
```

# Choosing a Package Name

Make sure your package names are unique. You can choose any package name, provided that it does not conflict with any existing package used in the Atlassian application you are developing for, or in any other plugins. Do **not** use `com.atlassian.confluence.plugins.*`. That is confusing to people who try to use the plugin. **Use a real package name** that corresponds to your organisation or project. For example: `org.mycompany.confluence.plugins.*`. The <a href="http://java.sun.com/docs/books/jls/second_edition/html/packages.doc.html#40169" class="external-link">Sun Java documentation</a> has some tips about conventions used to ensure unique package names.

# Eclipse Maven Plugin Build Error

Please note that the new Eclipse plugin is unable to deal with source 'includes' and 'excludes'.

Use the following command :`mvn org.apache.maven.plugins:maven-eclipse-plugin:2.6:eclipse` as this will force mvn to use version 2.6 of the maven eclipse plugin.

The error that you will see if 2.7 is used in your mvn build :

    [ERROR] BUILD ERROR
    [INFO] ------------------------------------------------------------------------
    [INFO] Request to merge when 'filtering' is not identical. 
    [INFO] Original=resource src/main/resources: output=target/classes, 
    [INFO]    include=[atlassian-plugin.xml], exclude=[**/*.java], test=false, 
    [INFO]    filtering=true, merging with=resource src/main/resources: 
    [INFO]    output=target/classes, include=[], exclude=[atlassian-plugin.xml|**/*.java], 
    [INFO]    test=false, filtering=false
    [INFO] ------------------------------------------------------------------------
    [INFO] For more information, run Maven with the -e switch
    [INFO] ------------------------------------------------------------------------

# If you change pom.xml, you may need to restart the atlas-cli

If you are using `atlas-cli` and `pi` for a fast development cycle of your plugin and you get compilation errors about "Unable to run mojo" and no Java line number in your plugin source code, it may be that you changed the dependencies in `pom.xml` but didn't restart `atlas-cli`.

# Instant Loading of Plugin Resources

During development, one of the main things that can slow you down is reloading the plugin just to see the effect of a change to a static CSS or JavaScript file. To solve this problem during development, you can point the plugin framework at a directory containing your resource files and have the plugin framework load them first before looking in the plugin itself.

To enable this feature, set the system property `plugin.resource.directories` to a comma-delimited list of directories containing plugin resources. For example, to point the framework at your current project's resource directory when running an Atlassian application from Maven, you could set the `MAVEN_OPTS` variable:

``` javascript
export MAVEN_OPTS=-Dplugin.resource.directories=/home/myuser/dev/myplugin/src/main/resources
```

#  Overriding the application's webapp when developing your plugin

The <a href="https://maven.atlassian.com/public/com/atlassian/amps/atlassian-plugin-sdk" class="external-link">Atlassian Plugin SDK</a> makes it easy to override any component of the application's webapp.

1.  Create a `src/test/resources/***-app` directory, where `***` is the name of the application you're developing your plugin against. For example `confluence`.
2.  To this directory add the resources you want to add (or override) following the webapp directory structure.

Now when you run your application via `atlas-run`, `atlas-debug` and/or `atlas-integration-test`, it will use the updated WAR built from the application configured in your `pom.xml` and the added resources you have defined.

## Example

This can be useful for example to disable the velocity caches by overriding `velocity.properties` when developing a Confluence plugin.

Create a `src/test/resources/confluence-app/WEB-INF/classes/velocity.properties` file specifying the properties as defined in the [Confluence developer documentation](https://developer.atlassian.com/display/CONFDEV/Disable+Velocity+Caching). That's it.

# Specifying a particular version of the host application

The `atlas-run` command will download the latest version of the application binaries into your local Maven repository. If you want to develop against a version of the host application other than the very latest, you can specify the version to use as a parameter of your `atlas-run` command.

For example, let's assume you want to use Confluence 3.1:

1.  Run `atlas-clean`.
2.  Run `atlas-run -v 3.1`  
    or `atlas-run --version 3.1`.

Alternatively, you can permanently change the application version number in the dependencies section of your POM. Note that your POM may use a property to hold the version number, like this:

``` javascript
<properties>
    <confluence.version>RELEASE</confluence.version>
</properties>
```

You plugin will always build and deploy against this version, until you change this property.

For example, if you are happy to use Confluence 3.1 for a while, you would change the version to the following:

``` javascript
<properties>
    <confluence.version>3.1</confluence.version>
</properties>
```

# Tips for Functional Tests with Selenium

With more and more UI being rendered and processed dynamically with JavaScript, in-browser testing has become a requirement for functional testing. Selenium is a popular choice for implementing tests that execute within the context of a browser but are still Java-driven. This page gives you tips for using Selenium to test your plugin.

## Add atlassian-selenium-browsers-auto to your pom.xml

Add this XML to the `<dependencies>` section in your pom.xml:

``` xml
<dependency>
   <groupId>com.atlassian.selenium</groupId>
   <artifactId>atlassian-selenium-browsers-auto</artifactId>
   <version>2.0.0.m3</version>
   <scope>test</scope>
</dependency>
```

You should verify the `<version>` value <a href="https://maven.atlassian.com/index.html#welcome" class="external-link">is the latest by searching</a> for the `<groupId>` in Atlassian's Maven repository. 

## Write a Selenium test

The Atlassian Plugin SDK comes with support for integration/functional tests that will run with the target Atlassian application started and your plugin installed. You just have to create one or more tests in the `src/test/java/it` directory. The convention is if your code is in the `com.mycompany.myplugin` package, your integration tests would be in the `it.com.mycompany.myplugin` package or `src/test/java/it/com/mycompany/myplugin` directory.

To use Selenium in these tests, the `atlassian-selenium-browsers-auto` artifact provides a few static helper methods. These methods, when used for the first time:

1.  Detect your operating system
2.  Install the appropriate browser (FireFox 3.5 is the default) for your OS in `target/seleniumTmp`
3.  If Linux and `xfvb.enable` is set to true, start `Xvfb` on an open DISPLAY detected automatically
4.  Start the Selenium server
5.  Start the newly installed browser

This all happens in the background, so you should just be able to focus on your test.

Here is a simple test that hits the home page and looks for the text of "Hello world":

``` java
import com.atlassian.selenium.SeleniumClient;
import static com.atlassian.selenium.browsers.AutoInstallClient.assertThat;
import static com.atlassian.selenium.browsers.AutoInstallClient.seleniumClient;
public class TestHelloWorld extends TestCase
{
    public void testHelloWorld() throws Exception
    {
        SeleniumClient client = seleniumClient();
        client.open("/");
        assertThat().textPresent("Hello world");
    }
}
```

## Specify a Browser

If you want to specify a browser other than Firefox 3.5, you can do so by specifying the `selenium.browser` system property in your atlassian-&lt;product&gt;-plugin configuration. For example:

``` javascript
<build>
  <plugins>
    <plugin>
      <groupId>com.atlassian.maven.plugins</groupId>
      <artifactId>maven-confluence-plugin</artifactId>
      <configuration>
        <systemPropertyVariables>
          <selenium.browser>firefox-3.6</selenium.browser> <!-- also available chrome-6 and chrome-7 -->
        </systemPropertyVariables>
      </configuration>
    </plugin>
  </plugins>
</build>
```

You can find out what strings are valid by looking at the `com.atlassian.browsers.BrowserVersion`.

# Using the Atlassian Plugin SDK with a Source Code License

This page is relevant to developers who hold a commercial license for an Atlassian application, with access to the source code.

Since you have purchased a commercial license to an Atlassian application, such as Confluence, you have access to the application source code. You can download a source distribution by visiting <a href="http://my.atlassian.com/" class="external-link">http://my.atlassian.com</a>. Then you can attach the application source code to your plugin project, so that you can step through the application code in your debugger. It is often helpful to do this to better understand the API or to track down problems.

Once you have downloaded and unpacked the source distribution, you will see a number of directories and files, exactly as they are checked out of our SVN repository. This is perfect for reading and exploring, but it does not do you much good in the brave new world of Maven 2. You'll need to create and install source artifacts into your local Maven repository. Once you have done that, the Maven IDE plugins will recognise that they are there and link them up for debugging purposes.

From the top level of the source distribution, run:  
`atlas-mvn source:jar install -Dmaven.test.skip=true -DskipTests=true`

This will build JAR files containing most of our source code into the `target` directory of each subproject. The important items are now set up, including the core application source code.

You can copy the JAR files into your local Maven repository to make them available in your IDE. For example, to install the source code for Confluence 3.4 core, copy `confluence-project/confluence/target/confluence-3.4-sources.jar` to `$HOME/.m2/repository/com/atlassian/confluence/confluence/2.10`. After doing so, run `atlas-mvn idea:idea` or `atlas-mvn eclipse:eclipse` again, close and reopen the project; the sources should now be available.

###### A Note about Memory

This is a resource intensive process, and you may need to allocate more memory to Maven in order to complete it. You can do so by setting an environment variable called `MAVEN_OPTS`, like this:  
`export MAVEN_OPTS=-Xmx512m`

###### A Note about Versions

Make sure that you download and install the **same** version of the source code that is set in the `atlassian.product.version` property in your `pom.xml`.

# Using your own log4j configuration for your plugin

The <a href="https://maven.atlassian.com/public/com/atlassian/amps/atlassian-plugin-sdk" class="external-link">Atlassian Plugin SDK</a> makes it easy to override the application's `log4j.properties` file, so that you can do custom logging for your plugin.

1.  Create your `log4j.properties` file. A simple way to do this is to copy the application's `log4j.properties` file and change it to suit your needs.
2.  Place the `log4j.properties` file somewhere in your source tree, for example in `src/aps/log4j.properties` ('aps' means the Atlassian Plugin SDK).
3.  Configure your `pom.xml` like this:

    ``` javascript
    <plugin>
      <groupId>com.atlassian.maven.plugins</groupId>
      <artifactId>maven-***-plugin</artifactId> <!-- *** is the name of the application (product) you're using -->
      <version>3.0.4</version>
      <extensions>true</extensions>
      <configuration>
        <productVersion>${product.version}</productVersion>
        <log4jProperties>src/aps/log4j.properties</log4jProperties>
      </configuration>
    </plugin>
    ```

Now you can run your application via `atlas-run` or `atlas-debug`.

{{% note %}}

A plugin specific log4j.properties file does not get picked up using this method once you deploy your plugin to another stand alone server. It only works using `atlas-run` or `atlas-debug`

{{% /note %}}

##### RELATED TOPICS

[Atlassian Plugin SDK FAQ](https://developer.atlassian.com/display/DOCS/Atlassian+Plugin+SDK+FAQ)

[Set up the Atlassian Plugin SDK and Build a Project](https://developer.atlassian.com/display/DOCS/Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project)

[Writing and Running Plugin Tests](https://developer.atlassian.com/display/DOCS/Writing+and+Running+Plugin+Tests)  
  

## Advanced Plugin Development FAQ

-   [Bundling extra dependencies in an OBR](https://developer.atlassian.com/display/DOCS/Bundling+extra+dependencies+in+an+OBR)
-   [Deployment stalled due to spaces in directory path](https://developer.atlassian.com/display/DOCS/Deployment+stalled+due+to+spaces+in+directory+path)
-   [Detecting the Presence or Absence of Classes in Different OSGI Bundles](https://developer.atlassian.com/display/DOCS/Detecting+the+Presence+or+Absence+of+Classes+in+Different+OSGI+Bundles)
-   [Getting Custom fields from Confluence V2 Searches](https://developer.atlassian.com/display/DOCS/Getting+Custom+fields+from+Confluence+V2+Searches)
-   [How to Speed Up Plugin Startup](https://developer.atlassian.com/display/DOCS/How+to+Speed+Up+Plugin+Startup)
-   [Plugins that Cannot be Reloaded with FastDev or pi](https://developer.atlassian.com/display/DOCS/Plugins+that+Cannot+be+Reloaded+with+FastDev+or+pi)
-   [Preventing Memory Leaks on Upgrades](https://developer.atlassian.com/display/DOCS/Preventing+Memory+Leaks+on+Upgrades)
-   [Supporting WebSudo in your Plugin](https://developer.atlassian.com/display/DOCS/Supporting+WebSudo+in+your+Plugin)

# FAQs for product development

## JIRA

**Content by label**

There is no content with the specified labels

## Confluence

-   Page:

    [How do I autowire a component?](/pages/viewpage.action?pageId=2031786)

-   Page:

    [How do I display the Confluence System Classpath?](/pages/viewpage.action?pageId=2031629)

-   Page:

    [How Do I find enabled and disabled plugins in the Database?](/pages/viewpage.action?pageId=2031825)

-   Page:

    [How does RENDERMODE work?](/pages/viewpage.action?pageId=2031720)

-   Page:

    [REV400 - How do I link to a comment?](/pages/viewpage.action?pageId=2031660)

-   Page:

    [How do I get the base URL and ContextPath of a Confluence installation?](/pages/viewpage.action?pageId=2031787)

-   Page:

    [How do I get my macro output exported to HTML and PDF?](/pages/viewpage.action?pageId=2031811)

-   Page:

    [How do I get hold of the HttpServletRequest?](/pages/viewpage.action?pageId=2031789)

-   Page:

    [How do I get a reference to a component?](/pages/viewpage.action?pageId=2031788)

-   Page:

    [How do I load a resource from a plugin?](/pages/viewpage.action?pageId=2031742)

-   Page:

    [What is the best way to load a class or resource from a plugin?](/pages/viewpage.action?pageId=2031736)

-   Page:

    [How do I associate my own properties with a ContentEntityObject?](/pages/viewpage.action?pageId=2031792)

-   Page:

    [How do I find the logged in user?](/pages/viewpage.action?pageId=2031739)

-   Page:

    [How do I get the location of the confluence.home directory?](/pages/viewpage.action?pageId=2031784)

-   Page:

    [How do I check which Jar file a class file belong to?](/pages/viewpage.action?pageId=2031766)

-   Page:

    [Enabling Developer Mode](/display/CONFDEV/Enabling+Developer+Mode)

-   Page:

    [What's the easiest way to render a velocity template from Java code?](/pages/viewpage.action?pageId=2031791)

-   Page:

    [What is Bandana? One form of Confluence Persistence](/pages/viewpage.action?pageId=2031780)

-   Page:

    [How do I tell if a user has permission to...?](/pages/viewpage.action?pageId=2031704)

-   Page:

    [How do I make my attachments open in a new window or a tab?](/pages/viewpage.action?pageId=2031705)

-   Page:

    [How do I prevent my rendered wiki text from being surrounded by paragraph tags?](/pages/viewpage.action?pageId=2031790)

-   Page:

    [I am trying to compile a plugin, but get an error about the target release](/display/CONFDEV/I+am+trying+to+compile+a+plugin%2C+but+get+an+error+about+the+target+release)

-   Page:

    [How do I find Confluence Test Suite?](/pages/viewpage.action?pageId=2031681)

-   Page:

    [Encrypting error messages in Sybase](/display/CONFDEV/Encrypting+error+messages+in+Sybase)

-   Page:

    [What class should my XWork action plugin extend?](/pages/viewpage.action?pageId=2031794)

-   Page:

    [What class should my macro extend?](/pages/viewpage.action?pageId=2031795)

-   Page:

    [How do I configure my Rich Text macro to receive unformatted input?](/pages/viewpage.action?pageId=14713072)

-   Page:

    [Within a Confluence macro, how do I retrieve the current ContentEntityObject?](/pages/viewpage.action?pageId=2031785)

-   Page:

    [How do I convert wiki text to HTML?](/pages/viewpage.action?pageId=2031793)

-   Page:

    [How do I get the information about Confluence such as version number, build number, build date?](/pages/viewpage.action?pageId=2031798)

-   Page:

    [How do I find information about lost attachments?](/pages/viewpage.action?pageId=2031805)

-   Page:

    [HTTP Response Code Definitions](/display/CONFDEV/HTTP+Response+Code+Definitions)

-   Page:

    [Disable Velocity Caching](/display/CONFDEV/Disable+Velocity+Caching)

## Fisheye/Crucible

This page contains answers to frequently asked questions posed by FishEye/Crucible developers.

Feel free to comment, make submissions, or pose your own question on FishEye/Crucible Development here.

-   **Q**: *I'm getting the error "API access is disabled" as a response from* <a href="http://fisheye/api/rest/repositories" class="uri external-link">http://fisheye/api/rest/repositories</a> *on my installation. How do I enable the API as a Fisheye administrator?*

    **A**: There is a toggle to enable the API under "Server Settings" in the web admin interface. See <a href="https://confluence.atlassian.com/display/FISHEYE/Configuring+the+FishEye+web+server" class="external-link">Configuring the FishEye web server</a> for more details.

<!-- -->

-   **Q**: *Is there any way to return unique results from an EyeQL query?*

    **A**: It is not currently possible to return unique results.  
    An improvement request exists: <a href="http://jira.atlassian.com/browse/FE-1136" class="external-link">FE-1136</a>. Your vote and comments on that issue are appreciated.

<!-- -->

-   **Q**: *How do I use AUI on a page generated by a servlet plugin module?*

    **A**: FishEye 2.4 and earlier don't include AUI by default, so your servlet will need to explicitly include it. There are two ways to do this:

    1.  In FishEye/Crucible 2.4 and later, specify that the context of its [page decorator](https://developer.atlassian.com/display/FECRUDEV/Page+Decorators) requires the `com.atlassian.auiplugin:ajs` resource. i.e. your `atlassian-plugin.xml` file should include:

        ``` xml
        <web-resource key="aui">
            <dependency>com.atlassian.auiplugin:ajs</dependency>
            <context>atl.general</context>
        </web-resource>
        ```

        assuming your generated page will request the `atl.general` decorator.

    2.  If you are rendering a velocity template, include `$webResourceManager.requireResource('com.atlassian.auiplugin:ajs')` in your template.

## Bamboo

-   Page:

    [How do I inject managers into my plugin?](/pages/viewpage.action?pageId=1638474)

-   Page:

    [Note to Atlassian staff on the Bamboo Developer FAQ](/display/BAMBOODEV/Note+to+Atlassian+staff+on+the+Bamboo+Developer+FAQ)

-   Page:

    [How do I search for previous build result?](/pages/viewpage.action?pageId=1638475)





























































