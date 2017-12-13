---
aliases:
- /server/framework/atlassian-sdk/-url-pattern-format-852129.html
- /server/framework/atlassian-sdk/-url-pattern-format-852129.md
category: devguide
confluence_id: 852129
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852129
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852129
date: '2017-12-08'
legacy_title: _URL Pattern Format
platform: server
product: atlassian-sdk
subcategory: other
title: _URL Pattern Format
---
# \_URL Pattern Format

The URL pattern format is used in Atlassian plugin types to map them to URLs. On the whole, the pattern rules are consistent with those defined in the Servlet 2.3 API. The following wildcards are supported:

-   \* matches zero or many characters, including directory slashes
-   ? matches zero or one character

###### Examples

-   `/mydir/*` matches `/mydir/myfile.xml`
-   `/*/admin/*.??ml` matches `/mydir/otherdir/admin/myfile.html`
