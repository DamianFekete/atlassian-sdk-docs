---
aliases:
- /server/framework/atlassian-sdk/atlassian-plugin-sdk-ignores-customisations-for-port-or-context-path-2818650.html
- /server/framework/atlassian-sdk/atlassian-plugin-sdk-ignores-customisations-for-port-or-context-path-2818650.md
category: devguide
confluence_id: 2818650
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818650
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818650
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/atlassian-plugin-sdk-faq/atlassian-plugin-sdk-ignores-customisations-for-port-or-context-path
new_url: /server/framework/atlassian-sdk/atlassian-plugin-sdk-ignores-customisations-for-port-or-context-path
platform: server
product: atlassian-sdk
subcategory: other
title: Atlassian Plugin SDK ignores customisations for port or context path
---
# Atlassian Plugin SDK ignores customisations for port or context path

# Problem

Passing `context-path` or `http-port` parameters to `atlas-run` or `atlas-debug` doesn't change the base URL of the application instance.

# Solution

Make sure to run `atlas-clean` every time you change the runtime parameters through the SDK scripts; the scripts will cache previous installations and settings, which must be manually cleared.


















































