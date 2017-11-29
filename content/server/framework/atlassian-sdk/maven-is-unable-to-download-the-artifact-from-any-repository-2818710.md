---
title: Maven is Unable to Download the Artifact From Any Repository 2818710
aliases:
    - /server/framework/atlassian-sdk/maven-is-unable-to-download-the-artifact-from-any-repository-2818710.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818710
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818710
confluence_id: 2818710
platform:
product:
category:
subcategory:
---
# Maven is unable to download the artifact from any repository

You may find that Maven complains it is "Unable to download the artifact from any repository."

We use the Maven project's <a href="http://maven.apache.org/archiva/" class="external-link">Archiva Maven Proxy</a> to act as our Maven repository. Sometimes, however, artifact downloads fail because of Archiva's instabilities. If you run into messages like this, sometimes a second attempt will succeed in downloading the artifact. If it doesn't work after a few times, then the artifact may be truly missing. You can <a href="http://maven.atlassian.com" class="external-link">search our Archiva</a> to confirm this.

 

























