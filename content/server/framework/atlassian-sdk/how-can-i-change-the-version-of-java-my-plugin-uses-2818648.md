---
title: How Can I Change the Version Of Java My Plugin Uses 2818648
aliases:
    - /server/framework/atlassian-sdk/how-can-i-change-the-version-of-java-my-plugin-uses-2818648.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818648
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818648
confluence_id: 2818648
platform:
product:
category:
subcategory:
---
# How can I change the version of Java my plugin uses

#### How do I specify the default Java version?

By default, Maven uses the JDK that you run it with to compile your sources. To change the default version of Java that is selected on your machine, please see the specific instructions for your platform. Check with `java -version` from a command line prompt.

Windows - use the <a href="http://download.oracle.com/javase/1.5.0/docs/guide/deployment/deployment-guide/jcp.html" class="external-link">Java Control Panel</a>  
Linux - use the `alternatives` command. More information can be found <a href="http://lanestechblog.blogspot.com/2008/03/using-alternatives-in-linux-to-use.html" class="external-link">here</a>  
OSX - run Applications, Utilities, Java Preferences. Making changes to soft links by hand is error prone and can produce cryptic errors.

#### How do I specify a particular version of Java for my plugin?

If you would like to enforce a particular JDK version or version range, add these parameters to your plugin's POM file.

``` xml
<project>
    <build>
        <plugins>
        <plugin>
        <groupId>org.apache.maven.plugins</groupId>
        <artifactId>maven-enforcer-plugin</artifactId>
        <executions>
            <execution>
            <id>enforce-java</id>
            <goals>
              <goal>enforce</goal>
            </goals>
            <configuration>
              <rules>
                <requireJavaVersion>
                <version>[1.4,1.5)</version>
                </requireJavaVersion>
              </rules>
            </configuration>
            </execution>
              </executions>
            </plugin>
        </plugins>
    </build>
</project>
```

Plugins are pre-configured to use Java 1.5 as the source level when compiling. If you would like to use a different source level, you'll need to set the `jdkLevel` property:

``` xml
<project>
  ...
  <properties>
    ...
    <jdkLevel>1.4</jdkLevel>
  </properties>
  ...
</project>
```

This property is also used by the Maven IDEA plugin to set the source level for the project generated when you run `mvn idea:idea`.





















































































































































































































































