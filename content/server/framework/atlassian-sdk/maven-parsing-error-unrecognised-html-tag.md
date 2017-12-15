---
aliases:
- /server/framework/atlassian-sdk/maven-parsing-error-unrecognised-html-tag-2818368.html
- /server/framework/atlassian-sdk/maven-parsing-error-unrecognised-html-tag-2818368.md
category: devguide
confluence_id: 2818368
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818368
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818368
date: '2017-12-08'
legacy_title: Maven Parsing Error Unrecognised HTML Tag
platform: server
product: atlassian-sdk
subcategory: faq
title: Maven parsing error unrecognised HTML tag
---
# Maven parsing error unrecognised HTML tag

You may receive a Maven error: "Parsing error.... Unrecognized tag: 'html'"

Occasionally, our Maven proxy will return a 404 file instead of the POM that it should. We are investigating this error (XPR-259) with the Archiva developers. In the mean time, should this happen to you, you should try remove the artifact and its POM from your local repository to force a re-download. If that does not work, contact [our developer relations team](https://developer.atlassian.com/help#contact-us) and we will correct the problem at the source.
