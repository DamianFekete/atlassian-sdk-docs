---
aliases:
- /server/framework/atlassian-sdk/differences-between-spring-and-pico-852131.html
- /server/framework/atlassian-sdk/differences-between-spring-and-pico-852131.md
category: devguide
confluence_id: 852131
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852131
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852131
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/plugin-framework-faq/differences-between-spring-and-pico
new_url: /server/framework/atlassian-sdk/differences-between-spring-and-pico
platform: server
product: atlassian-sdk
subcategory: other
title: Differences between Spring and Pico
---
# Differences between Spring and Pico

{{% note %}}

Applicable to JIRA plugin development only

{{% /note %}}

Version 1 plugins in JIRA use the internal Pico Container system to inject dependencies into plugin components. Version 2 plugins in JIRA or any other Atlassian application use Spring 2.5, which is set to default to constructor injection. While both support constructor injection, there are subtle differences:

1.  Spring looks for constructors in the order of the number of arguments, regardless of access modifier. Pico only looks at public constructors. This means if you use no-arg public constructors but have private constructors with multiple arguments for testing, Spring will try to use the private constructors, and throw exceptions if it is unsuccessful. The workaround is to configure the bean directly in Spring XML configuration by placing your configuration file in `META-INF/spring`.







































