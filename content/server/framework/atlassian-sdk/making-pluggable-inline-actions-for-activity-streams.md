---
aliases:
- /server/framework/atlassian-sdk/making-pluggable-inline-actions-for-activity-streams-852073.html
- /server/framework/atlassian-sdk/making-pluggable-inline-actions-for-activity-streams-852073.md
category: devguide
confluence_id: 852073
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852073
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852073
date: '2017-12-08'
guides: tutorials
legacy_title: Making Pluggable Inline Actions for Activity Streams
platform: server
product: atlassian-sdk
subcategory: learning
title: Making pluggable inline actions for Activity Streams
---
# Making pluggable inline actions for Activity Streams

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
Confluence 4.0 and later.</p></td>
</tr>
</tbody>
</table>

 

Activity streams are great. They funnel lots of information into an easily accessible view to allow users an easy way to keep up with the latest activities. They are even better if they allow the users to act on the items they see, right there on the stream itself.

As a plugin developer, you can use the Atlassian Activity Streams 4 API to add your own inline actions whenever you please. The API is entirely in JavaScript.

The instructions below show you how to write your own pluggable action for Atlassian Activity Streams.

 

{{% note %}}

A sample pluggable inline action plugin can be found <a href="https://bitbucket.org/atlassian_tutorial/inline-action-sample-plugin" class="external-link">here</a>.

{{% /note %}}

## Prerequisites

You need to know a little bit about the Atlassian Plugin SDK and a small amount of experience in writing plugins.

## Step 1. Create your plugin skeleton

Follow the Atlassian plugin SDK guide to [create a plugin skeleton](https://developer.atlassian.com/docs/common-coding-tasks/development-cycle/creating-a-plugin-skeleton-with-the-atlassian-sdk).

## Step 2. Implement your JavaScript function

Your pluggable action should be implemented as an anonymous function. This function will be invoked upon Activity Streams loading the file.

The most important part is calling `ActivityStreams.registerAction(type, element, sortBy)`. This function has the potential to add a link (or any other arbitrary HTML) to the bottom of Activity Streams entries.

For example, to add a 'Trigger Build' inline action, you could implement the following `build-trigger.js`:

``` javascript
/**
 * Registers a "Trigger build" action against any feed items with a "build" type.
 *
 * Creates a link which triggers a build for the specified plan.
 */
(function() {

    /**
     * Builds a "Trigger" link that triggers the action
     *
     * @method buildTriggerBuildLink
     * @param {Object} feedItem Object representing the activity item
     * @return {HTMLElement}
     */
    function buildTriggerBuildLink(feedItem) {
        ...
    }

    // Registers the trigger action for any builds in the feed
    ActivityStreams.registerAction('job', buildTriggerBuildLink, 5);
})();
```

`registerAction` takes three parameters:

-   **type**: the type of streams entries to attach to. The following types are supported for the given applications and activity providers:
    -   JIRA: `issue`, `comment`, and `file` (attachment)
    -   Confluence: `page`, `article` (blog), `comment`, `file` (attachment), `space`, `personal-space`, and `status` (user status)
    -   FishEye: `changeset`
    -   Crucible: `review` and `comment`
    -   Bamboo: `job`
    -   [Custom Activity Streams Providers](https://developer.atlassian.com/display/STREAMS/Making+your+own+Activity+Streams+Provider): the `activity:object-type` belonging to your `entry`'s `activity:object`.
-   **element**: the function that will produce a hyperlink or other HTML. This function will take a `feedItem` parameter containing information about the specific Activity Streams entry.
-   **sortBy**: a weight used to sort the action with other inline actions.

For the 'Trigger Build' example, we only want to register this action towards `feedItem` items of type `build`. Now that you can add hyperlinks to build entries, let's hook up the link to actually do something.

``` javascript
...

    /**
     * Adds a Bamboo build to the queue.
     *
     * @method addBuildToQueue
     * @param {Event} e Event object
     */
    function addBuildToQueue(e) {
        var activityItem = AJS.$(e.target).closest('div.activity-item'),
            triggerUrl;

        if (e.data && e.data.feedItem) {
            triggerUrl = e.data.feedItem.links['http://streams.atlassian.com/syndication/build-trigger'];
        } else {
            return;
        }

        e.preventDefault();

        AJS.$.ajax({
            type : 'POST',
            url : ActivityStreams.InlineActions.proxy(triggerUrl)
        });
    }

    /**
     * Builds a "Trigger" link that triggers the action
     *
     * @method buildTriggerBuildLink
     * @param {Object} feedItem Object representing the activity item
     * @return {HTMLElement}
     */
    function buildTriggerBuildLink(feedItem) {
        //if no build-trigger link exists in the feed item, do not bind the entry to a trigger handler
        if (!feedItem.links['http://streams.atlassian.com/syndication/build-trigger']) {
            return;
        }

        var link = AJS.$('<a href="#" class="activity-item-build-trigger-link"></a>')
                .text('Trigger Build')
                .bind('click', {feedItem: feedItem}, addBuildToQueue);

        return link;
    }

    ...
```

The above code adds a `Trigger Build` link to any `build` entry specified as being capable of executing builds. For this example, the Bamboo server determines whether or not a build is capable of being triggered (disabled builds cannot be triggered) and communicates this capability by including the link in the `feedItem`. This example is still as minimal as possible. It does not yet i18n text nor offer any user-visible feedback.

When the newly created link is clicked, the `addBuildToQueue()` event handler is executed, POSTing an AJAX call to the Bamboo REST API.

You probably noticed that instead of hitting `triggerUrl` directly, our POST hits `ActivityStreams.InlineActions.proxy(triggerUrl)`. Since this POST request originates from a JIRA/Confluence instance to a Bamboo instance, we cannot make a cross-machine request from JavaScript. Instead, we will need to proxy this URL to ensure the request's success. GET, POST, and PUT types are supported when proxying.

## Step 3. Register your JavaScript file as a pluggable action

This part is easy. Activity Streams 4.0 defines a new plugin module descriptor to use via the `<streams-action-handlers>` tag.

Have your JavaScript all ready to go? In order to register it as an Activity Streams action handler, all you need to do is define it as a resource within a `<streams-action-handlers>` module.

``` xml
<atlassian-plugin key="com.atlassian.streams.bamboo.inlineactions" name="Bamboo Streams Inline Actions Plugin" pluginsVersion="2">

    ...

    <streams-action-handlers key="actionHandlers">
        <resource type="download" name="build-trigger.js" location="/js/inline-actions/build-trigger.js"/>
    </streams-action-handlers>

    ...

</atlassian-plugin>
```

That's it! Activity Streams will take care of the rest for you.

## Step 4. Install your plugin on an Activity Streams server

Once you have your plugin packaged into a JAR, install it on **your application containing the Activity Streams gadget** (currently either JIRA or Confluence). You do not need to install it on the application involved in the action handle (in the above example, Bamboo).

The logic here is that we want to restrict our applications to running JavaScript installed on their own servers. It would not be secure for JIRA to run JavaScript downloaded from a remote Bamboo server.

## Enhancing your pluggable action

{{% tip %}}

Congratulations! You have a functioning pluggable action for your Activity Streams!

Now let's jazz it up a bit and make it better.

{{% /tip %}}

### Step 5. Add internationalisation (i18n)

You will probably want to internationalise your plugin. And it is easy enough to do, so why not?

First, create your `i18n.properties` file. Let's start with just a single i18n property for the hyperlink label.

``` bash
streams.bamboo.action.trigger.title=Run
```

Now register your `i18n.properties` file with your plugin.

``` xml
<atlassian-plugin key="com.atlassian.streams.bamboo.inlineactions" name="Bamboo Streams Inline Actions Plugin" pluginsVersion="2">

    ...

    <resource type="i18n" name="bamboo-actions-i18n" location="com.atlassian.streams.bamboo.inline-actions.i18n"/>

    ...

</atlassian-plugin>
```

To make the internationalized properties available to your JavaScript, you'll want to use Activity Streams' support to transform the properties into a format accessible from your JavaScript. Again in your `atlassian-plugin.xml`, let's add to your existing `streams-action-handlers`. The new resource name and location (in this case, `streams.bamboo.action.i18n.js` and `/js/inline-actions/streams.bamboo.i18n.js` should have the filename in the form of `<i18n-prefix-pattern>.i18n.js`. For this example, all of this inline action's internationalization properties will begin with `streams.bamboo.action`.

``` xml
<atlassian-plugin key="com.atlassian.streams.bamboo.inlineactions" name="Bamboo Streams Inline Actions Plugin" pluginsVersion="2">

    ...

    <streams-action-handlers key="actionHandlers">
        <transformation extension="i18n.js">
            <transformer key="action-i18n-transformer" />
        </transformation>

        <resource type="download" name="streams.bamboo.action.i18n.js" location="/js/inline-actions/streams.bamboo.action.i18n.js"/>
        <resource type="download" name="build-trigger.js" location="/js/inline-actions/build-trigger.js"/>
    </streams-action-handlers>

    ...

</atlassian-plugin>
```

Now we're ready to use the i18n properties in your JavaScript. Activity Streams 4.0 has implemented a utility method `ActivityStreams.i18n.get(key)` to access internationalized values. Values are fetched from the dynamic JavaScript resource defined in the previous step and cached for future accessibility.

``` javascript
function buildTriggerBuildLink(feedItem) {

        ...

        var link = AJS.$('<a href="#" class="activity-item-build-trigger-link"></a>')
                .text(ActivityStreams.i18n.get('streams.bamboo.action.trigger.title'))
                .bind('click', {feedItem: feedItem}, addBuildToQueue);

        ...
    }
```

***Note:*** Because the Atlassian plugins system will be looking up a JavaScript file which does not exist (in this case, `/js/inline-actions/build-trigger.js`), you will probably want to create an empty file at that location. While this is not a required step, it will avoid any related warnings being output to the system logs.

### Step 6. Provide feedback for success and failure

You will probably want to provide some sort of feedback to the user specifying whether or not your inline action was successful in completing its task. For this task we provide a utility function, `statusMessage(activityItem, message, type, additionalEvents)`.

![](/server/framework/atlassian-sdk/images/screen-shot-2011-01-31-at-9.24.13-am.png) ![](/server/framework/atlassian-sdk/images/screen-shot-2011-01-31-at-9.25.46-am.png)  
This method takes the following parameters:

-   **activityItem**: the `activity-item` `<div>` used by your action handler
-   **message**: a textual message to display in the status message
-   **type**: type of message to display (any of the "classes" supported by <a href="/pages/createpage.action?spaceKey=AUI&amp;title=Messages" class="createlink">AUI Messages</a>).
-   **additionalEvents**: an optional callback function to invoke upon the status message fading out.

Atlassian Gadgets have some built-in ajax error handling, so if you're issuing an ajax request and using `statusMessage()`, you'll want to disable the global error handling by setting `global` to `false` in the jQuery ajax method.

Now let's add some status messages to our Trigger Build action.

``` javascript
function addBuildToQueue(e) {
        var activityItem = AJS.$(e.target).closest('div.activity-item'),
            triggerUrl;

        if (e.data && e.data.feedItem) {
            triggerUrl = e.data.feedItem.links['http://streams.atlassian.com/syndication/build-trigger'];
        } else {
            ActivityStreams.InlineActions.statusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.general'), 'error');
            return;
        }

        e.preventDefault();

        AJS.$.ajax({
            type : 'POST',
            url : ActivityStreams.InlineActions.proxy(triggerUrl),
            global: false,
            success : function() {
                ActivityStreams.InlineActions.statusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.success'), 'info');
            },
            error : function(request) {
                if (request.rc == 401) {
                    // User triggering build likely does not exist on Bamboo instance,
                    // or trusted apps configuration is not properly set up.
                    ActivityStreams.InlineActions.statusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.authentication'), 'error');
                } else {
                    ActivityStreams.InlineActions.statusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.general'), 'error');
                }
            }
        });
    }
```

If the POST request completes successfully, `statusMessage()` will be invoked with a type of `info`. Otherwise, in the case of an error, `statusMessage()` will be invoked with a type of `failure`.

Let's go even farther now and say that we want the inline action link to disable upon clicking, and then re-enable when the status message fades out. We can add this functionality with the optional `additionalEvents` callback parameter. For this example, we will add a hidden `<span>` label with identical text next to the trigger link, and will toggle both of their visibilities based on the action's current state. When the action is first invoked, `hideTriggerLink()` will hide the link and display the `<span>` label. When the action's status message fades out, `showTriggerLink()` will redisplay the link and hide the `<span>` label.

``` javascript
function addBuildToQueue(e) {

        ...

        e.preventDefault();
        hideTriggerLink(activityItem);

        AJS.$.ajax({
            type : 'POST',
            url : ActivityStreams.InlineActions.proxy(triggerUrl),
            global: false,
            success : function() {
                ActivityStreams.InlineActions.infoStatusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.success'), function() {
                    showTriggerLink(activityItem);
                });
            },
            error : function(request) {
                if (request.rc == 401) {
                    // User triggering build likely does not exist on Bamboo instance,
                    // or trusted apps configuration is not properly set up.
                    ActivityStreams.InlineActions.errorStatusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.authentication'), function() {
                        showTriggerLink(activityItem);
                    });
                } else {
                    ActivityStreams.InlineActions.errorStatusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.general'), function() {
                        showTriggerLink(activityItem);
                    });
                }
            }
        });
    }

    /**
     * Hide the trigger link, showing the non-hyperlinked label instead.
     *
     * @method hideTriggerLink
     * @param {Object} activityItem the .activity-item div
     */
    function hideTriggerLink(activityItem) {
        activityItem.find('a.activity-item-build-trigger-link').addClass('hidden');
        activityItem.find('span.activity-item-build-trigger-label').removeClass('hidden');
    }

    /**
     * Show the trigger link, hiding the non-hyperlinked label in the process.
     *
     * @method showTriggerLink
     * @param {Object} activityItem the .activity-item div
     */
    function showTriggerLink(activityItem) {
        activityItem.find('a.activity-item-build-trigger-link').removeClass('hidden');
        activityItem.find('span.activity-item-build-trigger-label').addClass('hidden');
    }

    function buildTriggerBuildLink(feedItem) {

        ...

        var link = AJS.$('<a href="#" class="activity-item-build-trigger-link"></a>')
                .text(ActivityStreams.i18n.get('streams.bamboo.action.trigger.title'))
                .bind('click', {feedItem: feedItem}, addBuildToQueue),
            label = AJS.$('<span class="activity-item-build-trigger-label hidden"></span>')
                .text(ActivityStreams.i18n.get('streams.bamboo.action.trigger.title'));

        return link.add(label);
    }

    ...
```

### Step 7. Provide feedback while waiting for an asynchronous request

Even with status messages to indicate successful or failed actions, users get antsy when they initiate an action and don't get immediate visual feedback. So it's a good idea to let the user know that something is happening while waiting for an asynchronous (ajax) request to return. We've provided a mechanism to easily hide and show a throbber to indicate that something is happening.

To hide and show the throbber, simply trigger the `beginInlineAction` and `completeInlineAction` events (respectively). These can be triggered on any element in the dom, though it's recommended that you trigger them on the target element for your pluggable action.

We recommend using the `beforeSend` and `complete` callbacks jQuery provides in its `ajax` function, but the events can be triggered at any time you feel is appropriate:

``` javascript
function addBuildToQueue(e) {
        var target = AJS.$(e.target),
            activityItem = target.closest('div.activity-item'),
            triggerUrl;

        if (e.data && e.data.feedItem) {
            triggerUrl = e.data.feedItem.links['http://streams.atlassian.com/syndication/build-trigger'];
        } else {
            ActivityStreams.InlineActions.statusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.general'), 'error');
            return;
        }

        e.preventDefault();

        AJS.$.ajax({
            type : 'POST',
            url : ActivityStreams.InlineActions.proxy(triggerUrl),
            global: false,
            beforeSend: function() {
                target.trigger('beginInlineAction');
            },
            complete: function() {
                target.trigger('completeInlineAction');
            }
        });
    }
```

## Final Result

{{% tip %}}

You can also check out the <a href="https://studio.atlassian.com/source/browse/STRM/branches/activity-stream-4.0.x/bamboo-inline-actions-plugin" class="external-link">source code</a> for the example used in this tutorial.

{{% /tip %}}

After completing all of the above steps and enhancements, we have a fully functional pluggable inline action for our Activity Streams! Our final `build-trigger.js` is as follows:

``` javascript
/**
 * Registers a "Trigger build" action against any feed items with a "build" type.
 *
 * Creates a link which triggers a build for the specified plan.
 */
(function() {

    /**
     * Adds a Bamboo build to the queue.
     *
     * @method addBuildToQueue
     * @param {Event} e Event object
     */
    function addBuildToQueue(e) {
        var target = AJS.$(e.target),
            activityItem = target.closest('div.activity-item'),
            triggerUrl;

        if (e.data && e.data.feedItem) {
            triggerUrl = e.data.feedItem.links['http://streams.atlassian.com/syndication/build-trigger'];
        } else {
            ActivityStreams.InlineActions.errorStatusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.general'));
            return;
        }

        e.preventDefault();
        hideTriggerLink(activityItem);

        AJS.$.ajax({
            type : 'POST',
            url : ActivityStreams.InlineActions.proxy(triggerUrl),
            global: false,
            beforeSend: function() {
                target.trigger('beginInlineAction');
            },
            complete: function() {
                target.trigger('completeInlineAction');
            },
            success : function() {
                ActivityStreams.InlineActions.infoStatusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.success'), function() {
                    showTriggerLink(activityItem);
                });
            },
            error : function(request) {
                if (request.rc == 401) {
                    // User triggering build likely does not exist on Bamboo instance,
                    // or trusted apps configuration is not properly set up.
                    ActivityStreams.InlineActions.errorStatusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.authentication'), function() {
                        showTriggerLink(activityItem);
                    });
                } else {
                    ActivityStreams.InlineActions.errorStatusMessage(activityItem, ActivityStreams.i18n.get('streams.bamboo.action.trigger.failure.general'), function() {
                        showTriggerLink(activityItem);
                    });
                }
            }
        });
    }

    /**
     * Hide the trigger link, showing the non-hyperlinked label instead.
     *
     * @method hideTriggerLink
     * @param {Object} activityItem the .activity-item div
     */
    function hideTriggerLink(activityItem) {
        activityItem.find('a.activity-item-build-trigger-link').addClass('hidden');
        activityItem.find('span.activity-item-build-trigger-label').removeClass('hidden');
    }

    /**
     * Show the trigger link, hiding the non-hyperlinked label in the process.
     *
     * @method showTriggerLink
     * @param {Object} activityItem the .activity-item div
     */
    function showTriggerLink(activityItem) {
        activityItem.find('a.activity-item-build-trigger-link').removeClass('hidden');
        activityItem.find('span.activity-item-build-trigger-label').addClass('hidden');
    }

    /**
     * Builds a "Trigger" link that triggers the action
     *
     * @method buildTriggerBuildLink
     * @param {Object} feedItem Object representing the activity item
     * @return {HTMLElement}
     */
    function buildTriggerBuildLink(feedItem) {
        //if no build-trigger link exists in the feed item, do not bind the entry to a trigger handler
        if (!feedItem.links['http://streams.atlassian.com/syndication/build-trigger']) {
            return;
        }

        var link = AJS.$('<a href="#" class="activity-item-build-trigger-link"></a>')
                .text(ActivityStreams.i18n.get('streams.bamboo.action.trigger.title'))
                .bind('click', {feedItem: feedItem}, addBuildToQueue),
            label = AJS.$('<span class="activity-item-build-trigger-label hidden"></span>')
                .text(ActivityStreams.i18n.get('streams.bamboo.action.trigger.title'));

        return link.add(label);
    }

    // Registers the trigger action for any builds in the feed
    ActivityStreams.registerAction('job', buildTriggerBuildLink, 5);
})();
```

And our final `atlassian-plugin.xml` is:

``` xml
<atlassian-plugin key="com.atlassian.streams.bamboo.inlineactions" name="Bamboo Streams Inline Actions Plugin" pluginsVersion="2">
    <plugin-info>
        <description>Bamboo Streams Inline Actions Plugin</description>
        <version>${project.version}</version>
        <vendor name="Atlassian Software Systems Pty Ltd" url="http://www.atlassian.com/"/>
    </plugin-info>

    <streams-action-handlers key="actionHandlers">
        <transformation extension="i18n.js">
            <transformer key="action-i18n-transformer" />
        </transformation>

        <resource type="download" name="streams.bamboo.action.i18n.js" location="/js/inline-actions/streams.bamboo.action.i18n.js"/>
        <resource type="download" name="build-trigger.js" location="/js/inline-actions/build-trigger.js"/>
    </streams-action-handlers>

    <resource type="i18n" name="bamboo-actions-i18n" location="com.atlassian.streams.bamboo.inline-actions.i18n"/>

</atlassian-plugin>
```




































































































































































































































