---
aliases:
- /server/framework/atlassian-sdk/adding-activities-to-a-third-party-feed-with-the-java-api-5669691.html
- /server/framework/atlassian-sdk/adding-activities-to-a-third-party-feed-with-the-java-api-5669691.md
category: devguide
confluence_id: 5669691
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669691
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669691
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/activity-streams/adding-activities-to-a-third-party-feed-with-the-java-api
new_url: /server/framework/atlassian-sdk/adding-activities-to-a-third-party-feed-with-the-java-api
platform: server
product: atlassian-sdk
subcategory: learning
title: Adding Activities to a Third Party feed with the Java API
---
# Adding Activities to a Third Party feed with the Java API

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p>Activity Streams 5.0 and later.<br />
JIRA 5.0 and later.</p></td>
</tr>
</tbody>
</table>

 

## Overview

Activity Streams 5.0 includes a new, lightweight API that allows plugins to add activities to the Activity Stream. This API doesn't give you as much power as [building a full-fledged Activity Provider](https://developer.atlassian.com/display/STREAMS/Making+your+own+Activity+Streams+Provider), but it's extremely easy to use.

We'll demonstrate the API by building a sample plugin that uses a JIRA issue event listener to add an activity whenever an issue is deleted.

{{% note %}}

Source code for the complete plugin is available on <a href="https://bitbucket.org/jkodumal/streams-jira-delete-issue-plugin/" class="external-link">Bitbucket</a>

{{% /note %}}{{% warning %}}

The sample code shown here assumes that Activity Streams 5.0 is already bundled with JIRA. The source code in the Bitbucket repository bundles Activity Streams 5 into an alpha version of JIRA 5.0. I'll clean up the discrepancy when Streams 5.0 final is bundled with JIRA

{{% /warning %}}

## Create the plugin project

First we need to set up our development environment and create our plugin project and source directories. Assuming you have the Atlassian Plugin SDK installed, execute the following:

``` javascript
$ atlas-create-jira-plugin
```

Follow the prompts to complete the initial plugin setup. We've used `com.atlassian.labs` as our `groupId` and `streams-jira-delete-issue-plugin` as our `artifactId`.

## Add dependencies to the POM

First, we need to add a dependency on the `streams-thirdparty-api` and `streams-api` artifacts to the `dependencies` section in our `pom.xml` file:

``` xml
<dependency>
    <groupId>com.atlassian.streams</groupId>
    <artifactId>streams-thirdparty-api</artifactId>
    <version>5.0</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.atlassian.streams</groupId>
    <artifactId>streams-api</artifactId>
    <version>5.0</version>
    <scope>provided</scope>
</dependency>
```

The scope should be `provided`, as the library is part of Activity Streams 5, which is already bundled in JIRA. To create an event listener, we also need to add a few other dependencies:

``` xml
<dependency>
    <groupId>com.atlassian.event</groupId>
    <artifactId>atlassian-event</artifactId>
    <version>${atlassian.event.version}</version>
    <scope>provided</scope>
</dependency>
<dependency>
    <groupId>com.atlassian.sal</groupId>
    <artifactId>sal-api</artifactId>
    <scope>provided</scope>
    <version>${sal.api.version}</version>
</dependency>
```

## Import the `ActivityService`

We need to import the `ActivityService` component in our `atlassian-plugin.xml`:

``` xml
<component-import key="activityService" interface="com.atlassian.streams.thirdparty.api.ActivityService"/>
```

We can then use constructor injection whenever we need the `activityService`.

## Import other components

To get our event listener example working, we'll also need to inject a few other components from JIRA. We'll add the following lines to our `atlassian-plugin.xml`:

``` xml
<component-import key="eventPublisher" interface="com.atlassian.event.api.EventPublisher"/>
<component-import key="applicationProperties" interface="com.atlassian.sal.api.ApplicationProperties"/>
```

We're going to use `applicationProperties` to fetch the base URL of our JIRA application. We'll need the `eventPublisher` to subscribe to JIRA's issue events.

## Create the `DeleteIssueListener`

We're going to create a new component that registers itself as an event listener, and responds to deletion events by posting an activity via the `ActivityService`. Let's first declare the component in our `atlassian-plugin.xml`:

``` xml
<component key="userListener" class="com.atlassian.labs.streams.jira.DeleteIssueListener">
    <description>Class that processes JIRA delete issue events.</description>
</component>
```

As the xml snippet indicates, we'll also want to create a class called `DeleteIssueListener` in the `com.atlassian.labs.streams` package. Create that class, and add a constructor that injects the components that we need:

``` java
public class DeleteIssueListener
{
    private final EventPublisher eventPublisher;
    private final ActivityService activityService;
    private final ApplicationProperties applicationProperties;

    public DeleteIssueListener(EventPublisher eventPublisher,
                               ActivityService activityService,
                               ApplicationProperties applicationProperties)
    {
        this.eventPublisher = eventPublisher;
        this.activityService = activityService;
        this.applicationProperties = applicationProperties;
    }
}
```

As described in our <a href="http://confluence.atlassian.com/display/DEVNET/Plugin+Tutorial+-+Writing+event+listeners+with+the+atlassian-event+library#PluginTutorial-Writingeventlistenerswiththeatlassian-eventlibrary-Coordinateeventregistrationwiththepluginlifecycle" class="external-link">event listener plugin tutorial</a>, this component needs to tie its registration with the `eventPublisher` to our plugin's lifecycle. We can do that by implementing `DisposableBean` and `LifecycleAware`

``` java
public class DeleteIssueListener implements DisposableBean, LifecycleAware
{
   ...

    @Override
    public void destroy() throws Exception
    {
        eventPublisher.unregister(this);
    }

    @Override
    public void afterPropertiesSet() throws Exception
    {
        eventPublisher.register(this);
    }
}
```

## Create the activity

We'll create an activity whenever a JIRA issue is deleted, and post it using our `ActivityService`. The code is as follows:

``` java
@EventListener
public void onIssueDelete(IssueEvent issueEvent)
{
    if (issueEvent.getEventTypeId().equals(EventType.ISSUE_DELETED_ID))
    {
        User user = issueEvent.getUser();
        Either<ValidationErrors, Activity> result = new Activity.Builder(application("JIRA Deleted Issues", URI.create(applicationProperties.getBaseUrl())),
                                                 new DateTime(),
                                                 new UserProfile.Builder(user.getName()).fullName(user.getDisplayName())
                                                     .build())
            .content(some(html(issueEvent.getIssue().getDescription())))
            .title(some(html(user.getDisplayName() + " deleted " + issueEvent.getIssue().getKey() + " - " + issueEvent.getIssue().getSummary())))
            .url(some(URI.create(applicationProperties.getBaseUrl())))
            .build();
        for (Activity activity : result.right())
        {
            activityService.postActivity(activity);
        }
        for (ValidationErrors errors : result.left())
            log.error("Errors encountered attempting to post activity: " + errors.toString());
        }
    }
}
```

We create a new `Activity` by using the `Activity.Builder` helper class. `Activity.Builder.build()` returns `Either<ValidationErrors, Activity>`, which is a disjoint union : either we created a valid `Activity`, or we received a set of errors indicating the reasons why the `Activity` we tried to construct wasn't well formed. The two `for` loops are a clean way of handling the two cases : only one of them actually executes, so we're either going to log the errors, or post the valid activity. Hopefully, the latter is the case, and our nice new activity well appear in the feed!

#### Activities for Deleted Issues

<img src="/server/framework/atlassian-sdk/images/deleted-issue-filters.jpg" width="300" height="259" />

<img src="/server/framework/atlassian-sdk/images/deleted-issue-activity.jpg" width="300" height="205" />






































































































































































































































































