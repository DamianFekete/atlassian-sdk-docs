---
aliases:
- /server/framework/atlassian-sdk/setting-the-platform-version-dependency-in-the-pom-2818408.html
- /server/framework/atlassian-sdk/setting-the-platform-version-dependency-in-the-pom-2818408.md
category: devguide
confluence_id: 2818408
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818408
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818408
learning: guides
legacy_url: https://developer.atlassian.com/docs/getting-started/working-with-the-pom/setting-the-platform-version-dependency-in-the-pom
new_url: /server/framework/atlassian-sdk/setting-the-platform-version-dependency-in-the-pom
platform: server
product: atlassian-sdk
subcategory: learning
title: Setting the platform version dependency in the POM
---
# Setting the platform version dependency in the POM

It can be cumbersome to update version numbers of platform modules whenever you need to update to a new version of the [Atlassian Platform Common Components](/server/framework/atlassian-sdk/atlassian-platform-common-components).

To avoid this, you can have just one version to maintain by using the `atlassian-platform-libraries` and `atlassian-platform-plugins` POM artifacts to set the versions via Maven's <a href="http://maven.apache.org/guides/introduction/introduction-to-dependency-mechanism.html#Importing_Dependencies" class="external-link">import scope</a>. This allows you to change the platform version and have all the appropriate versions of platform modules set automatically.

For your web application, add this to your `dependencyManagement` section:

``` xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.atlassian.refapp</groupId>
            <artifactId>atlassian-platform-libraries</artifactId>
            <version>2.7.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

For your bundled plugins module that builds the bundled plugins archive, add this:

``` xml
<dependencyManagement>
    <dependencies>
        <dependency>
            <groupId>com.atlassian.refapp</groupId>
            <artifactId>atlassian-platform-plugins</artifactId>
            <version>2.7.0</version>
            <type>pom</type>
            <scope>import</scope>
        </dependency>
    </dependencies>
</dependencyManagement>
```

With these elements in place, you can now remove the version elements for all platform libraries and plugins.

For consistency, we recommend that you use a Maven property for the version to allow easy overriding: `platform.version`

{{% note %}}

If you are depending on a project that contains the above `dependencyManagement` stanza, you may receive an error similar to:

``` xml
[INFO] Unable to find resource 'com.atlassian.refapp:atlassian-platform-libraries:pom:2.7.0' in repository central (http://repo1.maven.org/maven2)
[INFO] ------------------------------------------------------------------------
[ERROR] BUILD ERROR
[INFO] ------------------------------------------------------------------------
[INFO] Error building POM (may not be this project's POM).


Project ID: com.atlassian.refapp:atlassian-platform-libraries

Reason: POM 'com.atlassian.refapp:atlassian-platform-libraries' not found in repository: Unable to download the artifact from any repository

  com.atlassian.refapp:atlassian-platform-libraries:pom:2.7.0

from the specified remote repositories:
  central (http://repo1.maven.org/maven2)

 for project com.atlassian.refapp:atlassian-platform-libraries

[INFO] ------------------------------------------------------------------------
[INFO] For more information, run Maven with the -e switch
[INFO] ------------------------------------------------------------------------
```

  
This is due to a bug (<a href="http://jira.codehaus.org/browse/MNG-4148" class="external-link">MNG-4148</a>) in Maven 2.x where profiles specified in `settings.xml` are ignored.

Apart from upgrading to Maven 3.x, there is currently no workaround for this.

Note that this does not affect projects that have the above `dependencyManagement` in their POM. For example, if project A has the stanza, it will build successfully. However, if project B depends on project A, it will cause the error mentioned above.

{{% /note %}}

##### RELATED TOPICS

[Atlassian Platform Common Components](/server/framework/atlassian-sdk/atlassian-platform-common-components)  
[Plugin Framework 2.6 Migration Guide](https://developer.atlassian.com/pages/viewpage.action?pageId=852068)








































































































