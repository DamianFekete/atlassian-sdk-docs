---
aliases:
- /server/framework/atlassian-sdk/configure-amps-to-run-jira-core-with-additional-applications-installed-34669832.html
- /server/framework/atlassian-sdk/configure-amps-to-run-jira-core-with-additional-applications-installed-34669832.md
category: devguide
confluence_id: 34669832
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=34669832
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=34669832
date: '2017-12-11'
guides: guides
legacy_title: Configure AMPS to run JIRA Core with additional applications installed
platform: server
product: atlassian-sdk
subcategory: learning
title: Configure AMPS to run JIRA Core with additional applications installed
---
# Configure AMPS to run JIRA Core with additional applications installed

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p>Atlassian AMPS 5.1.7 and later.</p></td>
</tr>
</tbody>
</table>

 

## Overview

Add-ons that integrate with functionality provided by applications, such as JIRA Software or JIRA Service Desk, need to run their tests against a JIRA instance with those applications installed. This document describes how it can be done using AMPS's new configuration tag: `applications`. You'll also find some advanced examples that illustrate how this feature can be used to test add-ons with complicated dependencies and complex AMPS configurations.

## Configuring applications

Atlassian AMPS 5.1.7 and above supports a new element: `applications.`` `This element defines a list of additional applications that should be installed on another tested product. For example, the following configuration will install JIRA Software and JIRA Service Desk on top of JIRA Core:

``` xml
<plugin>
    <groupId>com.atlassian.maven.plugins</groupId>
    <artifactId>maven-jira-plugin</artifactId>
    <configuration>
        <applications>
            <application>
                <applicationKey>jira-software</applicationKey>
                <version>${jira.software.application.version}</version>
            </application>
            <application>
                <applicationKey>jira-servicedesk</applicationKey>
                <version>${jira.servicedesk.application.version}</version>
            </application>
        </applications>
    </configuration>
</plugin>
```

For each application that should be installed, you must define an `application` element that has the following two child elements:

-   `applicationKey` -- identifies the application to be installed
-   `version -- `defines the version of the application to be installed

If more than one application is defined, the product will run with all defined applications installed. Applications are installed into the product's home directory, so changing application versions or removing an application from the applications list may require you to run `mvn clean`.

## Advanced configurations

There are three important characteristics of the `applications` element that makes this feature quite flexible:

-   The `<applications>` element can be applied on both the global configuration level and the per product element. For example, you could configure it like this:

    ``` xml
    <plugin>
        <groupId>com.atlassian.maven.plugins</groupId>
        <artifactId>maven-amps-plugin</artifactId>
        <configuration>
            <products>
                <product>
                    <id>jira</id>
                    <instanceId>jira</instanceId>
                    <version>${jira.version}</version>
                    <applications>
                        <application>
                            <applicationKey>jira-software</applicationKey>
                            <version>${jira.software.application.version}</version>
                        </application>
                    </applications>
                </product>
                <product>
                     <id>confluence</id>
                     <instanceId>confluence</instanceId>
                     <version>${confluence.version}</version>
                </product>
            </products>
        </configuration>
    </plugin>
    ```

-   Application keys are defined per product Id. This means that, for example,* *`jira-software` is defined for product `jira` and will be ignored by `confluence`*.* As a result, the following example config will work the same as the previous one:

    ``` xml
    <plugin>
        <groupId>com.atlassian.maven.plugins</groupId>
        <artifactId>maven-amps-plugin</artifactId>
        <configuration>
            <applications>
                <application>
                    <applicationKey>jira-software</applicationKey>
                    <version>${jira.software.application.version}</version>
                </application>
            </applications>
            <products>
                <product>
                    <id>jira</id>
                    <instanceId>jira</instanceId>
                    <version>${jira.version}</version>
                </product>
                <product>
                     <id>confluence</id>
                     <instanceId>confluence</instanceId>
                     <version>${confluence.version}</version>
                </product>
            </products>
        </configuration>
    </plugin>
    ```

-   Applications can be added to products that have already been defined, by using a Maven profile. See the example below.  
    *Note, this only applies to the configuration level, not the product level. At the product level, you must repeat the entire `<products>` element.   
    *

    ``` xml
    <plugins>
        <plugin>
            <groupId>com.atlassian.maven.plugins</groupId>
            <artifactId>maven-amps-plugin</artifactId>
            <configuration>
                <products>
                    <product>
                        <id>jira</id>
                        <instanceId>jira</instanceId>
                        <version>${jira.version}</version>
                    </product>
                    <product>
                         <id>confluence</id>
                         <instanceId>confluence</instanceId>
                         <version>${confluence.version}</version>
                    </product>
                </products>
            </configuration>
        </plugin>
    </plugins>
    <profiles>
        <profile>
            <id>jira7</id>
            <plugins>
                <plugin>
                    <groupId>com.atlassian.maven.plugins</groupId>
                    <artifactId>maven-amps-plugin</artifactId>
                    <configuration>
                        <applications>
                                <application>
                                    <applicationKey>jira-software</applicationKey>
                                    <version>${jira.software.application.version}</version>
                                </application>
                            </applications>
                    </configuration>
                </plugin>
            </plugins>
        </profile>
    </profiles>
    ```









































































































































































































































































































































































































































































