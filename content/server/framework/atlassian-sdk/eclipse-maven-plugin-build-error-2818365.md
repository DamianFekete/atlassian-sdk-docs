---
title: Eclipse Maven Plugin Build Error 2818365
aliases:
    - /server/framework/atlassian-sdk/eclipse-maven-plugin-build-error-2818365.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818365
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818365
confluence_id: 2818365
platform:
product:
category:
subcategory:
---
# Documentation : Eclipse Maven Plugin Build Error

Please note that the new Eclipse plugin is unable to deal with source 'includes' and 'excludes'.

Use the following command :`mvn org.apache.maven.plugins:maven-eclipse-plugin:2.6:eclipse` as this will force mvn to use version 2.6 of the maven eclipse plugin.

The error that you will see if 2.7 is used in your mvn build :

    [ERROR] BUILD ERROR
    [INFO] ------------------------------------------------------------------------
    [INFO] Request to merge when 'filtering' is not identical. 
    [INFO] Original=resource src/main/resources: output=target/classes, 
    [INFO]    include=[atlassian-plugin.xml], exclude=[**/*.java], test=false, 
    [INFO]    filtering=true, merging with=resource src/main/resources: 
    [INFO]    output=target/classes, include=[], exclude=[atlassian-plugin.xml|**/*.java], 
    [INFO]    test=false, filtering=false
    [INFO] ------------------------------------------------------------------------
    [INFO] For more information, run Maven with the -e switch
    [INFO] ------------------------------------------------------------------------

























