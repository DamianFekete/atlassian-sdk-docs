---
aliases:
- /server/framework/atlassian-sdk/packaging-and-releasing-your-plugin-2818640.html
- /server/framework/atlassian-sdk/packaging-and-releasing-your-plugin-2818640.md
category: devguide
confluence_id: 2818640
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818640
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818640
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks/development-cycle/packaging-and-releasing-your-plugin
new_url: /server/framework/atlassian-sdk/packaging-and-releasing-your-plugin
platform: server
product: atlassian-sdk
subcategory: learning
title: Packaging and releasing your plugin
---
# Packaging and releasing your plugin

So you've developed a killer plugin and you want to share it with the world. How do you do it? This page gives you an outline. For complete information on making your plugin available on the <a href="https://marketplace.atlassian.com/" class="external-link">Atlassian Marketplace</a>, see [Marketplace documentation](https://developer.atlassian.com/display/MARKET). 

## Packaging your plugin

Once you're happy with your plugin and ready to release it, [use the SDK to package your plugin](/server/framework/atlassian-sdk/atlas-package).

This will produce a `jar` file in the plugin's `target` directory. You can <a href="http://confluence.atlassian.com/display/UPM" class="external-link">use the UPM</a> to install it for testing in your staging or production environments.

## Releasing your plugin

**A Note about Quality**

We have set certain criteria for our own plugin development. If you are working on a plugin that you wish to share with the community, we encourage you to try and meet these same criteria in your work. It will result in a higher quality product and make it easier for others to collaborate.

-   Have unit and functional tests with a reasonable amount of code coverage.
-   Support internationalization, as many of Atlassian's customers use a first language other than English.
-   Most importantly, **make the plugin available in the <a href="https://marketplace.atlassian.com" class="external-link">Atlassian Marketplace</a>.**This allows your users to one-click install it from the UPM. This listing is also the place to provide the following essential information:
    -   an issue tracker where your users can file bugs and feature requests;
    -   a link to source code to allow them to hack the plugin to meet their specific needs;
    -   a link to the plugin's complete, accurate and attractive documentation;
    -   screenshots of your plugin in action;
    -   a YouTube video giving a walkthrough or marketing the plugin's features.

### 1. Choose a License

If you're going to be distributing your plugin, it's a good idea to explicitly license your software. There are many choices, and for the most part you are free to choose whichever one you'd like. The only caveat is that you can't use the GPL, as Confluence and JIRA are not themselves GPL'd. (There is much argument about this point, but we've had GPL authors complain, and we'd rather err on the side of doing the right thing.)

If you don't know which license to use, we generally recommend the <a href="http://www.apache.org/licenses/LICENSE-2.0.html" class="external-link">Apache2 license</a>. It simple and completely open: people are free to do whatever they want to the software, and you're free of any liability. It's the license we use for most of our plugins.

Of course, you're also free to charge for your plugin, if you want. If so, you should create an appropriate commercial software license. You can also sell your plugin in the [Atlassian Marketplace](https://developer.atlassian.com/display/MARKET/Atlassian+Marketplace), available from <a href="http://plugins.atlassian.com" class="uri external-link">http://plugins.atlassian.com</a>; [see here for details](https://developer.atlassian.com/display/MARKET/Atlassian+Marketplace).

### 2. Upload your Code to a Public Source Control Server

One of the best reasons to share your plugin is that you might attract other developers to help you with it. In order for them to do that, you'll need a way to share source code. Atlassian offers free Git and Mercurial hosting on <a href="http://bitbucket.org" class="external-link">bitbucket.org</a>.

Of course, you're also free to host it on any service of your choosing.

### 3. Provide a Public Issue Tracker

As soon as you make your plugin available, the very first question people will ask is, "where can I file feature requests and bug reports?" Handling such reports through email will become unwieldy almost immediately. Make sure an issue tracker, such as JIRA Cloud or Bitbucket, is available. In all cases, take care that your plugin's entry on the Atlassian Marketplace takes users to it.

### 4. Upload your Plugin to the Internet

Your packaged plugin must be accessible on the Internet in order for users to download and install it. The easiest way to do this is to list your plugin on the Atlassian Marketplace. Alternatively, any other file hosting service (such as a public Dropbox folder) is suitable.

### 5. Provide a Public Documentation site

Provide detailed information about the plugin's abilities, limitations, and requirements. Use Confluence Cloud, BitBucket's wiki, or your own site. Make sure it's linked from your plugin's Atlassian Marketplace entry.

### 6. Announce your Plugin

You should also announce the release of your plugin on <a href="http://answers.atlassian.com" class="external-link">Atlassian Answers</a>, where you can reach hundreds of potential users or customers.

### 7. Collaborate

Once people start to use your plugin, they're going to want to get involved. Some people will file bugs. Some people will request new features. And best of all, some users might pitch in an add new a feature themselves. You can encourage this behavior by being responsive, answering questions, making fixes and additions as quickly as you can. Demonstrating momentum is the surest way to keep people interested and motivate them to contribute themselves.

## Releasing a Version Update to your plugin

Each time you release a new version of a plugin, there are certain steps you should perform.

1.  Make sure your plugin's **pom.xml** is up-to-date. This includes accurate sections for:
    -   *Parent POM* -- Make sure that the plugin is using the correct parent POM for the product and the most recent version of it.
    -   *version* -- It should be `<version_to_be_released>`-SNAPSHOT.
    -   *scm* -- Source control repository locations.
    -   *atlassian.product.version*
    -   *atlassian.product.data.version*
2.  Run **mvn <a href="http://releaseprepare" class="external-link">release:prepare</a>** -- This will update your pom.xml release numbers and make a new tag for the release.
3.  Run **mvn <a href="http://releaseperform" class="external-link">release:perform</a>**-- This will:
    1.  Run tests
    2.  Compiles code and package it
    3.  Put the binary package in your local Maven repository.
4.  Copy the created binary package from your target sub-directory to the project's `jars` sub-directory (in SVN). Then schedule it for addition to SVN before finally committing the added resource.











































































































































































































