---
aliases:
- /server/framework/atlassian-sdk/saxparsercontextprovider-2818385.html
- /server/framework/atlassian-sdk/saxparsercontextprovider-2818385.md
category: devguide
confluence_id: 2818385
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818385
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818385
platform: server
product: atlassian-sdk
subcategory: faq
title: Saxparsercontextprovider 2818385
---
# SAXParserContextProvider

#### Symptom: The provider class, class com.sun.jersey.core.impl.provider.xml.SAXParserContextProvider, could not be instantiated

**Cause**: Your `pom.xml` file likely has a compile (not test) dependency on jersey version 1.1.2-ea  
<a href="http://jersey.576304.n2.nabble.com/Jersy-in-Jetty-Exceptions-td3481925.html" class="uri external-link">http://jersey.576304.n2.nabble.com/Jersy-in-Jetty-Exceptions-td3481925.html</a> suggests that different versions of jersey-core are involved in this problem.

**Solution**: Changing the jersey version 1.1.2 to 1.1.0 makes the error go away.

It's not clear what version of jersey is shipped with JIRA.

{{% note %}}

There is a JIRA Forum discussion about this <a href="http://forums.atlassian.com/message.jspa?messageID=257356502&amp;tstart=0" class="external-link">here</a>.

{{% /note %}}






























































