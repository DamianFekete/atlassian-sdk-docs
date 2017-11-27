---
aliases:
- /server/framework/atlassian-sdk/advanced-configuration-with-spring-xml-files-6849823.html
- /server/framework/atlassian-sdk/advanced-configuration-with-spring-xml-files-6849823.md
category: devguide
confluence_id: 6849823
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=6849823
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=6849823
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/plugin-framework/advanced-configuration-with-spring-xml-files
new_url: /server/framework/atlassian-sdk/advanced-configuration-with-spring-xml-files
platform: server
product: atlassian-sdk
subcategory: learning
title: Advanced configuration with Spring XML files
---
# Advanced configuration with Spring XML files

The plugin framework provides the ability to create plugin components using complete Spring configuration files. If you provide Spring Dynamic Modules (Spring DM) configuration files in `META-INF/spring/`, these will be loaded into your plugin OSGi bundle by the Spring DM loader. Using this option for configuration provides you with a lot of flexibility about how your plugin components are created and managed.

``` xml
<?xml version="1.0" encoding="UTF-8"?>
<beans:beans xmlns:beans="http://www.springframework.org/schema/beans" 
             xmlns:osgi="http://www.springframework.org/schema/osgi" 
             xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance" 
             xsi:schemaLocation="http://www.springframework.org/schema/beans http://www.springframework.org/schema/beans/spring-beans-2.5.xsd http://www.springframework.org/schema/osgi http://www.springframework.org/schema/osgi/spring-osgi.xsd" 
             default-autowire="autodetect">
        <beans:bean id="repositoryManager" class="com.atlassian.plugin.repository.logic.ConfluenceRepositoryManager"/>
</beans:beans>
```

To include a Spring configuration file, ensure it is included in the `META-INF/spring/` directory inside your plugin JAR file. All files matching `*.xml` inside this directory will be loaded as Spring configuration files when your plugin is loaded. For more details on Spring configuration, see the <a href="http://www.springframework.org/" class="external-link">Spring documentation</a>.

#### Related topics

<a href="/pages/createpage.action?spaceKey=PLUGINFRAMEWORK&amp;title=Converting+from+Version+1+to+Version+2+%28OSGi%29+Plugins" class="createlink">Converting from Version 1 to Version 2 (OSGi) Plugins</a>  
<a href="/pages/createpage.action?spaceKey=PLUGINFRAMEWORK&amp;title=OSGi%2C+Spring+and+the+Plugin+Framework" class="createlink">OSGi, Spring and the Plugin Framework</a>  
[Writing Atlassian Plugins](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Writing+Atlassian+Plugins)  
[Managing Plugin Dependencies](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Managing+Plugin+Dependencies)






























































































































































































































































