---
aliases:
- /server/framework/atlassian-sdk/staff-readme-for-foundation-test-docs-15336054.html
- /server/framework/atlassian-sdk/staff-readme-for-foundation-test-docs-15336054.md
category: devguide
confluence_id: 15336054
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=15336054
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=15336054
date: '2017-12-11'
legacy_title: Staff README for Foundation Test Docs
platform: server
product: atlassian-sdk
subcategory: other
title: Staff README for Foundation test documentation
---
# Staff README for Foundation test documentation

{{% warning %}}

This page is restricted to **atlassian-staff** by design. Do not remove the restriction on this page.

{{% /warning %}}

This page documents the status and suggestions for improvements to the Foundation test documentation.

## Information Related to Working with these Pages

This tutorial is designed so each page builds on the next.  It also provides readers with a sample code project. Readers that follow the tutorial exactly should be able to check their final code agains the Bitbucket project here:

<a href="https://bitbucket.org/atlassian_tutorial/testtutorial" class="uri external-link">https://bitbucket.org/atlassian_tutorial/testtutorial</a>

## Wish List for Improvements to this Tutorial

-   A more robust sample application that illustrates real-world page actions.  So, perhaps a servlet or page in the administration area, Javascript, and a template.   How would a user test each major component? Since this tutorial is a foundation tutorial, the sample application should be cross-functional. 
-   Include a section on Javascript testing for Qunit.  This should follow after updating the sample application.  Reference page for how to is on EAC here: <a href="https://extranet.atlassian.com/pages/viewpage.action?pageId=2020278642" class="uri external-link">https://extranet.atlassian.com/pages/viewpage.action?pageId=2020278642</a>.  Make sure to look at the comments because they reference other aspects of this work. 
-   Currently, all the code assumes an HSQL database.  In practice, testing with that database is not robust enough. We should provide a page instructions for using another more production-viable database such as MySQL
-   Running tests manually, using the test console are both demonstrated. Running tests from a Bamboo project is not.  The considerations are different but applicable. We should be encourage plugin programmers to automate their testing and to use our product -- Bamboo. 

    This text is for AOD THIS IS TEXT FOR BITBUCKET          

    this text that appears after































































































































































