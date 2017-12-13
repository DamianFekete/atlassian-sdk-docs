---
aliases:
- /server/framework/atlassian-sdk/-inclusionslibrary-5668913.html
- /server/framework/atlassian-sdk/-inclusionslibrary-5668913.md
category: devguide
confluence_id: 5668913
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5668913
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5668913
date: '2017-12-08'
legacy_title: _InclusionsLibrary
platform: server
product: atlassian-sdk
subcategory: other
title: _InclusionsLibrary
---
# \_InclusionsLibrary

The children of this page contain information which is **included in other pages**, both in the DOCS space and **in other spaces too**. This is a library of re-usable information chunks.

If you want to change any of these pages, be aware that:

-   Changing page names is problematic -- you will need to change all the `include` and `excerpt-include` macros manually.
-   The content is used in many places -- make sure your change is generic enough to fit the contexts in which the pages are used.

## Snippet Plugin Test

``` java
01. package com.example.plugins.tutorial.jira.mailhandlerdemo;
02. 
03. import com.atlassian.crowd.embedded.api.User;
04. import com.atlassian.jira.issue.Issue;
05. import com.atlassian.jira.service.util.handler.MessageHandler;
06. import com.atlassian.jira.service.util.handler.MessageHandlerContext;
07. import com.atlassian.jira.service.util.handler.MessageHandlerErrorCollector;
08. import com.atlassian.jira.service.util.handler.MessageUserProcessor;
09. import com.atlassian.mail.MailUtils;
10. import org.apache.commons.lang.StringUtils;
11. 
12. import java.util.Map;
13. import javax.mail.Message;
14. import javax.mail.MessagingException;
15. 
16. public class DemoHandler implements MessageHandler {
17.     private String issueKey;
18.     private final IssueKeyValidator issueKeyValidator;
19.     private final MessageUserProcessor messageUserProcessor;
20.     public static final String KEY_ISSUE_KEY = "issueKey";
21. 
22.     // we can use dependency injection here too!
23.     public DemoHandler(MessageUserProcessor messageUserProcessor, IssueKeyValidator issueKeyValidator) {
24.         this.messageUserProcessor = messageUserProcessor;
25.         this.issueKeyValidator = issueKeyValidator;
26.     }
27. 
28.     @Override
29.     public void init(Map<String, String> params, MessageHandlerErrorCollector monitor) {
30.         // getting here issue key configured by the user
31.         issueKey = params.get(KEY_ISSUE_KEY);
32.         if (StringUtils.isBlank(issueKey)) {
33.             // this message will be either logged or displayed to the user (if the handler is tested from web UI)
34.             monitor.error("Issue key has not been specified ('" + KEY_ISSUE_KEY + "' parameter). This handler will not work correctly.");
35.         }
36.         issueKeyValidator.validateIssue(issueKey, monitor);
37.     }
38. 
39.     @Override
40.     public boolean handleMessage(Message message, MessageHandlerContext context) throws MessagingException {
41.         // let's again validate the issue key - meanwhile issue could have been deleted, closed, etc..
42.         final Issue issue = issueKeyValidator.validateIssue(issueKey, context.getMonitor());
43.         if (issue == null) {
44.             return false; // returning false means that we were unable to handle this message. It may be either
45.             // forwarded to specified address or left in the mail queue (if forwarding not enabled)
46.         }
47.         // this is a small util method JIRA API provides for us, let's use it.
48.         final User sender = messageUserProcessor.getAuthorFromSender(message);
49.         if (sender == null) {
50.             context.getMonitor().error("Message sender(s) '" + StringUtils.join(MailUtils.getSenders(message), ",")
51.                     + "' do not have corresponding users in JIRA. Message will be ignored");
52.             return false;
53.         }
54.         final String body = MailUtils.getBody(message);
55.         final StringBuilder commentBody = new StringBuilder(message.getSubject());
56.         if (body != null) {
57.             commentBody.append("\n").append(StringUtils.abbreviate(body, 100000)); // let trim too long bodies
58.         }
59.         // thanks to using passed context we don't need to worry about normal run vs. test run - our call
60.         // will be dispatched accordingly
61.         context.createComment(issue, sender, commentBody.toString(), false);
62.         return true; // returning true means that we have handled the message successfully. It means it will be deleted next.
63.     }
64. }
```

## Children

-   [\_About Plugin Framework 2 Documentation](/server/framework/atlassian-sdk/about-plugin-framework-2-documentation.snippet)
-   [\_Bamboo Plugin Tutorials](/server/framework/atlassian-sdk/bamboo-plugin-tutorials.snippet)
-   [\_Components of Plugin Development Platform](/server/framework/atlassian-sdk/components-of-plugin-development-platform.snippet)
-   [\_Confluence Plugin Tutorials](/server/framework/atlassian-sdk/confluence-plugin-tutorials.snippet)
-   [\_Cross-Product Plugin Tutorials](/server/framework/atlassian-sdk/cross-product-plugin-tutorials.snippet)
-   [\_Development Hubs](/server/framework/atlassian-sdk/development-hubs.snippet)
-   [\_FastDevWorkFlow](/server/framework/atlassian-sdk/fastdevworkflow.snippet)
-   [\_FECRU Plugin Tutorials](/server/framework/atlassian-sdk/fecru-plugin-tutorials.snippet)
-   [\_Getting Help on Plugin SDK](/server/framework/atlassian-sdk/getting-help-on-plugin-sdk.snippet)
-   [\_Images for Release Notes](/server/framework/atlassian-sdk/images-for-release-notes.snippet)
-   [\_JIRA Plugin Tutorials](/server/framework/atlassian-sdk/jira-plugin-tutorials.snippet)
-   [\_LocalM2PluginSettings](/server/framework/atlassian-sdk/localm2pluginsettings.snippet)
-   [\_MailingLists](/server/framework/atlassian-sdk/mailinglists.snippet)
-   [\_Note about Maven Bundled with SDK](/server/framework/atlassian-sdk/note-about-maven-bundled-with-sdk.snippet)
-   [\_Package Name](/server/framework/atlassian-sdk/package-name.snippet)
-   [\_PluginFramework\_InclusionsLibrary](/server/framework/atlassian-sdk/pluginframework-inclusionslibrary.snippet)
-   [\_PluginPlatformDiagram](/server/framework/atlassian-sdk/pluginplatformdiagram.snippet)
-   [\_Plugin Platform Version](/server/framework/atlassian-sdk/plugin-platform-version.snippet)
-   [\_PluginSDK\_StepByStep\_Diagram](/server/framework/atlassian-sdk/pluginsdk-stepbystep-diagram.snippet)
-   [\_Plugin SDK Download Latest](/server/framework/atlassian-sdk/plugin-sdk-download-latest.snippet)
-   [\_PluginSDKQuickStart](/server/framework/atlassian-sdk/pluginsdkquickstart.snippet)
-   [\_Plugin SDK Supported Applications and Default Ports](/server/framework/atlassian-sdk/plugin-sdk-supported-applications-and-default-ports.snippet)
-   [\_Plugin SDK Version](/server/framework/atlassian-sdk/plugin-sdk-version.snippet)
-   [\_Plugin Tutorial Step - Build and Test](/server/framework/atlassian-sdk/plugin-tutorial-step-build-and-test.snippet)
-   [\_Plugin Tutorial Step - Create Plugin](/server/framework/atlassian-sdk/plugin-tutorial-step-create-plugin.snippet)
-   [\_RABDescription](/server/framework/atlassian-sdk/rabdescription.snippet)
-   [\_\_newreleaseSharedAccessLayer](/server/framework/atlassian-sdk/newreleasesharedaccesslayer.snippet)
-   [\_Images](/server/framework/atlassian-sdk/images.snippet)
-   [\_SAL Overview](/server/framework/atlassian-sdk/sal-overview.snippet)
-   [\_Version Compatibility for Shared Access Layer](/server/framework/atlassian-sdk/version-compatibility-for-shared-access-layer.snippet)
-   [\_RABQuickStart](/server/framework/atlassian-sdk/rabquickstart.snippet)
-   [\_REST Plugin Module Overview](/server/framework/atlassian-sdk/rest-plugin-module-overview.snippet)
-   [\_SDK Known Issues](/server/framework/atlassian-sdk/sdk-known-issues.snippet)
-   [\_SDK Linux](/server/framework/atlassian-sdk/sdk-linux.snippet)
-   [\_SDK Version](/server/framework/atlassian-sdk/sdk-version.snippet)
-   [\_SDK Windows](/server/framework/atlassian-sdk/sdk-windows.snippet)
-   [\_TempPagetree](/server/framework/atlassian-sdk/temppagetree.snippet)
-   [\_Version Compatibility for Plugin Development Platform](/server/framework/atlassian-sdk/version-compatibility-for-plugin-development-platform.snippet)
-   [\_Version Compatibility for REST Plugin](/server/framework/atlassian-sdk/version-compatibility-for-rest-plugin.snippet)
-   [REST\_QuickStart\_References](/server/framework/atlassian-sdk/rest-quickstart-references.snippet)
-   [\_Module definition example](/server/framework/atlassian-sdk/module-definition-example.snippet)
-   [\_Copyright Notice](/server/framework/atlassian-sdk/copyright-notice.snippet)














































































































