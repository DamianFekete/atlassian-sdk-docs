---
title: Troubleshooting 2818641
aliases:
    - /server/framework/atlassian-sdk/troubleshooting-2818641.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818641
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818641
confluence_id: 2818641
platform:
product:
category:
subcategory:
---
# Troubleshooting

This page contains guidelines for resolving errors related to classes not being found by a plugin. Some of these errors are due to unresolved Maven dependencies, some are due to OSGI dependencies. These errors were all generated using JIRA plugins but apply to all Atlassian applications.

{{% note %}}

Some of these bundle gotchas can be debugged using the <a href="http://confluence.atlassian.com/display/PLUGINFRAMEWORK/Troubleshooting+a+BundleException" class="external-link">Felix Web Console</a> or better still, the <a href="http://blogs.atlassian.com/developer/2011/01/announcing_upm_1_dot_3_and_osgi_tab.html" class="external-link">OSGI</a> tab in the Universal Plugin Manager (UPM) version 1.3 and later (JIRA 4.3+).

{{% /note %}}

## Types of errors

Errors typically fall into these categories:

-   *Compile time errors* are triggered by any PDK command that starts a `javac` compile such as `atlas-compile`, `atlas-package` or even `mvn package`. These go beyond the usual "cannot find symbol" <a href="http://mindprod.com/jgloss/compileerrormessages.html" class="external-link">Java compilation errors</a> due to typos in the method or class name, or missing import statements, or typos in a package name.For an example, see [Compilation failure: package does not exist](#compilation-failure:-package-does-not-exist).
-   Start up errors are triggered when your new plugin is deployed and the application starts up. The application log file contains errors or warnings about it even before you try to use the plugin. An example of this type of error is [Cannot start plugin](#cannot-start-plugin).
-   Run time errors are triggered when a new plugin is used and the application log file contains an error the first time the plugin is used. Note the following points for diagnosing these errors:

    -   Some of these errors and warnings only appear in `logs/catalina.out` and not in `atlassian-jira.log`
    -   If one REST resource in a plugin has a problem, then all the other resources and their URLs will produce HTTP 404 errors

    Examples of these error are[NoClassDefFoundError](#noclassdeffounderror)[, UnsatisfiedDependencyException](#,-unsatisfieddependencyexception)[,](#,)[java.lang.LinkageError](#,)[, PluginException](#,-pluginexception)[, SAXParserContextProvider](#,-saxparsercontextprovider), and so on.

## Troubleshooting topics

-   [BeanCreationException from Spring Framework](/server/framework/atlassian-sdk/beancreationexception-from-spring-framework-2818633.html)
-   [BundleException](/server/framework/atlassian-sdk/bundleexception-852121.html)
-   [BundleException with no bundle constraint specified](/server/framework/atlassian-sdk/bundleexception-with-no-bundle-constraint-specified-851974.html)
-   [Cannot start plugin](/server/framework/atlassian-sdk/cannot-start-plugin-2818394.html)
-   [Dependency Issues during Plugin Initialisation](/server/framework/atlassian-sdk/dependency-issues-during-plugin-initialisation-852094.html)
-   [ClassNotFoundException](/server/framework/atlassian-sdk/classnotfoundexception-851975.html)
-   [Compilation failure - package does not exist](/server/framework/atlassian-sdk/compilation-failure-package-does-not-exist-2818393.html)
-   [java.lang.LinkageError - loader constraints violated](/server/framework/atlassian-sdk/java.lang.linkageerror-loader-constraints-violated-2818383.html)
-   [LinkageError](/server/framework/atlassian-sdk/linkageerror-851986.html)
-   [NoClassDefFoundError](/server/framework/atlassian-sdk/noclassdeffounderror-2818395.html)
-   [PluginException](/server/framework/atlassian-sdk/pluginexception-2818384.html)
-   [SAXParserContextProvider](/server/framework/atlassian-sdk/saxparsercontextprovider-2818385.html)
-   [UnsatisfiableDependenciesException](/server/framework/atlassian-sdk/unsatisfiabledependenciesexception-2818382.html)
-   [UnsatisfiedDependencyException - Error creating bean with name](/server/framework/atlassian-sdk/unsatisfieddependencyexception-error-creating-bean-with-name-2818380.html)
-   [Velocity in OSGi](/server/framework/atlassian-sdk/velocity-in-osgi-851989.html)

## Resources

-   [Using the OSGi Browser](/server/framework/atlassian-sdk/using-the-osgi-browser)
-   [Accessing Classes from Another Plugin](/server/framework/atlassian-sdk/accessing-classes-from-another-plugin-852151.html)
-   [Velocity in OSGi](/server/framework/atlassian-sdk/velocity-in-osgi-851989.html)
-   [Configuring the Plugin Descriptor](/server/framework/atlassian-sdk/configuring-the-plugin-descriptor)

 





















































































































































































































































