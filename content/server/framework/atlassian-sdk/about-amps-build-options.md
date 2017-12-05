---
aliases:
- /server/framework/atlassian-sdk/about-amps-build-options-16974627.html
- /server/framework/atlassian-sdk/about-amps-build-options-16974627.md
category: devguide
confluence_id: 16974627
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16974627
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16974627
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: About Amps Build Options 16974627
---
# About AMPS build options

When you create a new plugin project with the SDK, the generated POM file specifies the Atlassian Maven Plugin Suite (AMPS) as a build plugin for the project.

If using the SDK, you do not need to install AMPS or configure your project to use it yourself. However, there are a number of settings you can use to control its behavior.

You can pass AMPS parameters to Maven in one of two ways:

-   On the command line as Java system variables. For example:

    ``` bash
    mvn jira:run -D<parameter1Name>=<parameter1Value> -D<parameter2Name>=<parameter2Value> ...
    ```

-   In the POM, by using the configuration element in the AMPS declaration:  
      

    ``` xml
    <project>
      ...
      <build>
        <plugins>
          <plugin>
            <groupId>com.atlassian.maven.plugins</groupId>
            <artifactId>maven-jira-plugin</artifactId>
            <version>3.2.3</version>
            <extensions>true</extensions>
            <configuration>
                <!-- parameter key/value pairs go here -->
                <parameter1Name>parameter1Value</parameter1Name>
            </configuration>
          </plugin>
        </plugins>
      </build>
      ...
    </project>
    ```

{{% note %}}

Values specified on the command line override values in the POM.

{{% /note %}}

For details on AMPS configuration settings, see:

-   [AMPS Build Configuration Reference](/server/framework/atlassian-sdk/amps-build-configuration-reference)


















































































































































