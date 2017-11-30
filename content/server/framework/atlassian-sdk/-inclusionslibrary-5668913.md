---
title: Inclusionslibrary 5668913
aliases:
    - /server/framework/atlassian-sdk/-inclusionslibrary-5668913.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5668913
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5668913
confluence_id: 5668913
platform:
product:
category:
subcategory:
---
# Documentation : \_InclusionsLibrary

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

-   [\_About Plugin Framework 2 Documentation](/server/framework/atlassian-sdk/-about-plugin-framework-2-documentation-2818472.html)
-   [\_Bamboo Plugin Tutorials](/server/framework/atlassian-sdk/-bamboo-plugin-tutorials-8946290.html)
-   [\_Components of Plugin Development Platform](/server/framework/atlassian-sdk/-components-of-plugin-development-platform-2818473.html)
-   [\_Confluence Plugin Tutorials](/server/framework/atlassian-sdk/-confluence-plugin-tutorials-2818467.html)
-   [\_Cross-Product Plugin Tutorials](/server/framework/atlassian-sdk/-cross-product-plugin-tutorials-8946215.html)
-   [\_Development Hubs](/server/framework/atlassian-sdk/-development-hubs-6291467.html)
-   [\_FastDevWorkFlow](/server/framework/atlassian-sdk/-fastdevworkflow-8945826.html)
-   [\_FECRU Plugin Tutorials](/server/framework/atlassian-sdk/-fecru-plugin-tutorials-8946253.html)
-   [\_Getting Help on Plugin SDK](/server/framework/atlassian-sdk/-getting-help-on-plugin-sdk-2818463.html)
-   [\_Images for Release Notes](/server/framework/atlassian-sdk/-images-for-release-notes-7372858.html)
-   [\_JIRA Plugin Tutorials](/server/framework/atlassian-sdk/-jira-plugin-tutorials-2818468.html)
-   [\_LocalM2PluginSettings](/server/framework/atlassian-sdk/-localm2pluginsettings-13632950.html)
-   [\_MailingLists](/server/framework/atlassian-sdk/-mailinglists-5669830.html)
-   [\_Note about Maven Bundled with SDK](/server/framework/atlassian-sdk/-note-about-maven-bundled-with-sdk-2818464.html)
-   [\_Package Name](/server/framework/atlassian-sdk/-package-name-2818460.html)
-   [\_PluginFramework\_InclusionsLibrary](/server/framework/atlassian-sdk/-pluginframework-inclusionslibrary-852042.html)
-   [\_PluginPlatformDiagram](/server/framework/atlassian-sdk/-pluginplatformdiagram-7897096.html)
-   [\_Plugin Platform Version](/server/framework/atlassian-sdk/-plugin-platform-version-2818469.html)
-   [\_PluginSDK\_StepByStep\_Diagram](/server/framework/atlassian-sdk/-pluginsdk-stepbystep-diagram-5670021.html)
-   [\_Plugin SDK Download Latest](/server/framework/atlassian-sdk/-plugin-sdk-download-latest-2818137.html)
-   [\_PluginSDKQuickStart](/server/framework/atlassian-sdk/-pluginsdkquickstart-5669863.html)
-   [\_Plugin SDK Supported Applications and Default Ports](/server/framework/atlassian-sdk/-plugin-sdk-supported-applications-and-default-ports-2818466.html)
-   [\_Plugin SDK Version](/server/framework/atlassian-sdk/-plugin-sdk-version-2818470.html)
-   [\_Plugin Tutorial Step - Build and Test](/server/framework/atlassian-sdk/-plugin-tutorial-step-build-and-test-2818459.html)
-   [\_Plugin Tutorial Step - Create Plugin](/server/framework/atlassian-sdk/-plugin-tutorial-step-create-plugin-11306016.html)
-   [\_RABDescription](/server/framework/atlassian-sdk/-rabdescription-8947331.html)
-   [\_\_newreleaseSharedAccessLayer](/server/framework/atlassian-sdk/--newreleasesharedaccesslayer-5242947.html)
-   [\_Images](/server/framework/atlassian-sdk/-images-5242881.html)
-   [\_SAL Overview](/server/framework/atlassian-sdk/-sal-overview-5242884.html)
-   [\_Version Compatibility for Shared Access Layer](/server/framework/atlassian-sdk/-version-compatibility-for-shared-access-layer-5242943.html)
-   [\_RABQuickStart](/server/framework/atlassian-sdk/-rabquickstart-8947342.html)
-   [\_REST Plugin Module Overview](/server/framework/atlassian-sdk/-rest-plugin-module-overview-4915211.html)
-   [\_SDK Known Issues](/server/framework/atlassian-sdk/-sdk-known-issues-2818471.html)
-   [\_SDK Linux](/server/framework/atlassian-sdk/-sdk-linux-11305049.html)
-   [\_SDK Version](/server/framework/atlassian-sdk/-sdk-version-11305037.html)
-   [\_SDK Windows](/server/framework/atlassian-sdk/-sdk-windows-11305043.html)
-   [\_TempPagetree](/server/framework/atlassian-sdk/-temppagetree-5668905.html)
-   [\_Version Compatibility for Plugin Development Platform](/server/framework/atlassian-sdk/-version-compatibility-for-plugin-development-platform-2818465.html)
-   [\_Version Compatibility for REST Plugin](/server/framework/atlassian-sdk/-version-compatibility-for-rest-plugin-4915208.html)
-   [REST\_QuickStart\_References](/server/framework/atlassian-sdk/rest-quickstart-references-6291717.html)
-   [\_Module definition example](/server/framework/atlassian-sdk/-module-definition-example-5669180.html)
-   [\_Copyright Notice](/server/framework/atlassian-sdk/-copyright-notice-23691392.html)





















































































































































































































































