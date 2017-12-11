---
aliases:
- /server/framework/atlassian-sdk/unsatisfiabledependenciesexception-2818382.html
- /server/framework/atlassian-sdk/unsatisfiabledependenciesexception-2818382.md
category: devguide
confluence_id: 2818382
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818382
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818382
date: '2017-12-11'
legacy_title: UnsatisfiableDependenciesException
platform: server
product: atlassian-sdk
subcategory: faq
title: UnsatisfiableDependenciesException
---
# UnsatisfiableDependenciesException

#### Symptom: "UnsatisfiableDependenciesException"

**Cause**: you can refer to a Pico component in an OSGI plugin by getting the container, but Pico cannot reference OSGI components

**Solution**: TODO

**Example**:

``` bash
org.picocontainer.defaults.UnsatisfiableDependenciesException: 
com.atlassian.plugins.tutorial.workflow.sla.condition.TimeElapsedSinceCreationCondition doesn't have any satisfiable constructors. 
Unsatisfiable dependencies: [[interface com.atlassian.plugins.tutorial.workflow.sla.util.SLATimestampUtils]]
```























































































































































































































