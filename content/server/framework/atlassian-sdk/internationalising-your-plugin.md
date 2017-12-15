---
aliases:
- /server/framework/atlassian-sdk/internationalising-your-plugin-8946312.html
- /server/framework/atlassian-sdk/internationalising-your-plugin-8946312.md
category: devguide
confluence_id: 8946312
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8946312
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8946312
date: '2017-12-08'
guides: guides
legacy_title: Internationalising your plugin
platform: server
product: atlassian-sdk
subcategory: learning
title: Internationalising your plugin
---
# Internationalising your plugin

This document is a guide for developers wanting to provide internationalisation support for their plugins. This means that other people will be able to provide translated strings for the labels and messages in your plugin without you having to recompile your plugin, thereby simplifying the process of localisation.

## How Does Internationalisation Work?

Before you implement internationalisation (also called 'i18n' because there are 18 letters between 'i' and 'n') support for your plugin, it is important to understand how a plugin is internationalised.

First, all messages in the plugin must be moved outside the code into a properties file in the plugin. The properties file stores the default (English) translations for all messages inside the plugin. The properties file format is a key = value format, where the key is used to refer to the resource in the code and the value is the default message in English:

``` text
com.example.plugin.fruit.basket.label = Your Fruit Basket
com.example.plugin.fruit.apple = Apple
com.example.plugin.fruit.banana = Banana
com.example.plugin.fruit.pear = Pear
com.example.plugin.fruit.basket.add.button = Add Fruit
```

All i18n keys in the properties file:

-   Must include a prefix which is unique to your plugin. We suggest using your plugin key (which would be `com.example.plugin.fruit` in the example above).  
    The remainder of the key (for example, `basket.label` or `apple`) should define the message.
-   Must be unique.

Once you have your messages defined in a properties file, you need to use the relevant i18n APIs in the Atlassian product to replace hard-coded English strings with references to your properties file. The sections below describe how to do that.

## Translating an Existing Plugin

If your has already been internationalised, follow these steps to translate the plugin:

1.  Extract the contents of the plugin JAR file.
2.  Locate the properties file which contains i18n key-value pairs.
3.  Create a copy of this file with the same file name and desired locale extension. For example, if the default properties file is called `mypluginprops.properties`, make a copy of this file and rename it to `MyPluginName_ll_CC.properties`, where '`_ll_CC`' is the locale extension for your required language and country.
4.  In your copied properties file, replace the default string values (not the keys) with your translated strings as desired.
5.  When you rebundle your plugin into a JAR file, ensure that your translated file is copied to the same location from where you obtained the original properties file. For example, if the original properties file was in `path/to/`, your copied and translated properties file needs to be in the same location.

**What should you use for a locale extension?**

A locale is composed of a language code and optionally a country code (as described in <a href="http://java.sun.com/javase/6/docs/technotes/guides/intl/locale.doc.html" class="external-link">this Java document</a>), as follows:

`<language-code><COUNTRY-CODE>`

For example, the properties file `mypluginprops_fr_CH.properties` has a language code of '**fr**' (French) and country code of '**CH**' (Switzerland). Be aware that the language code is lower case and the country code is upper case (capital letters). Refer to the list of <a href="http://en.wikipedia.org/wiki/List_of_ISO_639-1_codes" class="external-link">language codes (ISO-639)</a> and <a href="http://www.iso.org/iso/english_country_names_and_code_elements" class="external-link">country codes (ISO-3166)</a> for more information.

A properties file with no locale extension is the *default* properties file and should be English.

## How Do I Internationalise My Plugin?

This section provides instructions on how to internationalise your plugin from scratch.

To internationalise your plugin, please follow these steps, described in more detail below:

1.  Add internationalisation properties to your plugin
2.  Internationalise your plugin descriptor file
3.  Internationalise your plugin classes
4.  Internationalise your Velocity templates

#### 1. Add internationalisation properties to your plugin

##### Create a properties files for all messages in your plugin

As mentioned above, a properties file contains translatable strings for your plugin in key-value pairs.

``` text
com.example.plugin.fruit.basket.label = Your Fruit Basket
com.example.plugin.fruit.apple = Apple
com.example.plugin.fruit.banana = Banana
com.example.plugin.fruit.pear = Pear
com.example.plugin.fruit.basket.add.button = Add Fruit
```

1.  You will need to create a default English properties files for your plugin in the following location:

    ``` bash
    src/main/resources/com/example/mypluginname/mypluginprops.properties
    ```

2.  If you can translate your plugin into another language, you should write your translated message strings in a own separate file for that language, and name the file with the correct locale extension. For example, to provide a German translation you would also provide:

    ``` bash
    src/main/resources/com/example/mypluginname/mypluginprops_de_DE.properties
    ```

    Create a separate properties file for each language you need. For the moment, your properties files will be empty. In the following steps we will demonstrate how language-specific messages in your plugin can be moved from your plugin into the properties file.

**Please Note:** If you any of your translations use non-ASCII characters, which will include most languages other than English, then you must convert your text file to a Unicode-encoded ASCII text file using a tool such as **native2ascii**. Please refer to the <a href="http://java.sun.com/javase/technologies/core/basic/intl/faq.jsp" class="external-link">Java Internationalization FAQ</a> for more information.

##### Define your properties file as a new i18n resource

To register the new i18n properties file with the system, you will need to add a resource of type 'i18n' at the top level of your plugin descriptor, `atlassian-plugin.xml`.

``` xml
<atlassian-plugin>
    ...
    <resource type="i18n" name="mypluginprops" location="com.example.mypluginname"/>
    ...
</atlassian-plugin>
```

The attributes on the resource element have the following meaning for i18n resources:

-   type: must always be 'i18n'.
-   name: must be unique and match the 'base' name of your plugin properties file (that is, without the locale extension and .properties file name extension).
-   location: the path to your properties file under the `src/main/resources` directory in your plugin which (based on the example above), would be `src/main/resources/com/example/mypluginname`.

**Please Note:**

-   It is good practice to ensure that all properties files for a specific plugin are located in a single directory that is unique to that Atlassian product and all its (other) plugins. For example, `com/example/mypluginname/` shown in the example above.
-   If you are developing a plugin for a version of Confluence earlier than 3.1, then you must ensure that the properties files your plugin has a unique directory path due to <a href="http://jira.atlassian.com/browse/CONF-9580" class="external-link">CONF-9580</a>.

#### 2. Internationalise your Plugin Descriptor File

If you have plugin modules that contain explicitly-defined text strings, they can be replaced with translated strings from your properties file.

For example, if you have a web-item plugin module with a explicitly-defined label in English:

``` xml
<atlassian-plugin>
...
    <web-item>
        <label>Add Fruit</label>
        <link>/pages/addfruittobasket.action?pageId=$page.id</link>
    </web-item>
...
</atlassian-plugin>
```

You can move the contents of that label to the properties file by using the key attribute on the label element.

``` xml
<atlassian-plugin>
...
    <web-item>
        <label key="com.example.plugin.fruit.basket.add.button"/>
        <link>/pages/addfruittobasket.action?pageId=$page.id</link>
    </web-item>

    <resource type="i18n" name="i18n" location="com.example.mypluginname.MyPluginName"/>
...
</atlassian-plugin>
```

The exact attribute name for this process may vary based on the type of module in your `atlassian-plugin.xml` file. For example, the [Confluence Component Module](https://developer.atlassian.com/display/CONFDEV/Component+Module) requires the attribute `i18n-name-key` for its localisation key. You should consult the relevant documentation for the module you wish to localise. A good starting place is the [Plugin Module Types](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Plugin+Module+Types) documentation.

For a list of plugin modules specific to:

-   Confluence - refer to [Confluence Developer Documentation](https://developer.atlassian.com/display/CONFDEV/Confluence+Plugin+Module+Types)
-   JIRA - refer to [JIRA Plugin Guide](https://developer.atlassian.com/display/JIRADEV/About+JIRA+Plugin+Development)

In your properties file, `src/main/resources/com/example/mypluginname/MyPluginName.properties`, add the property key with the value in English:

``` text
com.example.plugin.fruit.basket.add.button = Add Fruit
```

Do the same for your other language properties files.

#### 3. Internationalise your Plugin Classes

If you would like to retrieve the value of a properties file key for use in a class, follow the instructions below.

##### Confluence

Within an [action class](https://developer.atlassian.com/display/CONFDEV/XWork-WebWork+Module), which should be a subclass of ConfluenceActionSupport, you can retrieve a string from a properties file by calling the getText() method.

For example, if your i18n properties file has the `com.example.plugin.fruit.basket.add.button` property defined, you can use the value of the property by calling the following method:

``` javascript
getText("com.example.plugin.fruit.basket.add.button")
```

This will return the string, "Add Fruit", assuming the same properties file as above.

If your property value includes <a href="http://docs.oracle.com/javase/tutorial/i18n/format/messageFormat.html" class="external-link">MessageFormat-style parameters</a>, you can pass these as an array to the call to getText().

**In MyPluginName.properties:**

``` java
com.example.plugin.fruit.basket.contains = Your fruit basket contains {0} item(s)
```

**In an action class:**

``` java
List<String> fruits = Arrays.asList("apple", "banana", "apricot");
return getText("com.example.plugin.fruit.basket.contains", new String[]{ String.valueOf(fruits.size()) });
```

This will return the string, "Your fruit basket contains 3 item(s)" in this example.

***Tip:*** You should never write i18n strings that depend on the cardinality of the values passed to it - for instance, "com.example.plugin.fruit.basket.contains.one" or "com.example.plugin.fruit.basket.contains.multiple" - as not all languages have the same pluralisation rules as English. See [Pluralising internationalisation strings](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Pluralising+internationalisation+strings) to find out more on how to write i18n strings that account for plurals.

If you need to create an internationalised message for the user outside an action class, you can use the SAL I18nResolver object. It can be dependency-injected into your macro or component class through the setter or constructor:

``` java
public class AddFruitMacro extends BaseMacro {

    private final I18nResolver i18n;

    public void setI18nResolver(I18nResolver i18n) {
        this.i18n = i18n;
    }

    public String execute(Map params, String body, RenderContext context) {
        return "<button>" + i18n.getText("com.example.plugin.fruit.basket.add.button") + "</button>";
    }
}
```

In order to use I18nResolver (or any other SAL class), you will need to bring it into your plugin with a `<component-import>` like this:

``` xml
<component-import key="i18nResolver" interface="com.atlassian.sal.api.message.I18nResolver"/>
```

***Tip:*** Ensure that you use the appropriate services for dealing with date formatting (userAccessor.getConfluenceUserPreferences(user).getDateFormatter(formatSettingsManager) so that the time zones are respected.

#### 4. Internationalise your Velocity Templates

If your plugin contains English text in <a href="http://velocity.apache.org/" class="external-link">Velocity</a> templates, it is relatively easy to internationalise that content as well.

To render an internationalised message in Velocity templates, use $i18n.getText(), optionally with an array of parameter values. Here is a snippet of HTML with some examples:

``` xml
<p>
    $i18n.getText("com.example.plugin.fruit.basket.contains", [$fruits.size()])
</p>
<button>
    $i18n.getText("com.example.plugin.fruit.basket.add.button")
</button>
```

For details about the objects that are accessible from Velocity, please refer to:

-   [Our Confluence documentation](https://developer.atlassian.com/display/CONFDEV/Confluence+Objects+Accessible+From+Velocity) for Confluence objects available from Velocity.
-   [Our JIRA documentation](https://developer.atlassian.com/display/JIRADEV/Contents+of+the+Velocity+Context) for JIRA objects available from Velocity.

## Internationalisation Testing

The <a href="http://developers.sun.com/solaris/articles/i18n/I18N_Testing.html" class="external-link">Sun I18N Testing Guidelines and Techniques</a> contains information on internationalisation testing.

The <a href="http://mojo.codehaus.org/l10n-maven-plugin/" class="external-link">Maven 2 Localization Tools plugin</a> can also help you test i18n/l10n. It can report on missing keys, extra keys, messages that are same between locales, and more, and it has the ability to create pseudo-localised properties for testing. You can add it to your `pom.xml` like this:

``` xml
<project>
  ...
  <build>
    ...
  </build>
  ...
  <reporting>
    <plugins>
      <plugin>
        <groupId>org.codehaus.mojo</groupId>
        <artifactId>l10n-maven-plugin</artifactId>
        <version>1.0-SNAPSHOT</version>
        <configuration>
          <locales>
            <locale>de</locale>
            <locale>es</locale>
            <locale>fr</locale>
            ...
          </locales>
        </configuration>
      </plugin>
    </plugins>
  </reporting>
  ...
  <pluginRepositories>
    <pluginRepository>
      <id>codehaus.org</id>
      <name>CodeHaus Plugin Snapshots</name>
      <url></url>
      <releases>
        <enabled>false</enabled>
      </releases>
      <snapshots>
        <enabled>true</enabled>
      </snapshots>
    </pluginRepository>
  </pluginRepositories>
</project>
```

## Known i18n Issues

-   <a href="http://jira.atlassian.com/browse/CONF-9281" class="external-link">CONF-9281</a> - There seems to be an issue while using Confluence clustering with i18n properties. This problem goes away by restarting the node.
-   <a href="http://jira.atlassian.com/browse/CONF-9580" class="external-link">CONF-9580</a> - All plugins share the same i18n resources as well as other resources. If you don't choose something unique to your plugin you will almost certainly collide with another plugin.

## Related Topics

-   **(JIRA only)** If you want to develop a language pack to run JIRA in another language, please see <a href="http://confluence.atlassian.com/display/JIRA/Translating+JIRA" class="external-link">Translating JIRA</a>.
-   **(Confluence only)** If you want to develop a language pack to run Confluence in another language, please see [Language Module](https://developer.atlassian.com/display/CONFDEV/Language+Module).
-   **(Confluence only)** If you want to translate the text for the plugins bundled with Confluence, please see [Internationalising Confluence Plugins](https://developer.atlassian.com/display/CONFDEV/Internationalising+Confluence+Plugins).
-   **(Confluence only)** If you want to translate the properties in the `ConfluenceActionSupport_<locale>.properties` file, please see [Translating ConfluenceActionSupport Content](https://developer.atlassian.com/display/CONFDEV/Translating+ConfluenceActionSupport+Content)

## Additional Resources

-   <a href="http://rscbundlecheck.sourceforge.net/" class="uri external-link">rscbundlecheck.sourceforge.net/</a>
