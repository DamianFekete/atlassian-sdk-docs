---
title: Build Failure Manifest Validation Errors 2818376
aliases:
    - /server/framework/atlassian-sdk/build-failure-manifest-validation-errors-2818376.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818376
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818376
confluence_id: 2818376
platform:
product:
category:
subcategory:
---
# Documentation : Build Failure - Manifest Validation Errors

If you use a vendor name of "Atlassian" in your `atlassian-plugin.xml` file, you may receive errors like this:

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

To **skip the manifest validation**, you can add the following tag to the configuration element in your pom.xml

``` javascript
<skipManifestValidation>true</skipManifestValidation>
```

Note: This is not recommended if you want to make your plugin available to multiple Atlassian applications.

##### RELATED TOPICS

[Writing your first plugin FAQ](/server/framework/atlassian-sdk/writing-your-first-plugin-faq)  
<a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Writing+your+first+plugin&amp;linkCreation=true&amp;fromPageId=2818376" class="createlink">Writing your first plugin</a>
