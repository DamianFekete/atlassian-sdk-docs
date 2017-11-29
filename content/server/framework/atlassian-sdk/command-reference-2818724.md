---
title: Command Reference 2818724
aliases:
    - /server/framework/atlassian-sdk/command-reference-2818724.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818724
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818724
confluence_id: 2818724
platform:
product:
category:
subcategory:
---
# Command reference

-   [atlas-clean](/server/framework/atlassian-sdk/atlas-clean-2818352.html) -- atlas-clean \[options\] - Removes files from the project directory, that were generated during the build. (Runs mvn clean.) Passes all parameters straight through to Maven.
-   [atlas-cli](/server/framework/atlassian-sdk/atlas-cli-2818336.html) -- atlas-cli \[options\] - Starts up a command line interface to your plugin running in the host application. After you change the plugin code, enter pi at the CLI prompt to install the updated plugin in the Atlassian application. (Runs mvn amps:cli.) Interpreted parameters: http-port, context-path, server, cli-port.
-   [atlas-clover](/server/framework/atlassian-sdk/atlas-clover-2818720.html) -- atlas-clover \[options\] - Runs unit and integration tests, generating a code coverage report with Clover http://atlassian.com/clover. Passes all parameters straight through to Maven. Report is available in target/site/clover/index.html.
-   [atlas-compile](/server/framework/atlassian-sdk/atlas-compile-2818348.html) -- atlas-compile \[options\] - Compiles the sources of your project. (Runs mvn compile.) Passes all parameters straight through to Maven.
-   [atlas-create-bamboo-plugin](/server/framework/atlassian-sdk/atlas-create-bamboo-plugin-2818353.html) -- atlas-create-bamboo-plugin \[options\] - Creates an example of a Bamboo plugin, which you can adapt to suit your own plugin's needs. (Runs mvn bamboo:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-bamboo-plugin-module](/server/framework/atlassian-sdk/atlas-create-bamboo-plugin-module-8945887.html) -- atlas-create-bamboo-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a Bamboo plugin module that you can adapt to suit your own plugin's needs. (Runs mvn bamboo:create-plugin-module.) Passes all parameters straight through to Maven.
-   [atlas-create-confluence-plugin](/server/framework/atlassian-sdk/atlas-create-confluence-plugin-2818342.html) -- atlas-create-confluence-plugin \[options\] - Creates an example of a Confluence plugin, which you can adapt to suit your own plugin's needs. (Runs mvn confluence:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-confluence-plugin-module](/server/framework/atlassian-sdk/atlas-create-confluence-plugin-module-8945880.html) -- atlas-create-confluence-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a Confluence plugin module that you can adapt to suit your own plugin's needs. (Runs mvn confluence:create-plugin-module.) Passes all parameters straight through to Maven.
-   [atlas-create-crowd-plugin](/server/framework/atlassian-sdk/atlas-create-crowd-plugin-2818340.html) -- atlas-create-crowd-plugin \[options\] - Creates an example of a Crowd plugin, which you can adapt to suit your own plugin's needs. (Runs mvn crowd:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-crowd-plugin-module](/server/framework/atlassian-sdk/atlas-create-crowd-plugin-module-8945890.html) -- atlas-create-crowd-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a Crowd plugin module that you can adapt to suit your own plugin's needs. (Runs mvn crowd:create-plugin-module.) Passes all parameters straight through to Maven.
-   [atlas-create-fecru-plugin](/server/framework/atlassian-sdk/atlas-create-fecru-plugin-2818344.html) -- atlas-create-fecru-plugin \[options\] - Creates an example of a FishEye or Crucible plugin, which you can adapt to suit your own plugin's needs. (Runs mvn fecru:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-fecru-plugin-module](/server/framework/atlassian-sdk/atlas-create-fecru-plugin-module-8945893.html) -- atlas-create-fecru-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a FishEye/Crucible plugin module that you can adapt to suit your own plugin's needs. (Runs mvn fecru:create-plugin-module.) Passes all parameters straight through to Maven.
-   [atlas-create-home-zip](/server/framework/atlassian-sdk/atlas-create-home-zip-2818359.html) -- atlas-create-home-zip - Creates a test-resources zip of the current application's home directory. This zip file can then be pointed to in the AMPS productDataPath property to auto-populate application data during startup.
-   [atlas-create-jira-plugin](/server/framework/atlassian-sdk/atlas-create-jira-plugin-2818339.html) -- atlas-create-jira-plugin \[options\] - Creates an example of a JIRA plugin, which you can adapt to suit your own plugin's needs. (Runs mvn jira:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-jira-plugin-module](/server/framework/atlassian-sdk/atlas-create-jira-plugin-module-8945854.html) -- atlas-create-jira-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a JIRA plugin module that you can adapt to suit your own plugin's needs. (Runs mvn jira:create-plugin-module.) Passes all parameters straight through to Maven.
-   [atlas-create-refapp-plugin](/server/framework/atlassian-sdk/atlas-create-refapp-plugin-2818343.html) -- atlas-create-refapp-plugin \[options\] - Creates an example of a RefApp plugin, which you can adapt to suit your own plugin's needs. (Runs mvn refapp:create.) Interpreted parameters: artifact-id, group-id, version, package, non-interactive.
-   [atlas-create-refapp-plugin-module](/server/framework/atlassian-sdk/atlas-create-refapp-plugin-module-8945896.html) -- atlas-create-refapp-plugin-module \[options\] - Prompts you for plugin module type and related details, then creates an example of a plugin module for the RefApp that you can adapt to suit your own plugin's needs. (Runs mvn refapp:create-plugin-module.) Passes all parameters straight through to Maven.
-   [atlas-debug](/server/framework/atlassian-sdk/atlas-debug-2818346.html) -- atlas-debug \[options\] - Runs the application in debug mode with your plugin installed. (Runs mvn amps:debug.) Interpreted parameters: version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins, lib-plugins, bundled-plugins, product, jvm-debug-port, jvm-debug-suspend.
-   [atlas-help](/server/framework/atlassian-sdk/atlas-help-2818350.html) -- atlas-help \[--verbose\] - Displays help text for the shell scripts incorporated into the Atlassian Plugin SDK. Interpreted parameters: verbose.
-   [atlas-install-idea-plugin (not published)](/server/framework/atlassian-sdk/2818719.html) -- atlas-install-idea-plugin - Configures IntelliJ IDEA for CLI integration. (Runs mvn amps:idea.)
-   [atlas-install-plugin](/server/framework/atlassian-sdk/atlas-install-plugin-2818722.html) -- atlas-install-plugin \[options\] - Installs the plugin into a running application. (Runs mvn amps:install.) Interpreted parameters: http-port, context-path, server, username, password, plugin-key.
-   [atlas-integration-test](/server/framework/atlassian-sdk/atlas-integration-test-2818349.html) -- atlas-integration-test \[options\] - Runs the integration tests for the plugin. (Runs mvn integration-test.) Interpreted parameters: version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins,lib-plugins, bundled-plugins, product, no-webapp, skip-tests.
-   [atlas-mvn](/server/framework/atlassian-sdk/atlas-mvn-2818341.html) -- atlas-mvn \[options\] - Allows you to execute any Maven command using the version of Maven bundled with your Atlassian Plugin SDK. (Runs mvn.) Passes all parameters straight through to Maven.
-   [atlas-package](/server/framework/atlassian-sdk/atlas-package-2818351.html) -- atlas-package\[options\] - Packages the plugin artifacts and produces the JAR. (Runs mvn package.) Passes all parameters straight through to Maven.
-   [atlas-release](/server/framework/atlassian-sdk/atlas-release-2818354.html) -- atlas-release \[options\] - Performs a release of the current plugin. (Runs mvn release:prepare release:perform.) Passes all parameters straight through to Maven.
-   [atlas-release-rollback](/server/framework/atlassian-sdk/atlas-release-rollback-2818347.html) -- atlas-release-rollback \[options\] - Rolls back a release of the current plugin. (Runs mvn release:rollback.) Passes all parameters straight through to Maven.
-   [atlas-run](/server/framework/atlassian-sdk/atlas-run-2818725.html) -- atlas-run \[options\] - Runs the application with your plugin installed. (Runs mvn amps:run.) Interpreted parameters: version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins, lib-plugins, bundled-plugins, product.
-   [atlas-run-cloud](/server/framework/atlassian-sdk/atlas-run-cloud-37882647.html) -- atlas-run-cloud \[options\] - Runs an Atlassian application with Connect and the Cloud dependencies installed. Interpreted parameters: application, maven-plugin-version.
-   [atlas-run-standalone](/server/framework/atlassian-sdk/atlas-run-standalone-2818534.html) -- atlas-run-standalone \[options\] - Runs an Atlassian application standalone, without a plugin project (that is, not requiring atlas-create-&lt;product&gt;-plugin). Interpreted parameters: version, container, http-port, context-path, server, jvmargs, log4j, test-version, sal-version, rest-version, plugins, lib-plugins, bundled-plugins, product.
-   [atlas-unit-test](/server/framework/atlassian-sdk/atlas-unit-test-2818360.html) -- atlas-unit-test \[options\] - Runs the unit tests for your plugin. (Runs mvn test.) Passes all parameters straight through to Maven.
-   [atlas-update](/server/framework/atlassian-sdk/atlas-update-13633056.html) -- atlas-update \[options\] - Updates the Atlassian Plugin SDK.
-   [atlas-version](/server/framework/atlassian-sdk/atlas-version-2818345.html) -- atlas-version - Displays version and runtime information for the Atlassian Plugin SDK. (Runs mvn --version.)

























