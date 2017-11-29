---
title: Amps Sdk 5.0.0 Release Notes 28317040
aliases:
    - /server/framework/atlassian-sdk/amps-sdk-5.0.0-release-notes-28317040.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=28317040
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=28317040
confluence_id: 28317040
platform:
product:
category:
subcategory:
---
# AMPS SDK 5.0.0 release notes

We've released AMPS 5.0.0 with a major version bump chiefly to indicate the major change in Maven support, rather than any significant functional changes.

## Maven Support Changes

-   Maven 3.1 & 3.2 Support  
    *The AMPS SDK now comes bundled with **Maven 3.2.1**, but will also work with Maven 3.1.x*
-   Dropping Maven 2.x Support  
    *Now that Maven 2 is <a href="http://maven.apache.org/maven-2.x-eol.html" class="external-link">end-of-life</a>, we are also dropping support for this version of Maven in the AMPS SDK*
-   Skipping Maven 3.0.x Support  
    *There are some serious bugs in the reactor in Maven 3.0, which have subsequently been fixed in version 3.1. We are thus skipping support for Maven 3.0.x*

## Other Minor Changes

-   Atlas CLI upgraded to use Maven CLI Plugin 1.0.11  
    *No longer shows 'maven2' at the command, allows reverse history search*

-   <a href="https://ecosystem.atlassian.net/browse/AMPS-1136" class="external-link">AMPS-1136</a> Stash home/shared migration  
    *Supports Stash 3.1 directory locations*

-   <a href="https://ecosystem.atlassian.net/browse/AMPS-1135" class="external-link">AMPS-1135</a> Upgrade the version of Tomcat for the container tomcat8x  
    *Now uses version 8.0.5 *

## Download

-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-windows" class="external-link">Windows</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-mac" class="external-link">Mac OSX</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-deb" class="external-link">Linux/Debian</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-rpm" class="external-link">Linux/RPM</a>
-   <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-tgz" class="external-link">Standalone</a>

 

 

 

























