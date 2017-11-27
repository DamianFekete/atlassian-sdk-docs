---
aliases:
- /server/framework/atlassian-sdk/activity-streams-852150.html
- /server/framework/atlassian-sdk/activity-streams-852150.md
category: devguide
confluence_id: 852150
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852150
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852150
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/activity-streams
new_url: /server/framework/atlassian-sdk/activity-streams
platform: server
product: atlassian-sdk
subcategory: learning
title: Activity Streams
---
# Activity Streams

This information is for developers who want to interact programmatically with Atlassian activity streams. The documentation applies to **Activity Streams 4 and later**. Please refer to the [version matrix](/server/framework/atlassian-sdk/activity-streams-version-matrix) to see which version of Activity Streams is bundled with each product.

## What are Activity Streams?

An activity stream is a list of events, displayed to a user in an attractive and interactive interface. They are usually recent activities by the current user and other people using the same social site(s) or system(s).

An example is the <a href="https://confluence.atlassian.com/display/JIRA/Adding+the+Activity+Stream+Gadget" class="external-link">Activity Stream gadget</a> used on JIRA dashboards.

<img src="/server/framework/atlassian-sdk/images/activitystreamgadget-display.png" class="confluence-thumbnail" />

## Coding with Activity Streams

These are the ways you can interact with Activity Streams in Atlassian products.

### Consuming an Activity Streams Feed

Activity Streams generates feeds of activity items from Atlassian application events and other sources. For example, the default Activity Streams feed contains Bamboo build results, Crucible review comments and more. If you wish to consume an activity stream from an Atlassian application, [read on](/server/framework/atlassian-sdk/consuming-an-activity-streams-feed).

### Making Pluggable Inline Actions for an Activity Stream

Activity streams funnel lots of information into an easily accessible view, so that people can easily keep track of what's happening. The next step is to allow people to act on the items they see, right there on the stream itself. As a plugin developer, you can use the Atlassian Activity Streams API to add your own inline actions whenever you please. [More...](/server/framework/atlassian-sdk/making-pluggable-inline-actions-for-activity-streams)

### Adding Activities to a Third Party Feed

Activity Streams includes a lightweight API that allows plugins to add activities to the activity stream in an Atlassian application. This API doesn't give you as much power as building a fully-fledged activity streams provider (described below), but it's extremely easy to use. See how to add activities to a third party feed using the [Java API](/server/framework/atlassian-sdk/adding-activities-to-a-third-party-feed-with-the-java-api) or the [REST API](/server/framework/atlassian-sdk/adding-activities-to-a-third-party-feed-with-the-rest-api).

### Making your own Activity Streams Provider

An activity stream is created from the input of 'providers' that create sets of items for inclusion in the stream. You can create your own external provider and inject custom events into the activity streams. See how to [build a provider plugin](/server/framework/atlassian-sdk/making-your-own-activity-streams-provider).









































































































































































































































































