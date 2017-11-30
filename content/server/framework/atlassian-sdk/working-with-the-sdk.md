---
aliases:
- /server/framework/atlassian-sdk/working-with-the-sdk-2818723.html
- /server/framework/atlassian-sdk/working-with-the-sdk-2818723.md
category: devguide
confluence_id: 2818723
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818723
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818723
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-with-the-sdk
new_url: /server/framework/atlassian-sdk/working-with-the-sdk
platform: server
product: atlassian-sdk
subcategory: learning
title: Working with the SDK
---
# Working with the SDK

The Atlassian Plugin SDK provides a set of shell scripts for creating, installing and building plugins for Atlassian products. This page introduces the SDK.

## Benefits of Using the Atlassian Plugin SDK

The Atlassian Plugin SDK makes your life easier by helping you do the following:

-   Build plugins for any Atlassian application with a single tool.
-   Create a plugin skeleton from a Maven archetype, specific to the Atlassian application you are developing for.
-   Download the application binaries, install your plugin and start the application.
-   Dynamically re-install your plugin after changes during development. No restart required, not even for JIRA.
-   Use dynamic bundle dependencies with the OSGi framework.
-   Write quality unit tests and integration tests.
-   Speed up the all-important code-deploy-test cycle.

And more! And we're continually improving the SDK with new and better features.

## Looking at the SDK Command Format

The SDK commands are wrappers for the underlying Maven commands. The SDK Maven plugin defines custom Maven goals for performing common plugin development tasks. If you want to run the integration tests - and only the integration tests - you can say:  
`atlas-integration-test`

Similarly, you can run the unit tests in isolation:  
`atlas-unit-test`

You can also install your plugin from the command line, instead of having to browse to the correct page and make several clicks:  
`atlas-install-plugin`  
Or:  
`atlas-cli` then `pi`

You can pass parameters on the command line in the form:

`atlas-run-standalone --product confluence`

To pass Java parameters in a command, use the `jvmargs` parameter, in the following form: 

`atlas-run-standalone --product confluence --jvmargs '-D<parameter1>=<value> -D<parameter2>=<value>`' 

## Running Behind a Corporate Firewall

If you're working behind a proxy server requiring NTLM authentication, you may find it convenient to use a local authenticating proxy server, such as `cntlm`. You can then set Java HTTP environment variables in your SDK commands to point to the proxy. For example, by using: `-Dhttp.proxyHost=localhost -Dhttp.proxyPort=3128 -Dhttps.proxyHost=localhost -Dhttps.proxyPort=3128 -Dhttp.nonProxyHosts=localhost|127.0.0.*`).

To run the SDK commands where your Java programs don't have direct access to the Internet, your atlas commands should be run with the `-DallowGoogleTracking=false` flag. This disables Google web requests during the build process.

## Supported Atlassian Applications and Default Ports

The table below shows the applications currently supported by the Atlassian Plugin SDK, the default port, and the product key for each host application.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Atlassian Application</p></th>
<th><p>Default Port</p></th>
<th><p>Product Key</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/bamboo" class="external-link">Bamboo</a></p></td>
<td><p>6990</p></td>
<td><p>bamboo</p></td>
</tr>
<tr class="even">
<td><a href="https://www.atlassian.com/software/bitbucket/server" class="external-link">Bitbucket</a></td>
<td>7990</td>
<td>bitbucket</td>
</tr>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/confluence" class="external-link">Confluence</a></p></td>
<td><p>1990</p></td>
<td><p>confluence</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.atlassian.com/software/crowd" class="external-link">Crowd</a></p></td>
<td><p>4990</p></td>
<td><p>crowd</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/crucible" class="external-link">Crucible</a></p></td>
<td><p>3990</p></td>
<td><p>fecru</p></td>
</tr>
<tr class="even">
<td><p><a href="http://www.atlassian.com/software/fisheye" class="external-link">FishEye</a></p></td>
<td><p>3990</p></td>
<td><p>fecru</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/jira" class="external-link">JIRA</a></p></td>
<td><p>2990</p></td>
<td><p>jira</p></td>
</tr>
<tr class="even">
<td><p><a href="https://developer.atlassian.com/display/DOCS/About+the+Atlassian+RefApp">RefApp</a></p></td>
<td><p>5990</p></td>
<td><p>refapp</p></td>
</tr>
<tr class="odd">
<td><p><a href="http://www.atlassian.com/software/stash" class="external-link">Stash</a></p></td>
<td><p>7990</p></td>
<td><p>stash</p></td>
</tr>
</tbody>
</table>

***Caveat for <a href="http://www.atlassian.com/software/jira" class="external-link">JIRA</a>:** Plugins developed for versions of JIRA before 4.0 are supported, but using the SDK with versions of JIRA earlier than 4.0 is not. For developing plugins for JIRA 3.13 and earlier, take a look at the [JIRA Documentation Archives](https://developer.atlassian.com/display/ARCHIVES/JIRA+Documentation+Archives).*

The SDK supports both [static](/server/framework/atlassian-sdk/static-plugin) and [dynamic](/server/framework/atlassian-sdk/dynamic-plugin) plugins. The focus is on [version 2 plugins](/server/framework/atlassian-sdk/version-1-or-version-2-plugin), as supported by the Atlassian Plugin Framework.

























































































































































































