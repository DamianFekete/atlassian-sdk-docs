---
aliases:
- /server/framework/atlassian-sdk/changing-the-default-maven-version-19071041.html
- /server/framework/atlassian-sdk/changing-the-default-maven-version-19071041.md
category: devguide
confluence_id: 19071041
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=19071041
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=19071041
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk/changing-the-default-maven-version
new_url: /server/framework/atlassian-sdk/changing-the-default-maven-version
platform: server
product: atlassian-sdk
subcategory: learning
title: Changing the default Maven version
---
# Changing the default Maven version

This page describes how to change the default instance of Apache Maven used by the SDK.

## About Maven and the SDK

The SDK includes a bundled instance of Apache Maven used, behind the scenes, to execute the `atlas` commands. You can change the default Maven instance used by the SDK to use another version, including Maven 3.

{{% note %}}

To check which version of Maven the SDK is using, enter the `atlas-version` command. The Maven version appears in a line similar to:

`Apache Maven 2.1.0 (r755702; 2009-03-18 12:10:27-0700)`

{{% /note %}}

The SDK works with any Maven version later than 2.1. While there are no known limitations in the use of a non-default Maven, the SDK has not been tested with all versions of Maven. 

## Setting the Maven version

To configure the SDK to use your own (non-default) Maven instance:

1.  Add an environment variable to your development system called `ATLAS_MVN.`
2.  Set the value of `ATLAS_MVN` to your Maven executable. Keep in mind this should be the Maven executable, not the Maven home.  
    For example, the following command sets and exports the variable with the location of the Maven executable:  
    `export ATLAS_MVN=/usr/bin/mvn3`
3.  Verify the configuration by running the `atlas-version` command. Make sure that the Maven instance in use is the one you specified.

That's it! Now you can use the usual SDK commands, such as `atlas-run` and `atlas-create-confluence-plugin`. When you do, the SDK uses your Maven instance instead of the bundled default one.






















































































































































































