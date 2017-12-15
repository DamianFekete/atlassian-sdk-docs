---
aliases:
- /server/framework/atlassian-sdk/-sdk-known-issues-2818471.html
- /server/framework/atlassian-sdk/-sdk-known-issues-2818471.md
category: devguide
confluence_id: 2818471
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818471
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818471
date: '2017-12-08'
legacy_title: _SDK Known Issues
platform: server
product: atlassian-sdk
subcategory: other
title: _SDK Known Issues
---
# \_SDK Known Issues

## Known Issues

### General SDK issues

-   If a plugin is in a directory with spaces in the name, the SDK commands will not work properly (<a href="https://studio.atlassian.com/browse/AMPS-126" class="external-link">AMPS-126</a>). To work around this, make sure the plugin directory has no spaces.
-   The SDK cannot deploy applications to the root context (e.g., `http://localhost:1990`) (<a href="https://studio.atlassian.com/browse/AMPS-122" class="external-link">AMPS-122</a>). To work around this, use a named context.

### Product-specific issues

None for recent versions.
