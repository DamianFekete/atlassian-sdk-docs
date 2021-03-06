---
aliases:
- /server/framework/atlassian-sdk/amps-sdk-5.0.2-release-notes-28318037.html
- /server/framework/atlassian-sdk/amps-sdk-5.0.2-release-notes-28318037.md
category: devguide
confluence_id: 28318037
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=28318037
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=28318037
date: '2017-12-08'
legacy_title: AMPS SDK 5.0.2 Release Notes
platform: server
product: atlassian-sdk
subcategory: updates
title: AMPS SDK 5.0.2 release notes
---
# AMPS SDK 5.0.2 release notes

The are no functional changes in this release - this is purely to fix the installer in certain cases.

## Fix To Installers

It is **recommended** that if you use a package manager (such as apt-get, yum, rpm, brew) that you do not use the *atlas-update* script, as otherwise you'll be updating the SDK within the same versioned directory as the current installation. This can cause the package manager to get confused with the currently installed versions, and removes your ability to easily regress to an earlier version.

-   Windows Installer Fix  
    *Will now no longer assume an existing install, and correctly pickup newly bundled Maven 3.2.1*

-   Tar Installer Fix  
    *Bundled Maven directory has been renamed, ensuring the new Maven 3.2.1 version will be used*

## Download

-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-windows" class="external-link">Windows</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-mac" class="external-link">Mac OSX</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-deb" class="external-link">Linux/Debian</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-rpm" class="external-link">Linux/RPM</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-tgz" class="external-link">Standalone</a>
