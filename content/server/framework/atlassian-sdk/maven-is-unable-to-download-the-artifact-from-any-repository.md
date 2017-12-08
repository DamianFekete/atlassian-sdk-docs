---
aliases:
- /server/framework/atlassian-sdk/maven-is-unable-to-download-the-artifact-from-any-repository-2818710.html
- /server/framework/atlassian-sdk/maven-is-unable-to-download-the-artifact-from-any-repository-2818710.md
category: devguide
confluence_id: 2818710
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818710
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818710
date: '2017-12-08'
legacy_title: Maven is Unable to Download the Artifact from Any Repository
platform: server
product: atlassian-sdk
subcategory: faq
title: Maven is unable to download the artifact from any repository
---
# Maven is unable to download the artifact from any repository

You may find that Maven complains it is "Unable to download the artifact from any repository."

We use the Maven project's <a href="http://maven.apache.org/archiva/" class="external-link">Archiva Maven Proxy</a> to act as our Maven repository. Sometimes, however, artifact downloads fail because of Archiva's instabilities. If you run into messages like this, sometimes a second attempt will succeed in downloading the artifact. If it doesn't work after a few times, then the artifact may be truly missing. You can <a href="http://maven.atlassian.com" class="external-link">search our Archiva</a> to confirm this.




























































































