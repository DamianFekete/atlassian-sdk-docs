---
title: Beancreationexception From Spring Framework 2818633
aliases:
    - /server/framework/atlassian-sdk/beancreationexception-from-spring-framework-2818633.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818633
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818633
confluence_id: 2818633
platform:
product:
category:
subcategory:
---
# BeanCreationException from Spring Framework

If you get an error like the one below when you attempt to use your plugin, check that your `atlassian-plugin.xml` file (i.e. your [plugin descriptor](/server/framework/atlassian-sdk/configuring-the-plugin-descriptor-852008.html)) contains `plugins-version="2"`.

## The Error

> Unable to render content due to system error: org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'com.sarah.confluence.plugins.ExampleMacro': Instantiation of bean failed; nested exception is org.springframework.beans.BeanInstantiationException: Could not instantiate bean class \[com.sarah.confluence.plugins.ExampleMacro\]: No default constructor found; nested exception is java.lang.NoSuchMethodException: com.sarah.confluence.plugins.ExampleMacro.&lt;init&gt;()

## The Solution

To fix the problem:

1.  Stop the Confluence server. (Go to the server command window and press Ctrl-C.)
2.  Add `plugins-version="2"` to the `<atlassian-plugin>` element in your `atlassian-plugin.xml` file. It will look something like this:

    ``` xml
    <atlassian-plugin key="${groupId}.${artifactId}" name="${artifactId}" plugins-version="2">
    ```

    Or this:

    ``` xml
    <atlassian-plugin key="com.atlassian.confluence.plugins.example" name="Example Plugin" plugins-version="2">
    ```

3.  Run `amps-clean`.
4.  Run `amps-run` again.
5.  Go to the application in your browser and try again.

##### RELATED TOPICS

[Advanced Plugin Development FAQ](/server/framework/atlassian-sdk/advanced-plugin-development-faq-2818634.html)  
[Advanced Topics](/server/framework/atlassian-sdk/advanced-topics-2818630.html)

























