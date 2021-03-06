---
title: Specifying a Particular Version Of the Host Application 2818657
aliases:
    - /server/framework/atlassian-sdk/specifying-a-particular-version-of-the-host-application-2818657.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818657
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818657
confluence_id: 2818657
platform:
product:
category:
subcategory:
---
# Documentation : Specifying a particular version of the host application

The `atlas-run` command will download the latest version of the application binaries into your local Maven repository. If you want to develop against a version of the host application other than the very latest, you can specify the version to use as a parameter of your `atlas-run` command.

For example, let's assume you want to use Confluence 3.1:

1.  Run `atlas-clean`.
2.  Run `atlas-run -v 3.1`  
    or `atlas-run --version 3.1`.

Alternatively, you can permanently change the application version number in the dependencies section of your POM. Note that your POM may use a property to hold the version number, like this:

``` javascript
<properties>
    <confluence.version>RELEASE</confluence.version>
</properties>
```

You plugin will always build and deploy against this version, until you change this property.

For example, if you are happy to use Confluence 3.1 for a while, you would change the version to the following:

``` javascript
<properties>
    <confluence.version>3.1</confluence.version>
</properties>
```
