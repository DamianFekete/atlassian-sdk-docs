---
aliases:
- /server/framework/atlassian-sdk/-fastdevworkflow-8945826.html
- /server/framework/atlassian-sdk/-fastdevworkflow-8945826.md
category: devguide
confluence_id: 8945826
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8945826
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8945826
date: '2017-12-08'
legacy_title: _FastDevWorkFlow
platform: server
product: atlassian-sdk
subcategory: other
title: _FastDevWorkFlow
---
# \_FastDevWorkFlow

{{% warning %}}

FastDev and atlas-cli have been deprecated. Please use [Automatic Plugin Reinstallation with QuickReload](https://developer.atlassian.com/docs/developer-tools/automatic-plugin-reinstallation-with-quickreload) instead.

{{% /warning %}}

 

To trigger the reinstallation of your plugin:

1.  Make the changes to your plugin module.
2.  Open the Developer Toolbar.  
    <img src="/server/framework/atlassian-sdk/images/fastdev1.png" width="600" />
3.  Press the FastDev icon.  
    <img src="/server/framework/atlassian-sdk/images/fastdev2.png" width="600" />  
    The system rebuilds and reloads your plugin:  
    <img src="/server/framework/atlassian-sdk/images/fastdev3.png" width="600" />

Use live reload to view real-time updates to templates and other resources:

1.  Open the Developer Toolbar.
2.  Press the live reload icon.  
    The  icon starts to revolve indicating it is on.
3.  Edit your project resources.
4.  Save your changes:  
    Back in the host application, your plugin displays any user visible changes you make.
