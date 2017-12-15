---
aliases:
- /server/framework/atlassian-sdk/plugin-release-checklist-2818392.html
- /server/framework/atlassian-sdk/plugin-release-checklist-2818392.md
category: devguide
confluence_id: 2818392
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818392
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818392
date: '2017-12-08'
guides: guides
legacy_title: Plugin Release Checklist
platform: server
product: atlassian-sdk
subcategory: learning
title: Plugin release checklist
---
# Plugin release checklist

Each time you release a new version of a plugin, there are certain steps you should perform.

## Creating the release

1.  Make sure your plugin's **pom.xml** is up-to-date. This includes accurate sections for:
    -   *Parent POM* -- Make sure that the plugin is using the correct parent POM for the product and the most recent version of it.
    -   *version* -- It should be `<version_to_be_released>`-SNAPSHOT.
    -   *scm* -- Source control repository locations.
    -   *atlassian.product.version*
    -   *atlassian.product.data.version*
2.  Run **mvn release:prepare** -- This will update your pom.xml release numbers and make a new tag for the release.
3.  Run **mvn release:perform** -- This will:
    1.  Run tests
    2.  Compiles code and package it
    3.  Put the binary package in an appropriate [Atlassian Maven Repository](/server/framework/atlassian-sdk/atlassian-maven-repositories-2818705.html) and your local Maven repository.
4.  Copy the created binary package from your target sub-directory to the project's `jars` sub-directory (in SVN). Then schedule it for addition to SVN before finally committing the added resource.

## Updating the plugin's project

\#You'll need to release the current version of the project in JIRA and move any unfinished issues for the project to a later version. Here's how:

1.  1.  Go to the project page in JIRA.
    2.  Click on **Administer Project**.
    3.  Under **Versions**, click on **Manage versions**.
    4.  From this screen, choose "release" for the version that you just created. Make sure the date is correct, and move any remaining open issues to the next unreleased version.

2.  Update plugins documentation on on <a href="http://studio.plugins.atlassian.com/wiki/" class="uri external-link">studio.plugins.atlassian.com/wiki/</a>.
3.  Update the plugin's listing on <a href="http://plugins.atlassian.com" class="uri external-link">plugins.atlassian.com</a>
4.  Communicate about release (probably with a blog post and a post to the appropriate mailing list.)
