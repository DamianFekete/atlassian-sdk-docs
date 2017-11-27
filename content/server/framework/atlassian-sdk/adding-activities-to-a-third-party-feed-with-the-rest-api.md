---
aliases:
- /server/framework/atlassian-sdk/adding-activities-to-a-third-party-feed-with-the-rest-api-5669688.html
- /server/framework/atlassian-sdk/adding-activities-to-a-third-party-feed-with-the-rest-api-5669688.md
category: devguide
confluence_id: 5669688
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669688
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669688
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/activity-streams/adding-activities-to-a-third-party-feed-with-the-rest-api
new_url: /server/framework/atlassian-sdk/adding-activities-to-a-third-party-feed-with-the-rest-api
platform: server
product: atlassian-sdk
subcategory: learning
title: Adding Activities to a Third Party Feed with the REST API
---
# Adding Activities to a Third Party Feed with the REST API

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

 

We've added a new feature to Activity Streams that allows anyone to add activities to an Atlassian application's feed via a simple REST api. Activities added via this api can be associated with projects, users, and other targets such as JIRA issues, Confluence spaces, and Bamboo builds. For example, an activity associated with a JIRA issue will appear in the Activity tab on the View Issue page.

We'll walk through the feature, starting with the simplest possible example.

### Adding a simple activity to the feed

Let's assume the application is running at `http://localhost:3990/jira`. To add an activity to the feed, POST a JSON document to `http://localhost:3990/jira/rest/activities/1.0/`. You need to authenticate (e.g. with basic auth), and the content-type header should be set to `application/vnd.atl.streams.thirdparty+json`. The document must adhere to the <a href="http://activitystrea.ms/specs/json/1.0/" class="external-link">activitystrea.ms JSON</a> specification. There are two deviations from the specification:

1.  The "generator" element is mandatory, and must have a displayName and id (those are all optional in the spec); the reason for this is explained below.
2.  The "published" property is optional, and defaults to the current date/time if omitted (it is mandatory in the spec).

Here's the simplest possible document that displays something interesting:

**Minimal example**

``` javascript
{
  "actor": {
    "id": "user"
  },
  "generator" : {
    "id": "http://www.bitbucket.org",
    "displayName" : "Bitbucket"
  },
  "id" : "http://bitbucket.org/jkodumal",
  "title" : "Merge commit '68041056c69461d93958197cdb401a9ba4e5a0a4' into HEAD",
  "content" : "<blockquote>Compile with '-unchecked -deprecation' and clean up what we found.</blockquote>"
}
```

And here's how this is displayed in the stream:

![](/server/framework/atlassian-sdk/images/entry-skitched1.jpg)

Here's a brief explanation of the meaning of the fields in the document:

1.  The "actor" is the person that performed the activity. If you set the "id" of the "actor" to a valid username on the Atlassian application, it'll automatically be associated with that user. The avatar image and profile link will be set up automatically, and the activity will appear in that user's activity stream on their profile page. Anyone with a filter set up for that username will also see the activity.
2.  The "generator" is the identity of the external system where the activity was generated. It might be a remote code hosting service like Bitbucket or GitHub, or a help desk system. That system should always add content with the same "id" and "displayName" for the generator. Users can filter their streams by generator. For example, they can choose to hide content from Bitbucket. This is why we've made the generator mandatory--- otherwise, we wouldn't be able to classify these entries.
3.  The "id" of the activity should be a unique identifier for the activity. It's (currently) not displayed in the feed, but it is mandatory.
4.  The "title" appears in the activity entry. It can be arbitrary HTML, but it will be sanitized. Certain tags will be stripped out.
5.  The "content" appears below the "title" in the activity entry. It is also sanitized HTML.

You can post this document with any http client. For simplicity, here's how you might do it using `curl`, a widely available command line tool (assume that the above document was saved as "sample.json", and that admin / admin is a valid username / password):

``` bash
curl -u admin:admin --data-binary @sample.json -H "Content-Type:application/vnd.atl.streams.thirdparty+json" http://localhost:3990/jira/rest/activities/1.0/
```

<a href="http://code.google.com/p/rest-client/" class="external-link">RESTClient</a> is another easy to use tool for testing out this feature.

### Deleting an activity from the feed

When you successfully post an activity, you'll receive a 201 CREATED response, along with a copy of the document containing additional information. The new information includes a "links" map containing a URL with a "self" link. That's the URL of the activity you just posted. If you do a GET on that URL, you'll fetch a copy of that document. If you do a DELETE, you'll remove it from the system.

You probably only want to delete activities for testing purposes. On production instances, it's probably best to keep activities indefinitely.

### A more extensive example

Let's show a more complete version of the same activity to demonstrate some additional capabilities:

**A complete example**

``` javascript
{
  "published": "2011-02-10T15:04:55.000Z",
  "actor": {
    "id": "jko",
    "image": {
      "url": "http://www.gravatar.com/avatar/00a08e3ffde37612301a0d65824cb6cb?s=48",
      "width": 48,
      "height": 48
    }
  },
  "icon" : {
    "url": "https://bitbucket.org/favicon.ico",
    "width" : "16",
    "height" : "16"
  },
  "object" : {
    "id": "csid19021043803344554",
    "objectType": "changeset",
    "url" : "https://bitbucket.org/scalatra/scalatra/commit/a74e68d7de52f98c1ea4f3c48fd5bbec70fa507c"
  },
  "generator" : {
    "id": "http://www.bitbucket.org",
    "displayName" : "Bitbucket"
  },
  "target": {
    "url": "ONE-1"
  },
  "id" : "http://bitbucket.org/jko/",
  "title" : "Merge commit '68041056c69461d93958197cdb401a9ba4e5a0a4' into HEAD",
  "content" : "<blockquote>Compile with '-unchecked -deprecation' and clean up what we found.</blockquote>"
}
```

We've used the same title and content, but we've added a few additional fields to the document. Let's walk through the changes.

1.  We've specified the "published" date. You can post activities that occur at a specific time in the remote application via this field. Use the date format above.
2.  We've added an "image" property to the "actor", which includes a URL, width, and height. If the user "id" ("jko" in this case) couldn't be mapped to a user in the application, we'll display that image for the avatar icon.
3.  There's also an "icon" associated with the activity itself. This will be displayed to the left of the date in the entry. It helps indicate the identity of the generator (ie, lets users know that this activity came from Bitbucket). Use a 16x16 image for this--- a favicon works well.
4.  We've added an "object" to the activity. It indicates the kind of activity that was performed, and provides a URL for that activity. It otherwise isn't displayed in the feed, but providing an object is a good idea--- in the future we may use the object for filtering (ie, allow users to filter by "changesets" or "status updates" or the like).
5.  There's now a "target". Generically speaking, the target is something that the activity is associated with. If the target's "url" is set to a JIRA issue key (it can be the full URL, or just the key), we'll associate the activity with that issue. That means that the activity will show up on the Activity tab on the View Issue page, and anyone filtering for activities related to that specific issue will see this activity. You can also associate with a project by naming the project key.

![](/server/framework/atlassian-sdk/images/entry-skitched2.jpg)

### Best practices for formatting entries

We recommend adhering to the following guidelines in order to make your activity entry appear consistent with the "native" activity feed:

-   The title of your entry should follow the pattern "Actor verbed object". For example : "Chris Okasaki committed changeset" or "Simon Jones posted a blog entry".
-   Linked entities (issue keys, usernames, etc.) should be mentioned in the title and content. We automatically add hyperlinks to issue keys and full names (not usernames) for users.
-   Use a 16x16 color image for the activity icon - do not omit the icon,






































































































































































































































































