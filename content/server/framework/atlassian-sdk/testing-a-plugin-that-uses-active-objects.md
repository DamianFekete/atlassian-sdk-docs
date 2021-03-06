---
aliases:
- /server/framework/atlassian-sdk/testing-a-plugin-that-uses-active-objects-5669196.html
- /server/framework/atlassian-sdk/testing-a-plugin-that-uses-active-objects-5669196.md
category: devguide
confluence_id: 5669196
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669196
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669196
date: '2017-12-08'
guides: guides
legacy_title: Testing a plugin that uses Active Objects
platform: server
product: atlassian-sdk
subcategory: learning
title: Testing a plugin that uses Active Objects
---
# Testing a plugin that uses Active Objects

We want to note a few items that you, the plugin developer, should be concerned with when testing a plugin that uses Active Objects.

#### Backup, Restore & Upgrade

Active Objects allows your plugins to participate in the host product's native backup and restore process. However, in so doing, your plugin also has the potential to cause problems with that process. That could have the very serious consequence of preventing customers from restoring their data.

If you are developing an plugin that uses AO, it is critically important that you test backup and restore, and do so over a representative selection of host product versions.

In addition, the Active Objects framework gives you the ability to upgrade your plugin's data. This process is also potentially risky, and you should ensure that this is tested as well.

#### Supported Databases

The AO framework is an ORM and deals directly with the host product's database. We ensure that our products work with a certain selection of databases. You, the plugin, must do likewise. You can find Atlassian's up-to-date list of supported databases in our documentation:

-   <a href="http://confluence.atlassian.com/display/DOC/Supported+Platforms" class="uri external-link">confluence.atlassian.com/display/DOC/Supported+Platforms</a>
-   <a href="http://confluence.atlassian.com/display/JIRA/Supported+Platforms" class="uri external-link">confluence.atlassian.com/display/JIRA/Supported+Platforms</a>
-   <a href="http://confluence.atlassian.com/display/FISHEYE/Supported+Platforms" class="uri external-link">confluence.atlassian.com/display/FISHEYE/Supported+Platforms</a>
-   <a href="http://confluence.atlassian.com/display/BAMBOO/Supported+Platforms" class="uri external-link">confluence.atlassian.com/display/BAMBOO/Supported+Platforms</a>

We *strongly* encourage you to test your plugin with all of these databases before you release it.

#### Working with Atlassian Support

We also remind you that Atlassian Support will not be able to support your plugin. If we encounter customers who are having difficulty due to an interaction with your plugin, our course of action will be to disable that plugin and return their host product to normal functionality. The burden for plugin-related support is on you, the plugin author, so it is in your best interest to make sure these areas are fully tested.
