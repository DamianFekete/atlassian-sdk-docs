---
title: Tips for Functional Tests with Selenium 2818377
aliases:
    - /server/framework/atlassian-sdk/tips-for-functional-tests-with-selenium-2818377.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818377
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818377
confluence_id: 2818377
platform:
product:
category:
subcategory:
---
# Documentation : Tips for Functional Tests with Selenium

With more and more UI being rendered and processed dynamically with JavaScript, in-browser testing has become a requirement for functional testing. Selenium is a popular choice for implementing tests that execute within the context of a browser but are still Java-driven. This page gives you tips for using Selenium to test your plugin.

## Add atlassian-selenium-browsers-auto to your pom.xml

Add this XML to the `<dependencies>` section in your pom.xml:

``` xml
<dependency>
   <groupId>com.atlassian.selenium</groupId>
   <artifactId>atlassian-selenium-browsers-auto</artifactId>
   <version>2.0.0.m3</version>
   <scope>test</scope>
</dependency>
```

You should verify the `<version>` value <a href="https://maven.atlassian.com/index.html#welcome" class="external-link">is the latest by searching</a> for the `<groupId>` in Atlassian's Maven repository. 

## Write a Selenium test

The Atlassian Plugin SDK comes with support for integration/functional tests that will run with the target Atlassian application started and your plugin installed. You just have to create one or more tests in the `src/test/java/it` directory. The convention is if your code is in the `com.mycompany.myplugin` package, your integration tests would be in the `it.com.mycompany.myplugin` package or `src/test/java/it/com/mycompany/myplugin` directory.

To use Selenium in these tests, the `atlassian-selenium-browsers-auto` artifact provides a few static helper methods. These methods, when used for the first time:

1.  Detect your operating system
2.  Install the appropriate browser (FireFox 3.5 is the default) for your OS in `target/seleniumTmp`
3.  If Linux and `xfvb.enable` is set to true, start `Xvfb` on an open DISPLAY detected automatically
4.  Start the Selenium server
5.  Start the newly installed browser

This all happens in the background, so you should just be able to focus on your test.

Here is a simple test that hits the home page and looks for the text of "Hello world":

``` java
import com.atlassian.selenium.SeleniumClient;
import static com.atlassian.selenium.browsers.AutoInstallClient.assertThat;
import static com.atlassian.selenium.browsers.AutoInstallClient.seleniumClient;
public class TestHelloWorld extends TestCase
{
    public void testHelloWorld() throws Exception
    {
        SeleniumClient client = seleniumClient();
        client.open("/");
        assertThat().textPresent("Hello world");
    }
}
```

## Specify a Browser

If you want to specify a browser other than Firefox 3.5, you can do so by specifying the `selenium.browser` system property in your atlassian-&lt;product&gt;-plugin configuration. For example:

``` javascript
<build>
  <plugins>
    <plugin>
      <groupId>com.atlassian.maven.plugins</groupId>
      <artifactId>maven-confluence-plugin</artifactId>
      <configuration>
        <systemPropertyVariables>
          <selenium.browser>firefox-3.6</selenium.browser> <!-- also available chrome-6 and chrome-7 -->
        </systemPropertyVariables>
      </configuration>
    </plugin>
  </plugins>
</build>
```

You can find out what strings are valid by looking at the `com.atlassian.browsers.BrowserVersion`.

##### RELATED TOPICS

[Writing and Running Plugin Tests](/server/framework/atlassian-sdk/writing-and-running-plugin-tests)





















































































































































































































































