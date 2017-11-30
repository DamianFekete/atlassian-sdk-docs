---
aliases:
- /server/framework/atlassian-sdk/unsatisfieddependencyexception-error-creating-bean-with-name-2818380.html
- /server/framework/atlassian-sdk/unsatisfieddependencyexception-error-creating-bean-with-name-2818380.md
category: devguide
confluence_id: 2818380
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818380
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818380
legacy_url: https://developer.atlassian.com/docs/faq/troubleshooting/unsatisfieddependencyexception-error-creating-bean-with-name
new_url: /server/framework/atlassian-sdk/unsatisfieddependencyexception-error-creating-bean-with-name
platform: server
product: atlassian-sdk
subcategory: other
title: UnsatisfiedDependencyException - error creating bean with name
---
# UnsatisfiedDependencyException - error creating bean with name

#### Symptom: "UnsatisfiedDependencyException: Error creating bean with name", "Unsatisfied dependency expressed through constructor argument with index 1"

**Cause**: the class is unknown to the OSGI plugin

**Solution**: add a `component-import` element in the `atlassian-plugin.xml` file to import the necessary class. See the <a href="http://confluence.atlassian.com/display/PLUGINFRAMEWORK/Component+Import+Plugin+Module" class="external-link">Component Import</a> plugin module for an example of what this element does.

Other useful introductions include [OSGi, Spring and the Plugin Framework](/server/framework/atlassian-sdk/852146.html) and [Automatic Generation of Spring Configuration](/server/framework/atlassian-sdk/automatic-generation-of-spring-configuration).

**Example**:

``` text
2010-02-23 14:15:46,831 http-8080-Processor25 ERROR admin 51345x1x1 1hageqe http://localhost:8080/rest/example/1.0/myplugin 
[atlassian.plugin.servlet.DefaultServletModuleManager] Unable to create filter
com.atlassian.plugin.servlet.util.LazyLoadedReference$InitializationException: 
org.springframework.beans.factory.UnsatisfiedDependencyException: Error creating bean with name 'com.example.jira.plugins.MyPlugin': 
Unsatisfied dependency expressed through constructor argument with index 1 of type [com.atlassian.sal.api.user.UserManager]: :
 No unique bean of type [com.atlassian.sal.api.user.UserManager] is defined: 
Unsatisfied dependency of type [interface com.atlassian.sal.api.user.UserManager]: expected at least 1 matching bean; 
nested exception is org.springframework.beans.factory.NoSuchBeanDefinitionException: No unique bean of type [com.atlassian.sal.api.user.UserManager] is defined: 
Unsatisfied dependency of type [interface com.atlassian.sal.api.user.UserManager]: expected at least 1 matching bean
    at com.atlassian.plugin.servlet.util.LazyLoadedReference.get(LazyLoadedReference.java:94)
...
```

Note that the first argument to the constructor has index 0, not index 1.

Add this to `atlassian-plugin.xml` so that the plugin knows about the missing class:

``` xml
<component-import key="userManager" interface="com.atlassian.sal.api.user.UserManager"/>
```

A good rule of thumb is to be careful with any class whose package doesn't start with `com.atlassian.JIRA`

Note that `component-import` may not always work if the host application exposes more than one bean under the same interface. The safest way is to use Constructor Injection is in combination with `@Qualifier` Spring annotation. See [the Plugin Framework documentation](https://developer.atlassian.com/display/DOCS/Converting+from+Version+1+to+Version+2+%28OSGi%29+Plugins#ConvertingfromVersion1toVersion2%28OSGi%29Plugins-3.1SpecifyqualifiersonambiguousSpringdependencies) for information on how to use `@Qualifier` to avoid ambiguity in your constructor.

**Beyond DI**

If using a `component-import` doesn't work you may be able to instantiate the object using `ManagerFactory.getMyObject()`  
or `ComponentManager.getInstance().getMyObject()`, or even `ComponentManager.getInstance().getComponentInstanceOfType(MyObject.class)`.

















