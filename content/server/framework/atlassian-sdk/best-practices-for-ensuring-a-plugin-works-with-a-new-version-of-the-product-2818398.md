---
title: Best Practices for Ensuring a Plugin Works with a New Version Of the Product 2818398
aliases:
    - /server/framework/atlassian-sdk/best-practices-for-ensuring-a-plugin-works-with-a-new-version-of-the-product-2818398.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818398
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818398
confluence_id: 2818398
platform:
product:
category:
subcategory:
---
# Documentation : Best Practices for ensuring a plugin works with a new version of the product

#### Read the Upgrade Guide

The product developers publish upgrade guides each time they release a new version of the product. They often use these upgrade guides to mention things that have changes in the code: new APIS, deprecations, new libraries, etc. Read **all** the upgrades between the version you are currently running on and the one you wish to move to.

-   <a href="#jira-upgrade-guides" class="unresolved">JIRA Upgrade Guides</a>
-   <a href="#jira-upgrade-guides" class="unresolved">Confluence Release Notes</a> (Upgrade guides are attached to each release notes page)
-   <a href="#jira-upgrade-guides" class="unresolved">Bamboo Upgrade Guides</a>
-   <a href="#jira-upgrade-guides" class="unresolved">Crowd Upgrade Guides</a>
-   <a href="#jira-upgrade-guides" class="unresolved">Fisheye Upgrade Guides</a>
-   <a href="#jira-upgrade-guides" class="unresolved">Crucible Upgrade Guides</a>

#### Upgrade your POM and recompile the plugin against the new product.version

Change your project's POM so that you specify the correct target version. For example, you might change the property `confluence.version` from 2.4.5 to 2.7.1. Once you've done this, do a `mvn clean compile` to see if anything has been broken.

#### Watch for deprecation warnings

Watch for deprecation warnings during compilation or in your IDE. It's a good idea to correct these warnings as early as possible.

#### Run the test suite

Be sure you run the full test-suite over your newly-compiled plugin. (You do have a [test suite](https://developer.atlassian.com/pages/viewpage.action?pageId=2818653), don't you?)

#### Test your plugin's functionality manually.

Be sure to test your plugin functionality manually inside a running instance of the product.

#### Test the product upgrade (including your plugin) with a backup copy of your data

If at all possible, we strongly recommend attempting the upgrade in a test-bed before doing so with your live system. You'll want to run the upgrade and install the new plugin, making sure that all the data is upgraded properly, that the new plugin works as expected, that there are not unexpected errors in the logs, etc.

#### Backup all your data

This is critical. You **must** perform a full backup of your data (database, attachments, indexes, confluence.home, etc) before attempting an upgrade.

#### Perform the real upgrade

Perform the real upgrade with your real data and install your new plugin. Test everything again before you bring your system back online.

















































































































































































































































































































