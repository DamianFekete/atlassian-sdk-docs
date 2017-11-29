---
title: Pluralising Internationalisation Strings 10421452
aliases:
    - /server/framework/atlassian-sdk/pluralising-internationalisation-strings-10421452.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=10421452
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=10421452
confluence_id: 10421452
platform:
product:
category:
subcategory:
---
# Pluralising internationalisation strings

During the development of your plugin, you will sometimes find the need to create messages which contain a full sentence that needs to be constructed differently in order to handle plural / singular forms.

For example:

``` text
"There were no matching files"
"There was 1 matching file"
"There were 2 matching files"
... 
```

As you can see, in English, there are three different ways to construct the message depending on the number of files in question.

This type of message can be catered for using the following strategies in preference order:

### Simplify the Message into a Plural-Independent Phrase

{{% tip %}}

Avoid creating messages which contain full sentences combined with the use of variables

{{% /tip %}}

This type of constructions should be avoided, because the message will then have to be written in such a way that it can cater to the syntax and pluralisation rules of every language out there, this in turn produces message strings that are complex and hard to understand for both developers and translators.

As an alternative, the previous message could simplified to the following form:

``` text
"Matching Files: {0}", where {0} is a place holder for the number of files in question.
```

The problem is solved by transforming the form of the sentence into a single phrase that does not need to change according to the pluralisation rules of the target language.

Whilst not perfect, this approach results in a message that is simple and comprehensible to both developers and translators and thus, it is the recommended default strategy to handle plural forms in your plugin's messages.

### Create a formatted string to cater for all plural forms using ChoiceFormat

However, there might be cases where transforming the message is not possible. If this is the case, then it's necessary to create the message as a <a href="http://docs.oracle.com/javase/7/docs/api/java/text/ChoiceFormat.html" class="external-link">ChoiceFormat</a> string.

In this case, a `ChoiceFormat` message allows us to attach a format to a range of numbers, thus allowing us to express the different variations of the message according to the passed in numeric value.

#### An example

``` text
"1 user has mentioned you on this issue"
```

We want to write our internationalisation string such that:

-   When we pass in the value '0', the translated string reads "No users have mentioned you on this issue".
-   When we pass in the value '1', the translated string reads "1 user has mentioned you on this issue"
-   When we pass a value 'X' that is greater than 1, the translated string reads "X users have mentioned you on this issue"

To accomplish this, we would write our internationalisation string as follows:

``` java
com.example.plugin.mentions = {0,choice, 0#No users have| 1#A user has| 1<{0,number} users have} mentioned you on this issue.
```

{{% note %}}

Ranges of Values In Languages Different Than English

It is worth mentioning that the number of ranges to be catered for will be different depending on the target language.

For example, according to the <a href="http://www.unicode.org/cldr/charts/supplemental/language_plural_rules.html#cy" class="external-link">CLDR Plural Rules Data</a>, it is possible in the Welsh language to have these ranges:

n is 0;  
n is 1;  
n is 2;  
n is 3;  
n is 6;  
*everything else*

Consequently, ranges will have to be defined for each in the ChoiceFormat message Welsh message and the message will have to be constructed to cater for each of them.

{{% /note %}}

#### Range Evaluation

When you write these choice format strings, you are defining **ranges** that values will be evaluated against. Sometimes, the values passed will not have exact matches in the choices, so the translation chosen for your value will be the **best fit**. The choices are evaluated in ascending order - that is, from the left-most option to the right-most.

For instance, if we passed a negative number - say, -1 - in to the string:

``` java
com.example.plugin.matches = {0} {0,choice, 0#matching things| 1#match| 1<matches}
```

Our translated string would read "-1 matching things", because -1 is smaller than the first range we provided.

{{% warning %}}

As seen in the examples, `ChoiceFormat` strings are complex, and the rules for their construction and evaluation are particular.

Additionally, translators have to be familiar with the intricacies of how to express ranges in the ChoiceFormat to cater for the different ranges required in the language they are targeting in order to preserve correct grammar for all plural forms in that language.

Therefore, it is only recommended to use `ChoiceFormat` in cases where the sentence can not be simplified into a simple plural form independent phrase.

{{% /warning %}}

## Additional Resources

-   <a href="http://stuartgunter.wordpress.com/2011/08/09/java-i18n-pluralisation-using-choiceformat/" class="external-link">Java i18n Pluralisation using ChoiceFormat</a>
-   <a href="http://docs.oracle.com/javase/tutorial/i18n/format/choiceFormat.html" class="external-link">Handling Plurals (The Java™ Tutorials)</a>
-   <a href="http://docs.oracle.com/javase/7/docs/api/java/text/ChoiceFormat.html" class="external-link">ChoiceFormat (Java Platform SE 7)</a>

























