---
aliases:
- /server/framework/atlassian-sdk/maven-warning-pom-for-x-is-invalid-2818357.html
- /server/framework/atlassian-sdk/maven-warning-pom-for-x-is-invalid-2818357.md
category: devguide
confluence_id: 2818357
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818357
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818357
date: '2017-12-08'
legacy_title: Maven Warning POM for X is Invalid
platform: server
product: atlassian-sdk
subcategory: faq
title: Maven warning POM for X is invalid
---
# Maven warning POM for X is invalid

You may see a Maven warning "\[WARN\] POM for 'X' is invalid.... Reason: Not a v4.0.0 POM"

The warning just means that this particular library has not been upgraded to have a Maven 2 POM yet. It will still work fine in your build, and you can safely ignore these errors. As we get all our dependencies moved over to Maven 2, and these errors will become less and less frequent.
