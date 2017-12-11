---
aliases:
- /server/framework/atlassian-sdk/noclassdeffounderror-2818395.html
- /server/framework/atlassian-sdk/noclassdeffounderror-2818395.md
category: devguide
confluence_id: 2818395
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818395
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818395
date: '2017-12-11'
legacy_title: NoClassDefFoundError
platform: server
product: atlassian-sdk
subcategory: faq
title: NoClassDefFoundError
---
# NoClassDefFoundError

#### Symptom: "NoClassDefFoundError: com/atlassian/jira/gadgets/system/AbstractResource"

**Cause**: a plugin is lazily instantiated and then fails to find a needed class

**Solution**: make sure the class and package name are correct and that the class is declared as a `component` in its `atlassian-plugin.xml`.

**Simple Example**:

``` bash
2010-02-23 13:17:10,611 http-8080-Processor19 ERROR admin 47830x17x3 1bvaudl 
http://localhost:8080/rest/gadget/1.0/stats/generate [atlassian.plugin.servlet.DefaultServletModuleManager] Unable to create filter
com.atlassian.plugin.servlet.util.LazyLoadedReference$InitializationException: java.lang.NoClassDefFoundError: com/atlassian/jira/gadgets/system/AbstractResource
    at com.atlassian.plugin.servlet.util.LazyLoadedReference.get(LazyLoadedReference.java:94)
...
```

In this case, the class using `AbstractResource` class was in the wrong package. Unfortunately, the name of the actual class in the plugin that required the missing class does not appear in the log file.

**A More Complex Example**

``` bash
2010-02-23 16:20:22,917 http-8080-Processor25 ERROR admin 58822x1x1 17hs118 
http://localhost:8080/rest/example/1.0/myplugin [atlassian.plugin.servlet.DefaultServletModuleManager] Unable to create filter
com.atlassian.plugin.servlet.util.LazyLoadedReference$InitializationException: java.lang.NoClassDefFoundError: com/atlassian/jira/gadgets/system/SearchQueryBackedResource
    at com.atlassian.plugin.servlet.util.LazyLoadedReference.get(LazyLoadedReference.java:94)
...
```

In this case, the `SearchQueryBackedResource` class was not exported by the `atlassian-plugin.xml` file. The workaround is to copy the required class (and all the classes it requires in turn) to your gadget source tree. Alternatively <a href="http://jira.atlassian.com/browse/JRA-18986" class="external-link">JRA-18986</a> recommends creating a simple class in your plugin that wraps the core JIRA class and just calls `super()`.


























































































































































































































