---
aliases:
- /server/framework/atlassian-sdk/java.lang.linkageerror-loader-constraints-violated-2818383.html
- /server/framework/atlassian-sdk/java.lang.linkageerror-loader-constraints-violated-2818383.md
category: devguide
confluence_id: 2818383
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818383
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818383
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/troubleshooting/java-lang-linkageerror-loader-constraints-violated
new_url: /server/framework/atlassian-sdk/java-lang-linkageerror-loader-constraints-violated
platform: server
product: atlassian-sdk
subcategory: other
title: java.lang.LinkageError - loader constraints violated
---
# java.lang.LinkageError - loader constraints violated

#### Symptom: "BeanCreationException: Error creating bean with name", "java.lang.LinkageError: loader constraints violated"

**Cause**: the class has already been loaded from different location than the plugin

**Solution**: see <a href="http://confluence.atlassian.com/display/PLUGINFRAMEWORK/Troubleshooting+a+LinkageError" class="uri external-link">http://confluence.atlassian.com/display/PLUGINFRAMEWORK/Troubleshooting+a+LinkageError</a>

**Example**:

    2010-02-23 13:29:51,421 http-8080-Processor25 ERROR admin 48590x7x1 b0gp1r 
    http://localhost:8080/rest/gadget/1.0/stats/generate [atlassian.plugin.servlet.DefaultServletModuleManager] Unable to create filter
    com.atlassian.plugin.servlet.util.LazyLoadedReference$InitializationException: 
    org.springframework.beans.factory.BeanCreationException: Error creating bean with name 'com.atlassian.jira.gadgets.stats.IssueTableResource': 
    Instantiation of bean failed; nested exception is java.lang.LinkageError: loader constraints violated when linking org/apache/log4j/Logger class
        at com.atlassian.plugin.servlet.util.LazyLoadedReference.get(LazyLoadedReference.java:94)
    ...

In this case the `log4j` class appears to be the cause of the error. Note that this error will also occur if your plugin has imported but not otherwise used the class that is using the missing class (so beware of `import foo.*` statements).





















