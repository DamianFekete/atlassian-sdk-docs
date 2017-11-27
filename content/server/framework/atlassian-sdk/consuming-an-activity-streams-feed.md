---
aliases:
- /server/framework/atlassian-sdk/consuming-an-activity-streams-feed-852027.html
- /server/framework/atlassian-sdk/consuming-an-activity-streams-feed-852027.md
category: devguide
confluence_id: 852027
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852027
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852027
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/activity-streams/consuming-an-activity-streams-feed
new_url: /server/framework/atlassian-sdk/consuming-an-activity-streams-feed
platform: server
product: atlassian-sdk
subcategory: learning
title: Consuming an Activity Streams feed
---
# Consuming an Activity Streams feed

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p>Activity Streams 4.0 and later.<br />
JIRA 4.4 and later.<br />
Confluence 4.0 and later.<br />
JIRA Studio</p></td>
</tr>
</tbody>
</table>

{{% note %}}

See a <a href="https://bitbucket.org/rmanalan/chrome-confluence-activity-stream/overview" class="external-link">sample project</a> that consumes Activity Streams.

{{% /note %}}

 

Activity Streams generates feeds of activity items from Atlassian application events and other sources. For example, the default Activity Streams feed contains Bamboo build results, Crucible review comments and more. This guide shows how to consume an activity stream from a <a href="http://www.atlassian.com/hosted/studio/" class="external-link">JIRA Studio</a> site.

## Getting started

Let's start with the simplest possible request for an activity stream:

``` javascript
curl https://studio.atlassian.com/activity
```

This fetches a feed of the ten most recent activities from any of the enabled JIRA Studio applications.

## Authentication

If you look closely at the feed returned by the above request, you will notice that it only contains entries that are visible to anonymous users. If you want to view restricted content, you will need to authenticate via basic authentication:

``` javascript
curl username:password https://studio.atlassian.com/activity?os_authType=basic
```

Note the `os_authType=basic` query parameter.

It is also possible to authenticate via Atlassian's Trusted Applications protocol, but that option is only useful for plugin developers who can to install their plugin in a JIRA Studio instance. For that reason, we do not give the details here.

## Filtering

Filters allow you to narrow down what type of activity items you would like to get in your feed. They can be global (for example, specifying that all items be from a certain project) or per provider (for example, only wanting to see the 'review closed' activity in Crucible). You can find out what filters are available at:  
GET <a href="https://studio.atlassian.com/rest/activity-stream/1.0/config" class="uri external-link">https://studio.atlassian.com/rest/activity-stream/1.0/config</a>.

The response might look like this:

``` javascript
{
"filters":[
{
"key":"streams",
"name":"",
"options":[
{
"key":"key",
"name":"Project",
"operators":[
{
"key":"is",
"name":"is"
},
{
"key":"not",
"name":"is not"
}
],
"type":"select",
"unique":true,
"values":{
"TEST":"TEST"
}
},
{
"key":"issue-key",
"name":"JIRA Issue Key",
"operators":[
{
"key":"is",
"name":"is"
},
{
"key":"not",
"name":"is not"
}
],
"type":"list",
"unique":true,
"values":{

}
},
{
"key":"update-date",
"name":"Update Date",
"operators":[
{
"key":"before",
"name":"is before"
},
{
"key":"after",
"name":"is after"
},
{
"key":"between",
"name":"is between"
}
],
"type":"date",
"unique":true,
"values":{

}
},
{
"key":"user",
"name":"Username",
"operators":[
{
"key":"is",
"name":"is"
},
{
"key":"not",
"name":"is not"
}
],
"type":"user",
"unique":true,
"values":{

}
}
]
},
{
"key":"issues",
"name":"JIRA",
"options":[
{
"key":"activity",
"name":"Activity",
"operators":[
{
"key":"is",
"name":"is"
},
{
"key":"not",
"name":"is not"
}
],
"type":"select",
"unique":true,
"values":{
"file:post":"Attachment added",
"comment:post":"Comment added",
"issue:close":"Issue closed",
"issue:post":"Issue created",
"issue:update":"Issue edited",
"issue:open":"Issue opened",
"issue:start":"Issue progress started",
"issue:stop":"Issue progress stopped",
"issue:reopen":"Issue reopened",
"issue:resolve":"Issue resolved",
"issue:transition":"Issue transitioned"
}
},
{
"key":"issue_type",
"name":"Issue Type",
"operators":[
{
"key":"is",
"name":"is"
},
{
"key":"not",
"name":"is not"
}
],
"type":"select",
"unique":true,
"values":{
"4":"Improvement",
"6":"Story",
"3":"Task",
"5":"Epic",
"1":"Bug",
"7":"Technical task",
"2":"New Feature"
}
}
]
},
{
"key":"wiki@confluence",
"name":"Confluence",
"options":[
{
"key":"activity",
"name":"Activity",
"operators":[
{
"key":"is",
"name":"is"
},
{
"key":"not",
"name":"is not"
}
],
"type":"select",
"unique":true,
"values":{
"file:post":"Attachment added",
"article:post":"Blog added",
"article:update":"Blog edited",
"comment:post":"Comment added",
"page:post":"Page added",
"page:update":"Page edited",
"space:post":"Space added",
"space:update":"Space edited",
"status:update":"User status updated"
}
}
]
},
{
"key":"reviews@fisheye",
"name":"Crucible",
"options":[
{
"key":"activity",
"name":"Activity",
"operators":[
{
"key":"is",
"name":"is"
},
{
"key":"not",
"name":"is not"
}
],
"type":"select",
"unique":true,
"values":{
"comment:post":"Comment added",
"review:abandon":"Review abandoned",
"review:close":"Review closed",
"review:complete":"Review completed",
"review:post":"Review created",
"review:reopen":"Review reopened",
"review:start":"Review started",
"review:summarize":"Review summarized",
"review:uncomplete":"Review uncompleted"
}
}
]
},
{
"key":"source@fisheye",
"name":"FishEye",
"options":[
{
"key":"activity",
"name":"Activity",
"operators":[
{
"key":"is",
"name":"is"
},
{
"key":"not",
"name":"is not"
}
],
"type":"select",
"unique":true,
"values":{
"changeset:push":"Changeset committed"
}
}
]
}
]
}
```

### Global Filtering

Global filters apply to all activity providers. Some examples are filters by username or date. If you would like to use a global filter on your feed, add it to your URL as a `streams` parameter. The URL has this format:

``` javascript
https://studio.atlassian.com/activity?streams=<option-key>\+<OPERATOR_KEY>\+<option-value>&streams=<option-key2>\+<OPERATOR_KEY2>\+<option-value2>...
```

For example, to filter activity by the user `johndoe`, your URL would look like this:

``` javascript
http://studio.atlassian.com/activity?streams=user+IS+johndoe
```

Note that operators in the URL must be upper case.

It is also possible to have multiple values for each filter operator. Examples of this include searching for activity belonging to a set of usernames or within a date range. For example, to filter activity within two specific dates (specified as the number of milliseconds since the epoch in GMT), your URL would look like this:

``` javascript
http://studio.atlassian.com/activity?streams=update-date+BETWEEN+1320652800000+1320998399999
```

You can get the list of available global filters by using the request described in the filtering section [above](#above), within the block of the JSON response with key `streams`.

### Per-Provider Filtering

Per-provider filters only apply to items from a particular activity provider (for example, the JIRA provider or the Crucible provider). They are used to apply criteria that only make sense in the context of a particular provider, for example asking for only 'review closed' items in Crucible. The URL for per-provider filters has this format:

``` javascript
https://studio.atlassian.com/activity?<provider-key>=<option-key>\+<OPERATOR_KEY>\+<value>&<provider-key>=<key2>\+<OPERATOR_KEY2>\+<value2>...
```

For example, to filter JIRA items so that you only get created issues, your URL would look like this:

``` javascript
http://studio.atlassian.com/activity?issues=activity+IS+issue%3Apost
```

You can get the list of available filters by using the request described in the filtering section [above](#above). Each provider has its own set of filters, which are found in the response JSON in blocks with keys other than `streams`.

### Combining Filters

You can combine the global and per-provider filters simply by using them together. For example, use the following URL to get the activity of user `admin`, and showing only created issues in JIRA:

``` javascript
http://studio.atlassian.com/activity?issues=activity+IS+issue%3Apost&streams=user+IS+admin
```

## Stream Contents

The contents of the Activity Streams items are in the <a href="http://activitystrea.ms/" class="external-link">activitystrea.ms</a> format, which is an open format for syndicating social activities around the web. You can read all the gory details of the format at the website.

Here is how an activity item appears in the Activity Streams feed:

``` xml
<entry xmlns:atlassian="http://streams.atlassian.com/syndication/general/1.0" xmlns:activity="http://activitystrea.ms/spec/1.0/">
<id>urn:uuid:66c95d7b-c54a-3849-ad40-1b105536fe97</id>
<title type="html">&lt;a href="https://studio.atlassian.com/secure/ViewProfile.jspa?name=wseliga" class="activity-item-user activity-item-author">wseliga&lt;/a> created &lt;a href="https://studio.atlassian.com/browse/JIM-22" class="issue-link">JIM-22 - Support import from Bugzilla 3.6.2&lt;/a>
</title>
<content type="html">&lt;link rel="stylesheet" type="text/css" href="https://studio.atlassian.com/s/614/11/1.0/_/download/resources/jira.webresources:global-static/wiki-renderer.css">
&lt;div class="user-content">
Issue description here &lt;/div>
</content>
<author xmlns:usr="http://streams.atlassian.com/syndication/username/1.0">
<name>wseliga</name>
<email>wseliga@example.com</email>
<uri>https://studio.atlassian.com/secure/ViewProfile.jspa?name=admin</uri>
<link xmlns:media="http://purl.org/syndication/atommedia" rel="photo" href="https://studio.atlassian.com/secure/useravatar?avatarId=10062&amp;s=16" media:height="16" media:width="16" />
<link xmlns:media="http://purl.org/syndication/atommedia" rel="photo" href="https://studio.atlassian.com/secure/useravatar?avatarId=10062&amp;s=48" media:height="48" media:width="48" />
<usr:username>admin</usr:username>
<activity:object-type>http://activitystrea.ms/schema/1.0/person</activity:object-type>
</author>
<published>2009-01-23T23:52:23.000Z</published>
<updated>2009-01-23T23:52:23.000Z</updated>
<category term="created" />
<link href="https://studio.atlassian.com/browse/JIM-22" rel="alternate" />
<link href="https://studio.atlassian.com/images/icons/bug.gif" rel="http://streams.atlassian.com/syndication/icon" />
<link href="https://studio.atlassian.com/plugins/servlet/streamscomments/issues/JIM-22" rel="http://streams.atlassian.com/syndication/reply-to" />
<link href="https://studio.atlassian.com/rest/jira-activity-stream/1.0/actions/issue-watch/JIM-22" rel="http://streams.atlassian.com/syndication/issue-watch" />
<link href="https://studio.atlassian.com/rest/jira-activity-stream/1.0/actions/issue-vote/JIM-22" rel="http://streams.atlassian.com/syndication/issue-vote" />
<generator uri="https://studio.atlassian.com" />
<atlassian:application>com.atlassian.jira</atlassian:application>
<activity:verb>http://activitystrea.ms/schema/1.0/post</activity:verb>
<activity:object>
<id>urn:uuid:66c95d7b-c54a-3849-ad40-1b105536fe97</id>
<title type="text">JIM-22</title>
<summary type="text">Support import from Bugzilla 3.6.2</summary>
<link rel="alternate" href="https://studio.atlassian.com/browse/JIM-22" />
<activity:object-type>http://streams.atlassian.com/syndication/types/issue</activity:object-type>
</activity:object>
</entry>
```




































































































































































































































































