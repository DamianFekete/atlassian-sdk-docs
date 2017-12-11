---
aliases:
- /server/framework/atlassian-sdk/configure-netbeans-to-use-the-sdk-2818379.html
- /server/framework/atlassian-sdk/configure-netbeans-to-use-the-sdk-2818379.md
category: devguide
confluence_id: 2818379
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818379
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818379
date: '2017-12-11'
guides: guides
legacy_title: Configure NetBeans to use the SDK
platform: server
product: atlassian-sdk
subcategory: learning
title: Configure NetBeans to use the SDK
---
# Configure NetBeans to use the SDK

Partial integration between <a href="http://netbeans.org/" class="external-link">NetBeans</a> and the Atlassian Plugin SDK can be achieved.  The NetBeans IDE includes native support for Maven projects.  The Atlassian Plugin SDK includes a bundled version of Maven.

An existing NetBeans user is unlikely to want to switch to the instance of Maven that comes with the Atlassian SDK.

**Step 1** - Setup the environment so that atlas Maven commands can be invoked from the command line.[  See: Step 2. Install the Atlassian Plugin SDK](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project)  
**Step 2** - Create an empty plugin project using "atlas-create-confluence-plugin".  
**Step 3** - Modify the pom.xml

In order for NetBeans to pick up the necessary files to recognize this correctly you need to add the following to the project's **pom.xml**

``` xml
<repositories>
    <repository>
        <id>atlassian</id>
        <name>Atlassian Repository</name>
        <url>https://maven.atlassian.com/content/groups/public/</url>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
        <releases>
            <enabled>true</enabled>
        </releases>
    </repository>
</repositories>

<pluginRepositories>
    <pluginRepository>
        <id>atlassian-public</id>
        <url>https://m2proxy.atlassian.com/repository/public/</url>
        <releases>
            <enabled>true</enabled>
        </releases>
        <snapshots>
            <enabled>true</enabled>
        </snapshots>
    </pluginRepository>
</pluginRepositories>
```

and to the properties section add a reference to your locally installed Atlassian Maven repository, so that your pom.xml contains something like:

``` xml
<properties>
    <maven.local.repo>C:\Atlassian\atlassian-plugin-sdk-3.2\repository</maven.local.repo>        
    <confluence.version>3.3</confluence.version>
    <confluence.data.version>3.1</confluence.data.version>
</properties>
```

Open the project in NetBeans, it will report that the project is unloadable. To resolve this you need to perform a priming build.

1.  Right-click the project in the Projects tab
2.  Choose "Show and Resolve Problems..." which should be the second last entry
3.  Click the button labelled "Resolve..." for NetBeans 7.3 and later; or, the button labelled "Priming Build" in NetBeans 7.2.x and earlier.

The project will perform an initial build and load correctly once complete. Check the output window for the build status. After this Netbeans should recognize the plugin and be able to perform all the usual dependency maintenance and code editing as per usual. You just need to remember to do any actual compilation and packaging using the atlas-mvn command line tools.

{{% tip %}}

Running from within Netbeans

If you want to start the plugin from within the Netbeans IDE, and not from the atlas-mvn command line tools, you can customize the project options in Netbeans to add the goal that is internally executed by the atlas-mvn commands. For example, to add the 'atlas-run' command

-   In the project properties, under Actions, select 'Run Project' and enter *com.atlassian.maven.plugins:maven-amps-dispatcher-plugin:3.7.3:run* in 'Execute Goals'.
-   With this, hitting F6 in Netbeans (or 'Run' menu 'Run Project') will launch the equivalent of 'atlas-run'

{{% /tip %}}















































































































































































































































































































