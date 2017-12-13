---
aliases:
- /server/framework/atlassian-sdk/example-settings.xml-2818713.html
- /server/framework/atlassian-sdk/example-settings.xml-2818713.md
category: devguide
confluence_id: 2818713
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818713
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818713
date: '2017-12-08'
legacy_title: Example settings.xml
platform: server
product: atlassian-sdk
subcategory: other
title: Example settings.xml
---
# Example settings.xml

{{% warning %}}

Try the new Plugin SDK

We've released a new Plugin SDK which handles almost all of this Maven tweaking for you. The SDK includes an embedded Maven installation and correct `settings.xml` that will be kept up to date as necessary. We believe it makes the plugin development process much easier. If you are using the SDK, you won't need this file. For more information, see [Developing with the Atlassian Plugin SDK](/server/framework/atlassian-sdk/developing-with-the-atlassian-plugin-sdk).

{{% /warning %}}

This is an example `settings.xml` file for Maven 2. It can be placed in your `$HOME/.m2` directory and it will apply to all maven projects that you build. If you would rather, you can make this a per-project settings by including a profile.xml in your project base directory. See <a href="http://maven.apache.org/guides/introduction/introduction-to-profiles.html" class="external-link">Maven's documentation on Build Profile Settings</a>.

If your network requires the use of an HTTP or HTTPS proxy, you'll need to <a href="http://maven.apache.org/guides/mini/guide-proxies.html" class="external-link">add those to your settings.xml</a>.

An error occurred: svn.atlassian.com. The error has been recorded.

Download <a href="https://svn.atlassian.com/svn/public/atlassian/maven2settings/settings.xml.devnet" class="external-link">here</a>

































































































































