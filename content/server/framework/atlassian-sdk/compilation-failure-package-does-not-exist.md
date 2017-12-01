---
aliases:
- /server/framework/atlassian-sdk/compilation-failure-package-does-not-exist-2818393.html
- /server/framework/atlassian-sdk/compilation-failure-package-does-not-exist-2818393.md
category: devguide
confluence_id: 2818393
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818393
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818393
legacy_url: https://developer.atlassian.com/docs/faq/troubleshooting/compilation-failure-package-does-not-exist
new_url: /server/framework/atlassian-sdk/compilation-failure-package-does-not-exist
platform: server
product: atlassian-sdk
subcategory: other
title: Compilation failure - package does not exist
---
# Compilation failure - package does not exist

#### Symptom: "Compilation failure: package does not exist"

**Cause**: the `javac` compile command did not have one or more required `.jar` files specified on the classpath

**Solution**: add a `dependency` element in `pom.xml` for the artifact that contains the missing class

**Example**: `package javax.servlet.http does not exist`

Add this element to `pom.xml`:

``` xml
    <dependency>
        <groupId>javax.servlet</groupId>
        <artifactId>servlet-api</artifactId>
        <version>2.3</version>
        <scope>provided</scope>
    </dependency>
```

{{% note %}}

How do I find the correct artifact name and version? Best practice is to use the same version as the jar file shipped with the version of JIRA, Confluence etc you are building with.  
The `provided` scope element indicates that the jar file doesn't need to be packaged with the plugin since the main application can already provide it.

{{% /note %}}




































































