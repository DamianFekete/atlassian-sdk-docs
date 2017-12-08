---
aliases:
- /server/framework/atlassian-sdk/servlet-modules-851996.html
- /server/framework/atlassian-sdk/servlet-modules-851996.md
category: reference
confluence_id: 851996
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851996
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851996
date: '2017-12-08'
legacy_title: Servlet Modules
platform: server
product: atlassian-sdk
subcategory: modules
title: Servlet modules
---
# Servlet modules

The Atlassian Plugin framework ships with the atlassian-plugin-servlet jar that contains several module types for providing implementations of key Servlet interfaces:

1.  HttpServlet -&gt; ServletModuleDescriptor
2.  Filter -&gt; ServletFilterModuleDescriptor
3.  ServletContextListener -&gt; ServletContextListenerModuleDescriptor
4.  Context parameters -&gt; ServletContextParamModuleDescriptor

Before any of these can be used, you need to perform a few setup steps:

1.  Copy the atlassian-plugin-servlet jar into your application
2.  Define, if you haven't already, a `HostContainer` instance as a bean in your application. Its implementation should delegate to your `BeanFactory` (or equivalent) for class instantiation.
3.  Define the `DefaultServletModuleManager` as a bean in your application. It is recommended this bean is also exposed as a host component. See [Exposing Host Components via Spring](/server/framework/atlassian-sdk/exposing-host-components-via-spring) for more information.
4.  Add the desired module descriptors to your instance of `DefaultModuleDescriptorFactory`

Some descriptors require additional configuration:

**ServletModuleDescriptor**

1.  Define the delegating servlet in `web.xml` that will delegate to plugin-provided servlets:

    ``` xml
    <servlet>
        <servlet-name>plugins</servlet-name>
        <servlet-class>com.atlassian.plugin.servlet.ServletModuleContainerServlet</servlet-class>
    </servlet>
    ```

2.  Define the servlet mapping in `web.xml`. While you can choose any mapping, it is recommended to go with `/plugins/servlet`:

    ``` xml
    <servlet-mapping>
        <servlet-name>plugins</servlet-name>
        <url-pattern>/plugins/servlet/*</url-pattern>
    </servlet-mapping>
    ```

**ServletFilterModuleDescriptor**

1.  Define four delegating filters in `web.xml` that will delegate to the plugin-provided filters:
    1.  after-encoding - This filter should as high up the chain as possible with only any request encoding filters ahead of it:

        ``` xml
        <filter>
            <filter-name>filter-plugin-dispatcher-after-encoding</filter-name>
            <filter-class>com.atlassian.plugin.servlet.filter.ServletFilterModuleContainerFilter</filter-class>
            <init-param>
                <param-name>location</param-name>
                <param-value>after-encoding</param-value>
            </init-param>
        </filter>
        ```

    2.  after-encoding - This filter should as high up the chain as possible with only any request encoding filters ahead of it:

        ``` xml
        <filter>
            <filter-name>filter-plugin-dispatcher-after-encoding</filter-name>
            <filter-class>com.atlassian.plugin.servlet.filter.ServletFilterModuleContainerFilter</filter-class>
            <init-param>
                <param-name>location</param-name>
                <param-value>after-encoding</param-value>
            </init-param>
        </filter>
        ```

    3.  before-login - This filter should right before any authentication filters:

        ``` xml
        <filter>
            <filter-name>filter-plugin-dispatcher-before-login</filter-name>
            <filter-class>com.atlassian.plugin.servlet.filter.ServletFilterModuleContainerFilter</filter-class>
            <init-param>
                <param-name>location</param-name>
                <param-value>before-login</param-value>
            </init-param>
        </filter>
        ```

    4.  before-decoration - This filter should go before any decorating filters like Sitemesh:

        ``` xml
        <filter>
            <filter-name>filter-plugin-dispatcher-before-decoration</filter-name>
            <filter-class>com.atlassian.plugin.servlet.filter.ServletFilterModuleContainerFilter</filter-class>
            <init-param>
                <param-name>location</param-name>
                <param-value>before-decoration</param-value>
            </init-param>
        </filter>
        ```

    5.  before-dispatch - This filter should go before the servlet or filter that dispatches to your web framework:

        ``` xml
        <filter>
            <filter-name>filter-plugin-dispatcher-before-dispatch</filter-name>
            <filter-class>com.atlassian.plugin.servlet.filter.ServletFilterModuleContainerFilter</filter-class>
            <init-param>
                <param-name>location</param-name>
                <param-value>before-dispatch</param-value>
            </init-param>
        </filter>
        ```

2.  Define the servlet filter mappings in `web.xml`.

    ``` xml
    <filter-mapping>
            <filter-name>my-request-encoder</filter-name>
            <url-pattern>/*</url-pattern>
        </filter-mapping>
        <filter-mapping>
            <filter-name>filter-plugin-dispatcher-after-encoding</filter-name>
            <url-pattern>/*</url-pattern>    
        </filter-mapping>
        
        <filter-mapping>
            <filter-name>my-url-rewriter</filter-name>
            <url-pattern>/foo/*</url-pattern>
        </filter-mapping>

        <filter-mapping>
            <filter-name>filter-plugin-dispatcher-before-login</filter-name>
            <url-pattern>/*</url-pattern>
        </filter-mapping>

        <filter-mapping>
            <filter-name>my-login-filter</filter-name>
            <url-pattern>/*</url-pattern>
        </filter-mapping>

        <filter-mapping>
            <filter-name>filter-plugin-dispatcher-before-decoration</filter-name>
            <url-pattern>/*</url-pattern>
        </filter-mapping>

        <filter-mapping>
            <filter-name>my-decorating-filter</filter-name>
            <url-pattern>/*</url-pattern>
        </filter-mapping>

        <filter-mapping>
            <filter-name>filter-plugin-dispatcher-before-dispatch</filter-name>
            <url-pattern>/*</url-pattern>    
        </filter-mapping>

        <filter-mapping>
            <filter-name>my-web-framework</filter-name>
            <url-pattern>/*</url-pattern>    
        </filter-mapping>
    ```





















































































































































































































