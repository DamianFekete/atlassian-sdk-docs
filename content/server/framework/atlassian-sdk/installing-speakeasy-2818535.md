---
aliases:
- /server/framework/atlassian-sdk/installing-speakeasy-2818535.html
- /server/framework/atlassian-sdk/installing-speakeasy-2818535.md
category: devguide
confluence_id: 2818535
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818535
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818535
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/speakeasy/installing-speakeasy
new_url: /server/framework/atlassian-sdk/installing-speakeasy
platform: server
product: atlassian-sdk
subcategory: learning
title: Installing Speakeasy
---
# Installing Speakeasy

## Installation

In order to start building and testing Speakeasy Extensions, you'll first need to install Speakeasy on a JIRA or Confluence instance. You can do this via the plugin manager built into JIRA and Confluence. Search for "Speakeasy Plugin" and click "Install".

#### Manual Installation

Run through the following steps to get the Speakeasy framework installed into an Atlassian application:

1.  Download and install the most recent <a href="/pages/createpage.action?spaceKey=SPEAK&amp;title=Atlassian+Plugin+SDK+Documentation" class="createlink">Plugin SDK</a> (v3.3).
2.  Start JIRA or Confluence using <a href="/pages/createpage.action?spaceKey=SPEAK&amp;title=atlas-run-standalone" class="createlink">atlas-run-standalone</a>:

    ``` bash
    atlas-run-standalone --product jira
    ```

    or

    ``` bash
    atlas-run-standalone --product confluence
    ```

    and login with username "admin", password "admin".

3.  Navigate to **Administration &gt; Plugins &gt; Available**, find Speakeasy, and click "Install".

## Configuration

The default Speakeasy configuration restricts who can develop and enable Extensions. You'll need to change these to suit your instance.

1.  Navigate to **Administration Dropdown (top right) &gt; Extensions** and click "Edit". If you do not see **Extensions**, refresh the page.
2.  Because you're developing on an instance with no sensitive data, untick the box titled 'Restrict to non-Administrators' and click "Save."

#### Extension Security For Production Servers

Speakeasy Extensions are still experimental, but if you wish to enable Speakeasy on a JIRA or Confluence server that contains non-public information, here are some notes on security implications:

Enabling an extension **allows the Extension author to execute JavaScript as you**. Because of this, by default, Administrators cannot run Extensions. You can enable Administrator access to Extensions, but we recommend only doing so if you *really* trust all your users.

A more sensible configuration might be to allow developers to to develop Extensions and internal users to view and enable them. **If your instance allows public signup, it's a bit soon to turn on Speakeasy.**

## Next Steps...

It's time to [start building a Speakeasy extension](https://developer.atlassian.com/display/SPEAK/Speakeasy+Extension+Development+Guide)!
























