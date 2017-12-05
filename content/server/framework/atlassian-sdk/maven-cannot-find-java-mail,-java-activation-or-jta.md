---
aliases:
- /server/framework/atlassian-sdk/2818709.html
- /server/framework/atlassian-sdk/2818709.md
category: devguide
confluence_id: 2818709
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818709
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818709
platform: server
product: atlassian-sdk
subcategory: faq
title: 2818709
---
# Maven cannot find Java Mail, Java Activation or JTA

When you run the shell scripts in the Atlassian Plugin SDK, Maven may complain that it cannot find **Java Mail**, **Java Activation** or **JTA**.

For example, for the Java Activation, Maven will give this error:

> Embedded error: Missing: javax.activation:activation:jar:1.0.2

## Background to this Problem

Sun will not allow Maven to redistribute its binaries. Instead, all users must install Sun binaries manually by downloading them from Sun's website and running the `atlas-mvn install` command. You'll find instructions in the Maven documentation <a href="http://maven.apache.org/guides/mini/guide-coping-with-sun-jars.html" class="external-link">here</a> and <a href="http://maven.apache.org/guides/mini/guide-3rd-party-jars-local.html" class="external-link">here</a>.

## Installing the Sun Binaries

You will find the Sun binaries in these locations:

-   <a href="http://java.sun.com/products/javamail/downloads/index.html" class="external-link">JavaMail</a>
-   <a href="http://java.sun.com/products/jta/" class="external-link">JTA</a>
-   <a href="http://java.sun.com/products/javabeans/glasgow/jaf.html" class="external-link">Java Activation</a>

The Maven install command looks like this:

``` bash
atlas-mvn install:install-file -DgroupId=javax.XXXXX -DartifactId=XXXXX \
  -Dversion=X.X.X -Dpackaging=jar -Dfile=/path/to/XXXX-X_X_X.jar
```

{{% note %}}

Issue with Atlassian Plugin SDK

A known issue with the Atlassian Plugin SDK is causing problems with maven parameters. You may need to run the above command directly from your maven directory. Please see <a href="https://studio.atlassian.com/browse/AMPS-197" class="external-link">AMPS-197</a> for more information.

{{% /note %}}

Below, as an example of the detailed installation process, we give specific instructions on installing the JavaBeans Activation Framework (JAF).

## Installing the JavaBeans Activation Framework (JAF)

1.  Download <a href="http://java.sun.com/javase/technologies/desktop/javabeans/glasgow/jaf.html" class="external-link">JAF</a>.
2.  Unzip the downloaded file.
3.  Go to the folder which contains the `activation.jar` file that you have just unzipped.
4.  Install JAF using the following command:

    ``` javascript
    atlas-mvn install:install-file -DgroupId=javax.activation -DartifactId=activation -Dversion=1.0.2 -Dpackaging=jar -Dfile=activation.jar
    ```

      
    {{% note %}}

    Issue with Atlassian Plugin SDK

A known issue with the Atlassian Plugin SDK is causing problems with maven parameters. You may need to run the above command directly from your maven directory. Please see <a href="https://studio.atlassian.com/browse/AMPS-197" class="external-link">AMPS-197</a> for more information.

    {{% /note %}}





























































































