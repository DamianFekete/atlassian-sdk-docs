---
aliases:
- /server/framework/atlassian-sdk/using-jdom-in-osgi-851991.html
- /server/framework/atlassian-sdk/using-jdom-in-osgi-851991.md
category: devguide
confluence_id: 851991
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851991
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851991
date: '2017-12-08'
legacy_title: Using JDOM in OSGi
platform: server
product: atlassian-sdk
subcategory: faq
title: Using JDOM in OSGi
---
# Using JDOM in OSGi

<a href="http://www.jdom.org/" class="external-link">JDOM</a> is a difficult package to use in <a href="http://www.osgi.org/" class="external-link">OSGi</a>, for the following reasons:

### JDOM has Classes in the Root Package

For some reason, the author of JDOM decided to break one of the fundamental rules of Java, that is, do not put classes in the root package. JDOM has a class called `JDOMAuthor` in the root package. If you want to include JDOM in your OSGi bundle, you'll need to remove these classes. In Maven, you can do it like this:

``` xml
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-dependency-plugin</artifactId>
    <executions>
        ...
        <execution>
            <id>unpack-jdom</id>
            <phase>compile</phase>
            <goals>
                <goal>unpack</goal>
            </goals>
            <configuration>
                <artifactItems>
                    <artifactItem>
                        <groupId>jdom</groupId>
                        <artifactId>jdom</artifactId>
                        <version>1.0</version>
                        <outputDirectory>
                            ${project.build.directory}/jdom
                        </outputDirectory>
                    </artifactItem>
                </artifactItems>
            </configuration>
        </execution>
        ...
    </executions>
</plugin>
...
<plugin>
    <groupId>org.apache.maven.plugins</groupId>
    <artifactId>maven-antrun-plugin</artifactId>
    <executions>
        ...
        <execution>
            <!-- Remove classes from the root package and re jar -->
            <id>fix-jdom</id>
            <phase>process-classes</phase>
            <goals>
                <goal>run</goal>
            </goals>
            <configuration>
                <tasks>
                    <delete>
                        <fileset dir="${project.build.directory}/jdom" includes="*.class"/>
                    </delete>
                    <jar destfile="${project.build.directory}/jdom-1.0-fixed.jar">
                        <fileset dir="${project.build.directory}/jdom"/>
                    </jar>
                </tasks>
            </configuration>
        </execution>
        ...
    </executions>
</plugin>
```

Additionally, if using the Maven Bundle Plugin, you will need to manually include this library, for example:

``` xml
<Bundle-ClassPath>.,{maven-dependencies},jdom-1.0-fixed.jar</Bundle-ClassPath>
<Include-Resource>{maven-resources},{maven-dependencies},${project.build.directory}/jdom-1.0-fixed.jar</Include-Resource>
```

Make sure JDOM is not included in your bundled Maven dependencies. You can usually do this by marking JDOM as 'provided'.

### JDOM Imports a Number of Optional Packages

'Optional' is the default setting for imports, if you do not include an OSGi manifest. But if you are using the Maven Bundle Plugin, the default is 'mandatory'.

Note that if you are not marking all packages as optional imports by default, then you will need to add at least the following to your imports:

``` xml
oracle*;resolution:=optional,org.jaxen*;resolution:=optional
```

##### RELATED TOPICS

[Marking Packages as Optional Imports](/server/framework/atlassian-sdk/marking-packages-as-optional-imports)
