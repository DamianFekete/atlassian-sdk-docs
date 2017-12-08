---
aliases:
- /server/framework/atlassian-sdk/deployment-stalled-due-to-spaces-in-directory-path-2818388.html
- /server/framework/atlassian-sdk/deployment-stalled-due-to-spaces-in-directory-path-2818388.md
category: devguide
confluence_id: 2818388
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818388
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818388
date: '2017-12-08'
legacy_title: Deployment stalled due to spaces in directory path
platform: server
product: atlassian-sdk
subcategory: faq
title: Deployment stalled due to spaces in directory path
---
# Deployment stalled due to spaces in directory path

If you get an error like the one below after running `atlas-run`, please check that the directory path to your plugin does not contain spaces. (Issue tracking is at <a href="https://studio.atlassian.com/browse/AMPS-126" class="external-link">AMPS-126</a>.)

``` bash
34K downloaded  (cargo-core-container-weblogic-1.0-beta-2.jar)
[INFO] [cargo:start]
[INFO] [stalledLocalDeployer] Deploying [C:\Documents and Settings\name\My Do
cuments\source\test-plugin\plugintest\target\confluence\confluence.war] to [C:\D
ocuments and Settings\name\My Documents\source\test-plugin\plugintest\target\
container\tomcat6x\cargo-confluence-home/webapps]...
[INFO] [talledLocalContainer] Tomcat 6.x starting...
[WARNING] [talledLocalContainer] java.lang.NoClassDefFoundError: and
[WARNING] [talledLocalContainer] Exception in thread "main"
[WARNING] [talledLocalContainer] Java Result: 1
[INFO] ------------------------------------------------------------------------
[ERROR] BUILD ERROR
[INFO] ------------------------------------------------------------------------
[INFO] Unable to execute mojo

Deployable [http://localhost:1990/cargocpc/index.html] failed to finish deployin
g within the timeout period [120000]. The Deployable state is thus unknown.
[INFO] ------------------------------------------------------------------------
[INFO] For more information, run Maven with the -e switch
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 6 minutes 36 seconds
[INFO] Finished at: Tue Jun 15 09:05:51 EDT 2010
[INFO] Final Memory: 49M/97M
[INFO] ------------------------------------------------------------------------
```








































































































