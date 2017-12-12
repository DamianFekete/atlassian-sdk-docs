---
aliases:
- /server/framework/atlassian-sdk/making-your-own-activity-streams-provider-852024.html
- /server/framework/atlassian-sdk/making-your-own-activity-streams-provider-852024.md
category: devguide
confluence_id: 852024
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852024
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852024
date: '2017-12-08'
guides: tutorials
legacy_title: Making your own Activity Streams Provider
platform: server
product: atlassian-sdk
subcategory: learning
title: Making your own Activity Streams provider
---
# Making your own Activity Streams provider

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Applicable:</p></td>
<td><ul>
<li>Activity Streams 4.1 and later.</li>
<li>JIRA 4.4 and later.</li>
<li>Confluence 4.0 and later.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>Level of experience:</p></td>
<td><p><strong>Intermediate</strong>. Our tutorials are classified as 'beginner', 'intermediate' and 'advanced'. This one is at 'intermediate' level. If you have never developed a plugin before, you may find this one a bit difficult.</p></td>
</tr>
<tr class="odd">
<td><p>Time to Complete:</p></td>
<td><p>1 hour</p></td>
</tr>
</tbody>
</table>

 

## Overview

Atlassian Activity Streams displays 'activities', which are items that represent recently occurring events. Example events are the creation of a Crucible review or the transition of a JIRA issue. The stream is created from the input of 'providers' that create sets of items. This screenshot shows what part of an activity stream looks like, displayed within a JIRA gadget:

![](/server/framework/atlassian-sdk/images/idog-stream-crop.png)

In the image, the review activity is created by a FishEye/Crucible provider and the items for issue creation and issue linking are created by a JIRA provider. These particular providers are included in the Activity Streams project, but providers do not have to be included in the project. External providers allow you to inject custom events into your activity streams. You can see an example external provider plugin in the <a href="https://bitbucket.org/cjerozal/external-provider-sample/overview" class="external-link">external-provider-sample project on Bitbucket</a>. Since external providers are structured in the same way as internal providers, you can look at the streams-&lt;product-name&gt;-plugin modules in the <a href="https://bitbucket.org/atlassian/atlassian-streams/commits/tag/streams-parent-5.0" class="external-link">Activity Streams source</a> for more examples. The FishEye/Crucible and JIRA providers shown above can be found in the Activity Streams source.

Users can filter the items providers create. For example, a user may want to see only items from the user 'admin'. See this screenshot:

![](/server/framework/atlassian-sdk/images/filters-crop.png)

The rest of this page shows you what you need to do to make a new provider for Activity Streams.

### Plugin Source

We encourage you to work through this tutorial. If you want to skip ahead or check your work when you are done, you can find the plugin source code on Atlassian Bitbucket. Bitbucket serves a public Git repository containing the tutorial's code. To clone the repository, issue the following command:

``` bash
$ git clone https://bitbucket.org/atlassian_tutorial/jira-external-provider-sample
```

Alternatively, you can download the source using the **get source** option here: <a href="https://bitbucket.org/atlassian_tutorial/jira-external-provider-sample" class="uri external-link">https://bitbucket.org/atlassian_tutorial/jira-external-provider-sample</a>.

## Step 1. Set up your plugin project

You can just copy and tweak the <a href="https://bitbucket.org/cjerozal/external-provider-sample/overview" class="external-link">sample project</a>, which is already set up to run Activity Streams 5.0 in an early-access milestone of JIRA 5.0. Or you may want to use the Atlassian Plugin SDK to [create a plugin skeleton](/server/framework/atlassian-sdk/creating-a-plugin-skeleton-with-the-atlassian-sdk) and then, in your sample project's pom.xml, specify a [product version](/server/framework/atlassian-sdk/activity-streams-version-matrix) containing your desired version of Activity Streams.

## Step. 2 Add the skeletons of classes for your provider

The following Activity Streams interfaces (all from package `com.atlassian.streams.spi`) are provided for you to implement.

This is the required implementation for a plugin that inserts items in Activity Streams:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>StreamsActivityProvider</p></td>
<td><p>In the getActivityFeed method, construct your feed out of StreamsEntry items. There is more detail on creating StreamsEntry items below, in the section on making a feed item <a href="#step-4-make-a-feed-item-a-streamsentry">below</a>.</p></td>
</tr>
</tbody>
</table>

Optionally, you can add these implementations as needed:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>StreamsFilterOptionProvider</p></td>
<td><p>Can provide filtering options that will be displayed to the user in the stream gadget configuration. For example, one filter implemented by the streams-jira-plugin is filtering by issue type (bug, task, etc).</p></td>
</tr>
<tr class="even">
<td><p>StreamsValidator</p></td>
<td><p>Can check that keys, such as project or space keys, submitted as user filtering options are valid. Can also be used to check permissions, for example that the requested key represents a project the user has permission to see.</p></td>
</tr>
<tr class="odd">
<td><p>StreamsKeyProvider</p></td>
<td><p>Can return a set of valid keys that a user can filter with.</p></td>
</tr>
<tr class="even">
<td><p>StreamsCommentHandler</p></td>
<td><p>Implement the postReply method to allow responses to your stream items to be made via the streams gadget. For example, the streams-confluence-plugin implements postReply to allow responses to comments or pages to be made via the gadget.</p></td>
</tr>
</tbody>
</table>

## Step 3. Add the activity-provider module to your `atlassian-plugin.xml`

It looks something like this, with the nested elements being optional based on whether you are using them or not:

``` xml
    <activity-streams-provider key="external-provider" name="External Provider" i18n-name-key="streams.external.provider.name"
                       class="com.atlassian.streams.ExternalStreamsActivityProvider">
        <filter-provider class="com.atlassian.streams.ExternalFilterOptionProvider" />
        <validator class="com.atlassian.streams.ExternalStreamsValidator" />
        <key-provider class="com.atlassian.streams.ExternalStreamsKeyProvider" />
        <comment-handler class="com.atlassian.streams.ExternalStreamsCommentHandler" />
    </activity-streams-provider>
```

 

## Step 4. Make a feed item (a StreamsEntry)

In your StreamsActivityProvider.getActivityFeed implementation, you will need to create the entries for the items you want to appear in the stream. The sample plugin does this in ExternalStreamsActivityProvider:

``` java
    /**
     * Transforms a single {@link AuditLogEntry} to a {@link StreamsEntry}.
     * @param auditLogEntry the log entry
     * @return the transformed streams entry
     */
    private StreamsEntry toStreamsEntry(final AuditLogEntry auditLogEntry)
    {
        final URI fakeUri = URI.create("http://example.com");

        StreamsEntry.ActivityObject activityObject = new StreamsEntry.ActivityObject(StreamsEntry.ActivityObject.params()
                                                                     .id("").alternateLinkUri(URI.create(""))
                                                                     .activityObjectType(upmEvent()));

        final UserProfile userProfile = userProfileAccessor.getUserProfile(auditLogEntry.getUsername());

        StreamsEntry.Renderer renderer = new StreamsEntry.Renderer()
        {
            public Html renderTitleAsHtml(StreamsEntry entry)
            {
                String userHtml = (userProfile.getProfilePageUri().isDefined()) ? "<a href=\""+userProfile.getProfilePageUri().get()+"\"  class=\"activity-item-user activity-item-author\">" + userProfile.getUsername() + "</a>" : userProfile.getUsername();
                return new Html(userHtml + " " + auditLogEntry.getTitle(i18nResolver));
            }

            public Option<Html> renderSummaryAsHtml(StreamsEntry entry)
            {
                return Option.none();
            }

            public Option<Html> renderContentAsHtml(StreamsEntry entry)
            {
                return Option.none();
            }
        };

        ActivityVerb verb = ExternalFilterOptionProvider.ExternalUPMActivityVerbs.getVerbFromEntryType(auditLogEntry.getEntryType());

        StreamsEntry streamsEntry = new StreamsEntry(StreamsEntry.params()
                .id(fakeUri)
                .postedDate(new DateTime(auditLogEntry.getDate()))
                .authors(ImmutableNonEmptyList.of(userProfile))
                .addActivityObject(activityObject)
                .verb(verb)
                .addLink(URI.create(webResourceManager.getStaticPluginResource(
                                   "com.atlassian.streams.external-provider-sample:externalProviderWebResources",
                                   "puzzle-piece.gif",
                                   UrlMode.ABSOLUTE)),
                        StreamsActivityProvider.ICON_LINK_REL,
                        none(String.class))
                .alternateLinkUri(fakeUri)
                .renderer(renderer)
                .applicationType(applicationProperties.getDisplayName()), i18nResolver);
        return streamsEntry;
    }
```

  
Here are some examples of the renderer implementation that show where method results end up in the gadget.

``` java
new StreamsEntry.Renderer()
{
    public StreamsEntry.Html renderTitleAsHtml(StreamsEntry entry)
    {
        return new StreamsEntry.Html("title");
    }

    public Option<StreamsEntry.Html> renderSummaryAsHtml(StreamsEntry entry)
    {
        return Option.some(new StreamsEntry.Html("summary"));
    }

    public Option<StreamsEntry.Html> renderContentAsHtml(StreamsEntry entry)
    {
        return Option.some(new StreamsEntry.Html("content"));
    }
}
```

``` java
new StreamsEntry.Renderer()
{
    public StreamsEntry.Html renderTitleAsHtml(StreamsEntry entry)
    {
        return new StreamsEntry.Html("title");
    }

    public Option<StreamsEntry.Html> renderSummaryAsHtml(StreamsEntry entry)
    {
        return Option.none();
    }

    public Option<StreamsEntry.Html> renderContentAsHtml(StreamsEntry entry)
    {
        return Option.some(new StreamsEntry.Html("content"));
    }
}
```

##  Step 5. Run your plugin

Use `mvn clean amps:debug -Dproduct=jira` in your plugin directory root to run JIRA with your provider plugin installed. Get an activity stream in JIRA by adding it to a dashboard with the "Activity Stream" gadget.  
The sample plugin has an activity stream loaded on the default dashboard if you log in as `admin` (password is also `admin`).

The sample plugin adds entries from the UPM (Universal Plugin Manager) audit log to the stream, in this case the installation of the Gliffy plugin to help create robot designs:

![](/server/framework/atlassian-sdk/images/sorry-bender-edited-crop.png)

Additionally, if you specify filters in your implementation of `StreamsFilterOptionProvider`, you can have your own provider-specific Activity Streams filters. The sample plugin includes filters for various kinds of plugin activity.

![](/server/framework/atlassian-sdk/images/activity-filters.png)























































































































































































































































































































