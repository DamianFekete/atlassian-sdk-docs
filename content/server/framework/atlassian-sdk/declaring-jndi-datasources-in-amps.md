---
aliases:
- /server/framework/atlassian-sdk/declaring-jndi-datasources-in-amps-16974213.html
- /server/framework/atlassian-sdk/declaring-jndi-datasources-in-amps-16974213.md
category: devguide
confluence_id: 16974213
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16974213
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16974213
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/declaring-jndi-datasources-in-amps
new_url: /server/framework/atlassian-sdk/declaring-jndi-datasources-in-amps
platform: server
product: atlassian-sdk
subcategory: learning
title: Declaring JNDI datasources in AMPS
---
# Declaring JNDI datasources in AMPS

This page describes how to declare a datasource in AMPS.

## Introduction

JNDI Datasources are useful when:

-   A plugin needs to access another database than the default one,
-   You want the product to store its data in the database you specify: Postgres, MySQL, ...

The datasource support was introduced by <a href="https://ecosystem.atlassian.net/browse/AMPS-737" class="external-link">AMPS-737</a>.

## Support

|                    | Use the datasource through a plugin | Use the datasource for the product's data |
|--------------------|-------------------------------------|-------------------------------------------|
| Confluence         | Yes                                 | Yes                                       |
| JIRA using AMPS    | Yes                                 | No                                        |
| All other products | Yes                                 | N/A                                       |

 

You can go through the setup of Confluence and tell it to use the datasource you've just provided, such as jdbc/DefaultDS. For JIRA, it is a little more complicated: You need to declare the file dbconfig.xml.

## Example

You can checkout this example on BitBucket: <a href="https://bitbucket.org/aragot/amps-examples" class="external-link">Examples using JNDI datasources for JIRA and Confluence</a>.

### Declare the datasource in the pom.xml

In the following example, we declare the JNDI datasource jdbc/DefaultDS and make it target a local Postgres instance. 

``` javascript
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/maven-v4_0_0.xsd">
    <modelVersion>4.0.0</modelVersion>
    <groupId>com.atlassian</groupId>
    <artifactId>datasource-example</artifactId>
    <version>1.0-SNAPSHOT</version>
    <name>Datasource Example</name>
    <packaging>atlassian-plugin</packaging>
    <dependencies>
        <dependency>
            <groupId>com.atlassian.confluence</groupId>
            <artifactId>confluence</artifactId>
            <version>${confluence.version}</version>
            <scope>provided</scope>
        </dependency>
        <dependency>
            <groupId>postgresql</groupId>
            <artifactId>postgresql</artifactId>
            <version>9.1-901-1.jdbc4</version>
            <scope>runtime</scope>
        </dependency>
    </dependencies>
    <build>
        <plugins>
            <plugin>
                <!-- Run me with "mvn clean amps:run" -->
                <groupId>com.atlassian.maven.plugins</groupId>
                <artifactId>maven-amps-plugin</artifactId>
                <version>4.1</version>
                <extensions>true</extensions>
                <configuration>
                    <instanceId>instanceId1</instanceId>
                    <products>
                        <product>
                            <id>confluence</id>
                            <instanceId>instanceId1</instanceId>
                            <version>${confluence.version}</version>
                            <dataPath>src/main/resources/empty-home</dataPath>
                            <dataSources>
                                <dataSource>
                                  <jndi>jdbc/DefaultDS</jndi>
                                  <url>jdbc:postgresql://localhost:5432/confluence</url>
                                  <username>confluence</username>
                                  <password>confluence</password>
                                  <driver>org.postgresql.Driver</driver>
                                  <libArtifacts>
                                    <libArtifact>
                                      <groupId>postgresql</groupId>
                                      <artifactId>postgresql</artifactId>
                                      <version>9.1-901-1.jdbc4</version>
                                    </libArtifact>
                                  </libArtifacts>
                                </dataSource>
                            </dataSources>
                        </product>
                    </products>
                </configuration>
            </plugin>
        </plugins>
    </build>
    <properties>
        <confluence.version>5.0-m9</confluence.version>
    </properties>
</project>
```

Notice how we set the Data Path to an empty directory: If you start Confluence using an empty Home, the setup process will be displayed. During the setup process, you will have the opportunity to tell Confluence to store its data in the JNDI datasource java:comp/env/jdbc/DefaultDS.

### Start your product

Using the previous pom.xml, you can start the product using:

``` javascript
atlas-run
```

 

## Configuration

This feature relies on CodeHaus Cargo to launch Tomcat with the datasource. You can get more understanding of the properties by reading <a href="http://cargo.codehaus.org/Tomcat+6.x" class="external-link">Cargo Configuration for Tomcat 6.x</a> .

| Parameter          | Default Value                                 | Description                                                                      |
|--------------------|-----------------------------------------------|----------------------------------------------------------------------------------|
| jndi               | \-                                            | The JNDI string for application to lookup                                        |
| driver             | \-                                            | The class of the JDBC driver, such as "org.hsqldb.jdbcDriver"                    |
| url                | \-                                            | The JDBC url, such as jdbc:hsqldb:/path/to/database                              |
| username           | \-                                            | The username to connect to the database                                          |
| password           | \-                                            | The password to connect to the database                                          |
| type               | Will not be sent to Cargo if empty            | The type of driver, such as "java.sql.Driver" or "javax.sql.XSDataSource"        |
| transactionSupport | Will not be sent to Cargo if empty            | LOCAL\_TRANSACTION or XQ\_TRANSACTION                                            |
| properties         | Will not be sent to Cargo if empty            | Properties to pass to the driver. Semi-colon delimited string.                   |
| cargoString        | Will be built using the other values if empty | Instead of providing any other value, you can directly pass the string for Cargo |

## Known Issues

There is no user interface to tell JIRA to use the provided datasource to store its data. However, it is still possible to use AMPS to declare the datasource; You will just need to provide JIRA with the dbconfig.xml. Please open the BitBucket repository for an example: <a href="https://bitbucket.org/aragot/amps-examples" class="external-link">Examples using JNDI datasources for JIRA and Confluence</a>





























































































































































































