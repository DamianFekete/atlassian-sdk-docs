---
aliases:
- /server/framework/atlassian-sdk/maven-is-unable-to-download-the-artifact-from-any-repository-2818710.html
- /server/framework/atlassian-sdk/maven-is-unable-to-download-the-artifact-from-any-repository-2818710.md
category: devguide
confluence_id: 2818710
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818710
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818710
learning: faq
legacy_url: https://developer.atlassian.com/docs/faq/atlassian-plugin-sdk-faq/maven-is-unable-to-download-the-artifact-from-any-repository
new_url: /server/framework/atlassian-sdk/maven-is-unable-to-download-the-artifact-from-any-repository
platform: server
product: atlassian-sdk
subcategory: other
title: Maven is unable to download the artifact from any repository
---
# Maven is unable to download the artifact from any repository

You may find that Maven complains it is "Unable to download the artifact from any repository."

We use the Maven project's <a href="http://maven.apache.org/archiva/" class="external-link">Archiva Maven Proxy</a> to act as our Maven repository. Sometimes, however, artifact downloads fail because of Archiva's instabilities. If you run into messages like this, sometimes a second attempt will succeed in downloading the artifact. If it doesn't work after a few times, then the artifact may be truly missing. You can <a href="http://maven.atlassian.com" class="external-link">search our Archiva</a> to confirm this.















































