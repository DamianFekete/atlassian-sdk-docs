---
aliases:
- /server/framework/atlassian-sdk/product-fails-to-start-within-timeout-period-45523672.html
- /server/framework/atlassian-sdk/product-fails-to-start-within-timeout-period-45523672.md
category: devguide
confluence_id: 45523672
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=45523672
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=45523672
date: '2017-12-08'
legacy_title: Product Fails to Start Within Timeout Period
platform: server
product: atlassian-sdk
subcategory: faq
title: Product fails to start within timeout period
---
# Product fails to start within timeout period

## Problem

Running a plugin project (via `atlas-run`, `atlas-debug` or `atlas-run-standalone`) results in the startup process taking a long time and eventually the following error:

``` bash
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 13:07 min
[INFO] Finished at: 2017-01-26T13:42:48-08:00
[INFO] Final Memory: 38M/436M
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal com.atlassian.maven.plugins:maven-amps-dispatcher-plugin:6.2.11:run (default-cli) on project myConfluenceMacro: Unable to execute mojo: Execution null of goal org.codehaus.cargo:cargo-maven2-plugin:1.4.7:start failed: Deployable [http://localhost:1990/cargocpc/index.html]
 failed to finish deploying within the timeout period [600000]. The 
Deployable state is thus unknown. -> [Help 1]
org.apache.maven.lifecycle.LifecycleExecutionException:
 Failed to execute goal 
com.atlassian.maven.plugins:maven-amps-dispatcher-plugin:6.2.11:run (default-cli) on project myConfluenceMacro: Unable to execute mojo
```

The example above is a Confluence plugin but this can happen for any product supported by the SDK. Cargo maven plugin has timeouts (600,000ms or 10 minutes in the above example) and if the product fails to launch within this time the maven build will fail.

## Solution

This problem can have different causes, the most frequently encountered being anti-virus scans slowing the build down. Play with the settings of your anti-virus software (whitelist directory, disable scanning of WARs and JARs) to get the build to finish within the timeout period.
