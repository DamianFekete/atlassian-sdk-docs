---
aliases:
- /server/framework/atlassian-sdk/common-coding-tasks-852076.html
- /server/framework/atlassian-sdk/common-coding-tasks-852076.md
category: devguide
confluence_id: 852076
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852076
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852076
learning: guides
legacy_url: https://developer.atlassian.com/docs/common-coding-tasks
new_url: /server/framework/atlassian-sdk/common-coding-tasks
platform: server
product: atlassian-sdk
subcategory: learning
title: Common coding tasks
---
# Common coding tasks

All of the <a href="http://www.atlassian.com/software/" class="external-link">Atlassian products</a> are extensible. Each one has unique capabilities and requirements, as described in our product tutorials and references. But they also share s common underlying platform. Thus, there are some coding tasks and concepts that are common across applications. These include adding a configuration UI for a plugin, working with the activity stream, or accommodating websudo in your plugin.

The following pages describe some of these common programming tasks. 

-   [Development Cycle](/server/framework/atlassian-sdk/development-cycle)
-   [Creating an Admin Configuration Form](/server/framework/atlassian-sdk/creating-an-admin-configuration-form)
-   [Using Standard Page Decorators](/server/framework/atlassian-sdk/using-standard-page-decorators)
-   [Adding a Configuration UI for your Plugin](/server/framework/atlassian-sdk/adding-a-configuration-ui-for-your-plugin)
-   [Adding WebSudo Support to your Plugin](/server/framework/atlassian-sdk/adding-websudo-support-to-your-plugin)
-   [Storing plugin settings](/server/framework/atlassian-sdk/storing-plugin-settings)
-   [Internationalising your plugin](/server/framework/atlassian-sdk/internationalising-your-plugin)

Once you've got a handle on the common aspects of Atlassian plugin programming, you can dive into the product-specific references below. You may know about Confluence or JIRA, but have you considered creating a plugin for Bitbucket Server or Bamboo?

 

{{% note %}}

JIRA

So you're thinking of customising [JIRA](https://developer.atlassian.com/display/JIRADEV), our issue tracker and project planning tool? Maybe you want to [change the way JIRA looks](https://developer.atlassian.com/display/JIRADEV/JIRA+templates+and+JSPs) . Or [create a custom field type](https://developer.atlassian.com/display/JIRADEV/Tutorial+-+Creating+a+custom+field+type). Take a look at the [Getting started guide](https://developer.atlassian.com/display/JIRADEV/Getting+started) or interact with JIRA via the [remote APIs](https://developer.atlassian.com/display/JIRADEV/JIRA+APIs) .

You can also build for the JIRA applications, like JIRA Software and JIRA Service Desk. Perhaps you want to interact with sprints via the JIRA Software REST API or develop your own Rule Component for JIRA Service Desk Automation. Check out the [JIRA Software development guide](https://developer.atlassian.com/display/JIRADEV/JIRA+Software+development+guide) and the [JIRA Service Desk development guide](https://developer.atlassian.com/display/JIRADEV/JIRA+Service+Desk+development+guide) for more details.

{{% /note %}}{{% note %}}

Confluence

[Confluence](https://developer.atlassian.com/display/CONFDEV) is a collaboration platform you can use for project planning, design, knowledge management, documentation, or as a company intranet--you name it. There are two main ways to develop with Confluence: using the remote API or developing an add-on. If you're integrating Confluence with another application, you'll most likely want to use the [remote API](https://developer.atlassian.com/display/CONFCLOUD/Confluence+REST+API). If you'd like to add capabilities to Confluence, an [add-on](https://developer.atlassian.com/display/CONFCLOUD/Confluence+Connect+patterns) may be the answer. For a quick customisation that requires only HTML, CSS and JavaScript, try a [user macro](https://developer.atlassian.com/display/CONFDEV/Confluence+User+Macro+Guide).

You can develop add-ons for [Confluence Cloud](https://developer.atlassian.com/display/CONFCLOUD) or [Server](https://developer.atlassian.com/display/CONFDEV).

{{% /note %}}{{% note %}}

Bitbucket Server (formerly Stash)

[Bitbucket Server](https://developer.atlassian.com/stash/docs/latest/) provides on-premises DVCS where you can keep all your stuff. And it's extensible. Take a look at some <a href="http://atlassian.bitbucket.org/stash/" class="external-link">examples</a>.

{{% /note %}}{{% note %}}

Bamboo

Got continuous integration? Then you've got [Bamboo](https://developer.atlassian.com/display/BAMBOODEV), a build server that does more than mindlessly run your builds over and over. Enhance Bamboo's awesomeness by building a [plugin](https://developer.atlassian.com/display/BAMBOODEV/Bamboo+Plugin+Guide) or check the [remote APIs](https://developer.atlassian.com/display/BAMBOODEV/REST+APIs) .

{{% /note %}}{{% note %}}

Crowd

[Crowd](https://developer.atlassian.com/display/CROWDDEV) is a web application that manages users, permissions and application access control. It offers a number of out-of-the-box connectors for well known applications and directories. If yours is not one of them, you can write a [custom connector](https://developer.atlassian.com/display/CROWDDEV/Remote+API+Reference). You can also add to Crowd functionality by writing a [plugin](https://developer.atlassian.com/display/CROWDDEV/Developing+Plugins+for+Crowd) .

{{% /note %}}{{% note %}}

FishEye and Crucible

[FishEye and Crucible](https://developer.atlassian.com/display/FECRUDEV) add reporting, visualisation, notifications, code sharing and peer review to your source repository. Develop [plugins and gadgets](https://developer.atlassian.com/display/FECRUDEV/FishEye+and+Crucible+Plugin+Guide) to extend FishEye and Crucible. Use the [remote APIs](https://developer.atlassian.com/display/FECRUDEV/Remote+API+Reference) to integrate FishEye and Crucible software with other systems.

{{% /note %}}




















































































































































































































