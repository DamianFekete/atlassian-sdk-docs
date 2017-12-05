---
aliases:
- /server/framework/atlassian-sdk/how-to-upgrade-ao-to-0.18.x-in-jira-5-8946978.html
- /server/framework/atlassian-sdk/how-to-upgrade-ao-to-0.18.x-in-jira-5-8946978.md
category: devguide
confluence_id: 8946978
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8946978
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8946978
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: How to Upgrade Ao to 0.18.X in JIRA 5 8946978
---
# How to upgrade AO to 0.18.x in JIRA 5

Prior to JIRA 5 RC3, in order to test the new version of AO you'll need to install it yourself. This is described in the procedure below, and is intended for testing only, not for use in production.

### Manually installing new AO version into older JIRA

Manually installing version 0.18.1 or above of ActiveObjects also requires manually upgrading the Activity Streams plugin. Since they each contain multiple components that must be upgraded together, they can't be upgraded through UPM.

#### AO and Streams jar files overview

ActiveObjects consists of two plugins and one library located in the WEB-INF/lib directory. Activity Streams consists of 8 plugins. In the lists below, $AO\_VERSION is the current ActiveObjects plugin version (0.18.1) and $STREAMS\_VERSION is the current Activity Streams version (5.1.m3).

Plugins to be installed into home/plugins/installed-plugins/: (note that these will override previous versions that are in home/plugins/.bundled-plugins):

-   activeobjects-plugin-$AO\_VERSION.jar
-   activeobjects-jira-spi-$AO\_VERSION.jar
-   streams-aggregator-plugin-$STREAMS\_VERSION.jar
-   streams-api-$STREAMS\_VERSION.jar
-   streams-core-plugin-$STREAMS\_VERSION.jar
-   streams-inline-actions-plugin-$STREAMS\_VERSION.jar
-   streams-jira-inline-actions-plugin-$STREAMS\_VERSION.jar
-   streams-jira-plugin-$STREAMS\_VERSION.jar
-   streams-spi-$STREAMS\_VERSION.jar
-   streams-thirdparty-plugin-$STREAMS\_VERSION.jar

Library to be installed into WEB-INF/lib/: (**note that the previous version in WEB-INF/lib/ must be deleted**)

-   activeobjects-spi-$AO\_VERSION.jar

#### Upgrading AO

All of the files need to be upgraded together before JIRA is restarted.

1.  Shut down JIRA
2.  Copy jar files in the first list above to home/plugins/installed-plugins/
3.  Delete jar file webapp/WEB-INF/lib/activeobjects-spi-\*.jar
4.  Copy activeobjects-spi-$AO\_VERSION.jar to webapp/WEB-INF/lib/
5.  Restart JIRA

#### If using AMPS

If you are launching JIRA along with your plugin via the Atlassian SDK, you can use the following configuration in your **pom.xml** to copy the appropriate jars into JIRA when it is launched. (Make sure to replace $AO\_VERSION and $STREAMS\_VERSION with the current version numbers.)

``` xml
<dependencies>
    <dependency>
        <groupId>com.atlassian.activeobjects</groupId>
        <artifactId>activeobjects-plugin</artifactId>
        <version>${ao.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.activeobjects</groupId>
        <artifactId>activeobjects-jira-spi</artifactId>
        <version>${ao.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.activeobjects</groupId>
        <artifactId>activeobjects-spi</artifactId>
        <version>${ao.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.streams</groupId>
        <artifactId>streams-aggregator-plugin</artifactId>
        <version>${streams.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.streams</groupId>
        <artifactId>streams-api</artifactId>
        <version>${streams.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.streams</groupId>
        <artifactId>streams-core-plugin</artifactId>
        <version>${streams.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.streams</groupId>
        <artifactId>streams-inline-actions-plugin</artifactId>
        <version>${streams.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.streams</groupId>
        <artifactId>streams-jira-inline-actions-plugin</artifactId>
        <version>${streams.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.streams</groupId>
        <artifactId>streams-jira-plugin</artifactId>
        <version>${streams.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.streams</groupId>
        <artifactId>streams-spi</artifactId>
        <version>${streams.version}</version>
        <scope>provided</scope>
    </dependency>
    <dependency>
        <groupId>com.atlassian.streams</groupId>
        <artifactId>streams-thirdparty-plugin</artifactId>
        <version>${streams.version}</version>
        <scope>provided</scope>
    </dependency>
</dependencies>

<build>
    <plugins>
        <plugin>
            <groupId>com.atlassian.maven.plugins</groupId>
            <artifactId>maven-jira-plugin</artifactId>
            <configuration>
                <libArtifacts>
                    <libArtifact>
                        <groupId>com.atlassian.activeobjects</groupId>
                        <artifactId>activeobjects-spi</artifactId>
                        <version>${ao.version}</version>
                    </libArtifact>
                </libArtifacts>
                <pluginArtifacts>
                    <pluginArtifact>
                        <groupId>com.atlassian.activeobjects</groupId>
                        <artifactId>activeobjects-plugin</artifactId>
                        <version>${ao.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.activeobjects</groupId>
                        <artifactId>activeobjects-jira-spi</artifactId>
                        <version>${ao.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.streams</groupId>
                        <artifactId>streams-aggregator-plugin</artifactId>
                        <version>${streams.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.streams</groupId>
                        <artifactId>streams-api</artifactId>
                        <version>${streams.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.streams</groupId>
                        <artifactId>streams-core-plugin</artifactId>
                        <version>${streams.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.streams</groupId>
                        <artifactId>streams-inline-actions-plugin</artifactId>
                        <version>${streams.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.streams</groupId>
                        <artifactId>streams-jira-inline-actions-plugin</artifactId>
                        <version>${streams.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.streams</groupId>
                        <artifactId>streams-jira-plugin</artifactId>
                        <version>${streams.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.streams</groupId>
                        <artifactId>streams-spi</artifactId>
                        <version>${streams.version}</version>
                    </pluginArtifact>
                    <pluginArtifact>
                        <groupId>com.atlassian.streams</groupId>
                        <artifactId>streams-thirdparty-plugin</artifactId>
                        <version>${streams.version}</version>
                    </pluginArtifact>
                </pluginArtifacts>
            </configuration>
        </plugin>
    </plugins>
</build>

<properties>
    <ao.version>$AO_VERSION</ao.version>
    <streams.version>$STREAMS_VERSION</streams.version>
</properties>
```






































































































































































































































































