---
aliases:
- /server/framework/atlassian-sdk/amps-sdk-5.0.3-release-notes-28868823.html
- /server/framework/atlassian-sdk/amps-sdk-5.0.3-release-notes-28868823.md
category: devguide
confluence_id: 28868823
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=28868823
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=28868823
date: '2017-12-08'
legacy_title: AMPS SDK 5.0.3 Release Notes
platform: server
product: atlassian-sdk
subcategory: updates
title: AMPS SDK 5.0.3 release notes
---
# AMPS SDK 5.0.3 release notes

## Fix For AMPS Dispatcher

AMPS 5.0 introduced an error with dispatched Maven goals failing to pickup plugin config. This fix means that atlas-run and atlas-debug will now correctly find configuration specified in the project POM.

## Package Manager vs atlas-update

It is **recommended** that if you use a package manager (such as apt-get, yum, rpm, brew) that you do not use the _atlas-update_ script, as otherwise you'll be updating the SDK within the same versioned directory as the current installation. This can cause the package manager to get confused with the currently installed versions, and removes your ability to easily regress to an earlier version.

## Download

-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-windows" class="external-link">Windows</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-mac" class="external-link">Mac OSX</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-deb" class="external-link">Linux/Debian</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-rpm" class="external-link">Linux/RPM</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-tgz" class="external-link">Standalone</a>
