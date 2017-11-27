---
title: Speeding Up Confluence Plugin Development Using Maven Cli 2818680
aliases:
    - /server/framework/atlassian-sdk/speeding-up-confluence-plugin-development-using-maven-cli-2818680.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818680
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818680
confluence_id: 2818680
platform:
product:
category:
subcategory:
---
# Documentation : Speeding Up Confluence Plugin Development Using Maven CLI

{{% warning %}}

These instructions are obsolete if you are using the <a href="/pages/createpage.action?spaceKey=DOCS&amp;title=Atlassian+Plugin+SDK&amp;linkCreation=true&amp;fromPageId=2818680" class="createlink">Atlassian Plugin SDK</a> (and you should be). Leaving here only as reference for those using very old versions of Confluence.

{{% /warning %}}

As everyone knows, running <a href="http://maven.apache.org/" class="external-link">Maven</a> can be pretty slow, which means deploying your plugin using the <a href="http://confluence.atlassian.com/display/DEVNET/Atlassian+Maven+PDK" class="external-link">Atlassian Maven PDK</a> takes quite a while. So I tried to find a way for faster turnaround times in Confluence plugin development. By using a combination of <a href="http://www.jroller.com/mrdon/" class="external-link">Don Brown's</a> excellent <a href="http://github.com/mrdon/maven-cli-plugin/wikis" class="external-link">CLI Plugin</a> and the [Atlassian Maven PDK](/server/framework/atlassian-sdk/obsolete-atlassian-maven-pdk-2818711.html), my deployment time for a changed plugin is down to -- TADA -- **1 to 2 seconds**.

## Setting Up a New Plugin Project

Here are the instructions to set up a new plugin project from scratch:

1.  Create a new Maven project using the [plugin archetypes](/server/framework/atlassian-sdk/atlassian-plugin-archetypes-2818678.html#confluence). You need to replace `$MY_PACKAGE` with your package name (e.g. `com.example.confluence`) and `$MY_PLUGIN` with your artifact ID (e.g. `fast-confluence-plugin`). More detailed instructions are available <a href="#here" class="unresolved">here</a>.
2.  Update your `~/.m2/settings.xml` (see [Example settings.xml](/server/framework/atlassian-sdk/example-settings.xml-2818713.html)) to include the following plugin repository for the CLI plugin:
    ``` javascript
    <pluginRepository>
        <id>cli</id>
        <url>http://twdata-m2-repository.googlecode.com/svn/</url>
        <snapshots>
            <enabled>false</enabled>
        </snapshots>
        <releases>
            <enabled>true</enabled>
        </releases>
    </pluginRepository>
    ```

    This will allow the plugin to be installed automatically when it is used for the first time.
3.  Make sure that you have specified the location of **your** Confluence instance in your settings.xml when configuring the [PDK](/server/framework/atlassian-sdk/obsolete-atlassian-maven-pdk-2818711.html):
    ``` javascript
    <atlassian.pdk.server.url>http://localhost:1990/confluence</atlassian.pdk.server.url>
    ```

4.  Add the following to your project's `pom.xml` as a child of the `<project>` element:
    ``` javascript
    <build>
        <plugins>
            <plugin>
                <groupId>org.twdata.maven</groupId>
                <artifactId>maven-cli-plugin</artifactId>
                <configuration>
                    <commands>
                        <pi>clean resources compile jar com.atlassian.maven.plugins:atlassian-pdk:install</pi>
                        <pu>com.atlassian.maven.plugins:atlassian-pdk:uninstall</pu>
                    </commands>
                </configuration>
            </plugin>
        </plugins>
    </build>
    ```

    This will define the two commands pi (plugin install) and pu (plugin uninstall). Of course you can adjust the commands to your needs or add more customs commands.
5.  Now start up your Confluence development instance.
6.  Run `mvn cli:execute` and type `pi` at the `maven2>` command prompt.

After the first run, which takes about 2 seconds, all subsequent runs take about 1 second on my machine. And because the CLI plugin supports command history, running it again is as easy as switching to your terminal, doing &lt;Arrow Up&gt;+&lt;Enter&gt;, switching to your browser and reloading your page.

The above procedure is very reliable and is as close to the usual plugin runtime environment as possible.

















































































































































































































































































































