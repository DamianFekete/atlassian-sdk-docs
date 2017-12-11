---
aliases:
- /server/framework/atlassian-sdk/command-reference-2818724.html
- /server/framework/atlassian-sdk/command-reference-2818724.md
category: devguide
confluence_id: 2818724
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818724
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818724
date: '2017-12-11'
guides: guides
legacy_title: Command Reference
platform: server
product: atlassian-sdk
subcategory: learning
title: Command reference
---
# Command reference

-   [atlas-clean](/server/framework/atlassian-sdk/atlas-clean) -- atlas-clean \[options\] - Removes files from the project directory, that were generated during the build. (Runs mvn clean.) Passes all parameters straight through to Maven.
-   [atlas-cli](/server/framework/atlassian-sdk/atlas-cli) -- atlas-cli \[options\] - Starts up a command line interface to your plugin running in the host application. After you change the plugin code, enter pi at the CLI prompt to install the updated plugin in the Atlassian application. (Runs mvn amps:cli.) Interpreted parameters: http-port, context-path, server, cli-port.
-   [atlas-clover](/server/framework/atlassian-sdk/atlas-clover) -- atlas-clover \[options\] - Runs unit and integration tests, generating a code coverage report with Clover http://atlassian.com/clover. Passes all parameters straight through to Maven. Report is available in target/site/clover/index.html.
-   [atlas-compile](/server/framework/atlassian-sdk/atlas-compile) -- atlas-compile \[options\] - Compiles the sources of your project. (Runs mvn compile.) Passes all parameters straight through to Maven.
-   [atlas-create-bamboo-plugin](/server/framework/atlassian-sdk/atlas-create-bamboo-plugin) -- atlas-create-bamboo-plugin \[options\] - Creates an example of a Bamboo plugin, which you can adapt to suit your own plugin's needs. (Runs mvn bamboo:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-bamboo-plugin-module](/server/framework/atlassian-sdk/atlas-create-bamboo-plugin-module) -- atlas-create-bamboo-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a Bamboo plugin module that you can adapt to suit your own plugin's needs. (Runs mvn bamboo:create-plugin-module.) Passes all parameters straight through to Maven.
-   [atlas-create-confluence-plugin](/server/framework/atlassian-sdk/atlas-create-confluence-plugin) -- atlas-create-confluence-plugin \[options\] - Creates an example of a Confluence plugin, which you can adapt to suit your own plugin's needs. (Runs mvn confluence:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-confluence-plugin-module](/server/framework/atlassian-sdk/atlas-create-confluence-plugin-module) -- atlas-create-confluence-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a Confluence plugin module that you can adapt to suit your own plugin's needs. (Runs mvn confluence:create-plugin-module.) Passes all parameters straight through to Maven. 
-   [atlas-create-crowd-plugin](/server/framework/atlassian-sdk/atlas-create-crowd-plugin) -- atlas-create-crowd-plugin \[options\] - Creates an example of a Crowd plugin, which you can adapt to suit your own plugin's needs. (Runs mvn crowd:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-crowd-plugin-module](/server/framework/atlassian-sdk/atlas-create-crowd-plugin-module) -- atlas-create-crowd-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a Crowd plugin module that you can adapt to suit your own plugin's needs. (Runs mvn crowd:create-plugin-module.) Passes all parameters straight through to Maven.
-   [atlas-create-fecru-plugin](/server/framework/atlassian-sdk/atlas-create-fecru-plugin) -- atlas-create-fecru-plugin \[options\] - Creates an example of a FishEye or Crucible plugin, which you can adapt to suit your own plugin's needs. (Runs mvn fecru:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-fecru-plugin-module](/server/framework/atlassian-sdk/atlas-create-fecru-plugin-module) -- This page describes the shell script atlas-create-fecru-plugin-module, part of the Atlassian Plugin SDK. 
-   [atlas-create-home-zip](/server/framework/atlassian-sdk/atlas-create-home-zip) -- atlas-create-home-zip - Creates a test-resources zip of the current application's home directory. This zip file can then be pointed to in the AMPS productDataPath property to auto-populate application data during startup.
-   [atlas-create-jira-plugin](/server/framework/atlassian-sdk/atlas-create-jira-plugin) -- This page describes the shell script atlas-create-jira-plugin, part of the Atlassian Plugin SDK.
-   [atlas-create-jira-plugin-module](/server/framework/atlassian-sdk/atlas-create-jira-plugin-module) -- atlas-create-jira-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a JIRA plugin module that you can adapt to suit your own plugin's needs. (Runs mvn jira:create-plugin-module.) Passes all parameters straight through to Maven. 
-   [atlas-create-refapp-plugin](/server/framework/atlassian-sdk/atlas-create-refapp-plugin) -- atlas-create-refapp-plugin \[options\] - Creates an example of a RefApp plugin, which you can adapt to suit your own plugin's needs. (Runs mvn refapp:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-refapp-plugin-module](/server/framework/atlassian-sdk/atlas-create-refapp-plugin-module) -- atlas-create-refapp-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a plugin module for the RefApp that you can adapt to suit your own plugin's needs. (Runs mvn refapp:create-plugin-module.) Passes all parameters straight through to Maven. 
-   [atlas-debug](/server/framework/atlassian-sdk/atlas-debug) -- atlas-debug \[options\] - Runs the application in debug mode with your plugin installed. (Runs mvn amps:debug.) Interpreted parameters: version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins, lib-plugins, bundled-plugins, product, jvm-debug-port, jvm-debug-suspend.
-   [atlas-help](/server/framework/atlassian-sdk/atlas-help) -- atlas-help \[--verbose\] - Displays help text for the shell scripts incorporated into the Atlassian Plugin SDK. Interpreted parameters: verbose.
-   [atlas-install-idea-plugin (not published)](/server/framework/atlassian-sdk/atlas-install-idea-plugin)
-   [atlas-install-plugin](/server/framework/atlassian-sdk/atlas-install-plugin) -- atlas-install-plugin \[options\] - Installs the plugin into a running application. (Runs mvn amps:install.) Interpreted parameters: http-port, context-path, server, username, password, plugin-key.
-   [atlas-integration-test](/server/framework/atlassian-sdk/atlas-integration-test) -- atlas-integration-test \[options\] - Runs the integration tests for the plugin. (Runs mvn integration-test.) Interpreted parameters: version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins,lib-plugins, bundled-plugins, product, no-webapp, skip-tests.
-   [atlas-mvn](/server/framework/atlassian-sdk/atlas-mvn) -- atlas-mvn \[options\] - Allows you to execute any Maven command using the version of Maven bundled with your Atlassian Plugin SDK. (Runs mvn.) Passes all parameters straight through to Maven.
-   [atlas-package](/server/framework/atlassian-sdk/atlas-package) -- atlas-package\[options\] - Packages the plugin artifacts and produces the JAR. (Runs mvn package.) Passes all parameters straight through to Maven.
-   [atlas-release](/server/framework/atlassian-sdk/atlas-release) -- atlas-release \[options\] - Performs a release of the current plugin. (Runs mvn release:prepare release:perform.) Passes all parameters straight through to Maven.
-   [atlas-release-rollback](/server/framework/atlassian-sdk/atlas-release-rollback) -- atlas-release-rollback \[options\] - Rolls back a release of the current plugin. (Runs mvn release:rollback.) Passes all parameters straight through to Maven.
-   [atlas-run](/server/framework/atlassian-sdk/atlas-run) -- atlas-run \[options\] - Runs the application with your plugin installed. (Runs mvn amps:run.) Interpreted parameters: version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins, lib-plugins, bundled-plugins, product.
-   [atlas-run-cloud](/server/framework/atlassian-sdk/atlas-run-cloud) -- atlas-run-cloud \[options\] - Runs an Atlassian application with Connect and the Cloud dependencies installed. Interpreted parameters: application, maven-plugin-version.
-   [atlas-run-standalone](/server/framework/atlassian-sdk/atlas-run-standalone) -- atlas-run-standalone \[options\] - Runs an Atlassian application standalone, without a plugin project (that is, not requiring atlas-create-&lt;product&gt;-plugin). Interpreted parameters: version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins, lib-plugins, bundled-plugins, product.
-   [atlas-unit-test](/server/framework/atlassian-sdk/atlas-unit-test) -- atlas-unit-test \[options\] - Runs the unit tests for your plugin. (Runs mvn test.) Passes all parameters straight through to Maven.
-   [atlas-update](/server/framework/atlassian-sdk/atlas-update) -- atlas-update \[options\] - Updates the Atlassian Plugin SDK.
-   [atlas-version](/server/framework/atlassian-sdk/atlas-version) -- atlas-version - Displays version and runtime information for the Atlassian Plugin SDK. (Runs mvn --version.)









































































































































































































































































































