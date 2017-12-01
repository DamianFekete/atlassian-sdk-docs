---
aliases:
- /server/framework/atlassian-sdk/writing-and-running-plugin-tests-15335861.html
- /server/framework/atlassian-sdk/writing-and-running-plugin-tests-15335861.md
category: devguide
confluence_id: 15335861
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=15335861
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=15335861
legacy_url: https://developer.atlassian.com/docs/getting-started/writing-and-running-plugin-tests
new_url: /server/framework/atlassian-sdk/writing-and-running-plugin-tests
platform: server
product: atlassian-sdk
subcategory: intro
title: Writing and running plugin tests
---
# Writing and running plugin tests

This tutorial describes the concepts you need to understand, the tools you use, and processes you follow for testing a plugin in the Atlassian Plugin Framework.  You can use all of the concepts, tools, and processes described in this section with any plugin regardless of the plugin's intended host application (for example, JIRA, Confluence, or Stash). This section contains the following topics:

-   [Generate and Examine Skeleton Tests](/server/framework/atlassian-sdk/generate-and-examine-skeleton-tests)
-   [Create and Run Unit Tests](/server/framework/atlassian-sdk/create-and-run-unit-tests)
-   [Create and Run Traditional Integration Tests](/server/framework/atlassian-sdk/create-and-run-traditional-integration-tests)
-   [Run Wired Tests with the Plugin Test Console](/server/framework/atlassian-sdk/run-wired-tests-with-the-plugin-test-console)
-   [Create Test Data and a Test Fixture](/server/framework/atlassian-sdk/create-test-data-and-a-test-fixture)
-   [Staff README for Foundation Test Docs](/server/framework/atlassian-sdk/staff-readme-for-foundation-test-documentation)

## How to work through the tutorial

Beginners should work through each page sequentially as each new page builds on the material from the previous page. Each page concludes with a **Next Steps** heading that recaps and tells you where to go next. Beginners should allow two hours to work through the entire tutorial.

Experienced programmers or readers with previous knowledge of Atlassian plugin development processes, may choose to just skim or skip around. Each page encapsulates the core knowledge for each part of the testing process.

## Check Your Work

We encourage you to work through this tutorial. If you want to skip ahead or check your work when you are done, you can find the plugin source code on Atlassian Bitbucket. Bitbucket serves a public Git repository containing the tutorial's code. To clone the repository, issue the following command:

``` bash
git clone https://atlassian_tutorial@bitbucket.org/atlassian_tutorial/testtutorial.git
```

Alternatively, you can download the latest source here: <a href="https://bitbucket.org/atlassian_tutorial/testtutorial/downloads" class="uri external-link">https://bitbucket.org/atlassian_tutorial/testtutorial/downloads</a>.











