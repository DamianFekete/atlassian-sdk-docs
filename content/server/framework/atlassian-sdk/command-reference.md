---
aliases:
- /server/framework/atlassian-sdk/command-reference-2818724.html
- /server/framework/atlassian-sdk/command-reference-2818724.md
category: devguide
confluence_id: 2818724
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818724
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818724
date: '2017-12-08'
guides: guides
legacy_title: Command Reference
platform: server
product: atlassian-sdk
subcategory: learning
title: Command reference
---
# Command reference

The Atlassian Plugin SDK commands below allow you to create, build, customize, package and test Add-ons for Atlassian Server products such as JIRA, Confluence, Bitbucket and Bamboo. 

To install the Atlassian Plugin SDK, see: 

- [Install the Atlassian SDK on a Windows system](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/install-the-atlassian-sdk-on-a-windows-system)
- [Install the Atlassian SDK on a Linux or Mac system](https://developer.atlassian.com/server/framework/atlassian-sdk/install-the-atlassian-sdk-on-a-linux-or-mac-system/)

{{% note title="New to the SDK?" %}}
If you haven't used the Atlassian Plugin SDK before, you may wish to start with the tutorial: [Set up the Atlassian SDK and build a project](http://localhost:8080/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project/)
{{% /note %}}

<table>
    <col width="25%">
    <col width="25%">
    <col width="50%">
    <thead>
        <tr>
            <th>Command</th>
            <th>Example</th>
            <th>Description</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-clean">atlas-clean</a></td>
            <td><code>atlas-clean [options]</code></td>
            <td><p>Removes files from the project directory, that were generated during the build. Runs <code>mvn clean</code>. </p>
            <p>Passes all parameters straight through to Maven.</p></td>
        </tr>
        <tr>
             <td><a href="/server/framework/atlassian-sdk/atlas-cli">atlas-cli</a></td>
             <td><code>atlas-cli [options]</code></td>
             <td><p>Starts up a command line interface to your plugin running in the host application. After you change the plugin code, enter pi at the CLI prompt to install the updated plugin in the Atlassian application. Runs <code>mvn amps:cli</code>.</p> 
             <p>Interpreted parameters: <code>http-port</code>, <code>context-path</code>, <code>server</code>, <code>cli-port</code>.</p></td>
        </tr>
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-clover">atlas-clover</a></td>
             <td><code>atlas-clover [options]</code></td>
             <td><p>Runs unit and integration tests, generating a code coverage report with <a href="http://atlassian.com/clover">Clover</a>. </p>
             <p>Passes all parameters straight through to Maven. Report is available in <code>target/site/clover/index.html</code>.</p></td>
        </tr>
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-compile">atlas-compile</a></td>
             <td><code>atlas-compile [options]</code></td>
             <td><p>Compiles the sources of your project. Runs <code>mvn compile</code>.</p>
              <p>Passes all parameters straight through to Maven.</p></td>
        </tr>
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-bamboo-plugin">atlas-create-bamboo-plugin</a></td>
            <td><code>atlas-create-bamboo-plugin [options]</code></td>
            <td><p>Creates an example of a Bamboo plugin, which you can adapt to suit your own plugin's needs. Runs <code>mvn bamboo:create</code>.</p> 
            <p>Interpreted parameters: <code>artifact-id</code>, <code>group-id</code>, <code>version</code>, <code>package</code>, <code>non-interactive</code>.</p></td>
        </tr>
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-bamboo-plugin-module">atlas-create-bamboo-plugin-module</a></td>
             <td><code>atlas-create-bamboo-plugin-module [options]</code></td> 
             <td><p>Prompts you for plugin module type and related details, then creates an example of a Bamboo plugin module that you can adapt to suit your own plugin's needs. Runs <code>mvn bamboo:create-plugin-module</code>.</p> 
             <p>Passes all parameters straight through to Maven.</p></td>
        </tr>
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-bitbucket-plugin">atlas-create-bitbucket-plugin</a></td>
            <td><code>atlas-create-bitbucket-plugin [options]</code></td>
            <td><p>Creates an example of a Bitbucket plugin, which you can adapt to suit your own plugin's needs. Runs <code>mvn bitbucket:create</code>.</p> 
            <p>Interpreted parameters: <code>artifact-id</code>, <code>group-id</code>, <code>version</code>, <code>package</code>, <code>non-interactive</code>.</p></td></td>
        </tr>
                <tr>
                    <td><a href="/server/framework/atlassian-sdk/atlas-create-bitbucket-plugin-module">atlas-create-bitbucket-plugin-module</a></td>
                     <td><code>atlas-create-bitbucket-plugin-module [options]</code></td> 
                     <td><p>Prompts you for plugin module type and related details, then creates an example of a Bitbucket plugin module that you can adapt to suit your own plugin's needs. Runs <code>mvn bitbucket:create-plugin-module</code>.</p> 
                     <p>Passes all parameters straight through to Maven.</p></td>
                </tr>
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-confluence-plugin">atlas-create-confluence-plugin</a></td>
            <td><code>atlas-create-confluence-plugin [options]</code></td>
            <td><p>Creates an example of a Confluence plugin, which you can adapt to suit your own plugin's needs. Runs <code>mvn confluence:create</code>.</p> 
            <p>Interpreted parameters: <code>artifact-id</code>, <code>group-id</code>, <code>version</code>, <code>package</code>, <code>non-interactive</code>.</p></td>
        </tr>
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-confluence-plugin-module">atlas-create-confluence-plugin-module</a></td>
            <td><code>atlas-create-confluence-plugin-module [options]</code></td>
            <td><p>Prompts you for plugin module type and related details, then creates an example of a Confluence plugin module that you can adapt to suit your own plugin's needs. Runs <code>mvn confluence:create-plugin-module</code>. </p>
            <p>Passes all parameters straight through to Maven.</p></td>
        </tr>        
        <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-crowd-plugin">atlas-create-crowd-plugin</a></td>
            <td><code>atlas-create-crowd-plugin [options]</code></td>
            <td><p>Creates an example of a Crowd plugin, which you can adapt to suit your own plugin's needs. Runs <code>mvn crowd:create</code>.</p> 
            <p>Interpreted parameters: <code>artifact-id</code>, <code>group-id</code>, <code>version</code>, <code>package</code>, <code>non-interactive</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-crowd-plugin-module">atlas-create-crowd-plugin-module</a></td>
            <td><code>atlas-create-crowd-plugin-module [options]</code></td>
            <td><p>Prompts you for plugin module type and related details, then creates an example of a Crowd plugin module that you can adapt to suit your own plugin's needs. Runs <code>mvn crowd:create-plugin-module</code>. </p>
            <p>Passes all parameters straight through to Maven.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-fecru-plugin">atlas-create-fecru-plugin</a></td>
            <td><code>atlas-create-fecru-plugin [options]</code></td>
            <td><p>Creates an example of a FishEye or Crucible plugin, which you can adapt to suit your own plugin's needs. Runs <code>mvn fecru:create</code>.</p> 
            <p>Interpreted parameters: <code>artifact-id</code>, <code>group-id</code>, <code>version</code>, <code>package</code>, <code>non-interactive</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-fecru-plugin-module">atlas-create-fecru-plugin-module</a></td> 
            <td><code>atlas-create-fecru-plugin-module [options]</code></td>
            <td><p>Prompts you for plugin module type and related details, then creates an example of a Fecru plugin module that you can adapt to suit your own plugin's needs. Runs <code>mvn crowd:create-plugin-module</code>.</p> 
            <p>Passes all parameters straight through to Maven.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-home-zip">atlas-create-home-zip</a></td>
            <td><code>atlas-create-home-zip</code></td>
            <td><p>Creates a test-resources zip of the current application's home directory. This zip file can then be pointed to in the AMPS productDataPath property to auto-populate application data during startup.</p></td>
         </tr>
         <tr>
            <td><a href="(/server/framework/atlassian-sdk/atlas-create-jira-plugin">atlas-create-jira-plugin</a>
            <td><code>atlas-create-jira-plugin [options]</code></td>
            <td><p>Creates an example of a JIRA plugin, which you can adapt to suit your own plugin's needs. Runs <code>mvn jira:create</code>. </p>
            <p>Interpreted parameters: <code>artifact-id</code>, <code>group-id</code>, <code>version</code>, <code>package</code>, <code>non-interactive</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-jira-plugin-module">atlas-create-jira-plugin-module</a></td>
            <td><code>atlas-create-jira-plugin-module [options]</code></td>
            <td><p>Prompts you for plugin module type and related details, then creates an example of a JIRA plugin module that you can adapt to suit your own plugin's needs. Runs <code>mvn jira:create-plugin-module</code>.</p>
             <p>Passes all parameters straight through to Maven.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-refapp-plugin">atlas-create-refapp-plugin</a></td>
            <td><code>atlas-create-refapp-plugin [options]</code></td>
            <td><p>Creates an example of a RefApp plugin, which you can adapt to suit your own plugin's needs. Runs <code>mvn refapp:create</code>.</p>
            <p>Interpreted parameters: <code>artifact-id</code>, <code>group-id</code>, <code>version</code>, <code>package</code>, <code>non-interactive</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-create-refapp-plugin-module">atlas-create-refapp-plugin-module</a></td>
            <td><code>atlas-create-refapp-plugin-module [options]</code></td>
            <td><p>Prompts you for plugin module type and related details, then creates an example of a plugin module for the RefApp that you can adapt to suit your own plugin's needs. Runs <code>mvn refapp:create-plugin-module</code>.</p> 
            <p>Passes all parameters straight through to Maven. </p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-debug">atlas-debug</a></td>
            <td><code>atlas-debug [options]</code></td>
            <td><p>Runs the application in debug mode with your plugin installed. Runs <code>mvn amps:debug</code>.</p> 
            <p>Interpreted parameters: <code>version</code>, <code>container</code>, <code>http-port</code>, <code>context-path</code>, <code>server</code>, <code>jvmargs</code>, <code>log4j</code>, <code>test-version</code>, <code>sal-version</code>, <code>rest-version</code>, <code>plugins</code>, <code>lib-plugins</code>, <code>bundled-plugins</code>, <code>product</code>, <code>jvm-debug-port</code>, <code>jvm-debug-suspend</code>.</p></td>
         </tr>
         <tr>
             <td><a href="/server/framework/atlassian-sdk/atlas-help">atlas-help</a></td>
             <td><code>atlas-help \[--verbose\]</code></td> 
             <td><p>Displays help text for the shell scripts incorporated into the Atlassian Plugin SDK. </p>
             <p>Interpreted parameters: <code>verbose</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-install-plugin">atlas-install-plugin</a></td>
            <td><code>atlas-install-plugin [options]</code></td>
            <td><p>Installs the plugin into a running application. Runs <code>mvn amps:install</code>.</p>     
            <p>Interpreted parameters: <code>http-port</code>, <code>context-path</code>, <code>server</code>, <code>username</code>, <code>password</code>, <code>plugin-key</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-integration-test">atlas-integration-test</a></td>
            <td><code>atlas-integration-test [options]</code></td>
            <td><p>Runs the integration tests for the plugin. Runs <code>mvn integration-test</code>.</p> 
            <p>Interpreted parameters: <code>version</code>, <code>container</code>, <code>http-port</code>, <code>context-path</code>, <code>server</code>, <code>jvmargs</code>, <code>log4j</code>, <code>test-version</code>, <code>sal-version</code>, <code>rest-version</code>, <code>plugins</code>, <code>lib-plugins</code>, <code>bundled-plugins</code>, <code>product</code>, <code>no-webapp</code>, <code>skip-tests</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-mvn">atlas-mvn</a></td>
            <td><code>atlas-mvn [options]</code></td>
            <td><p>Allows you to execute any Maven command using the version of Maven bundled with your Atlassian Plugin SDK. Runs <code>mvn</code>.</p> 
            <p>Passes all parameters straight through to Maven.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-package">atlas-package</a></td>
            <td><code>atlas-package[options]</code></td>
            <td><p>Packages the plugin artifacts and produces the JAR. Runs <code>mvn package</code>.</p> 
            <p>Passes all parameters straight through to Maven.</p></td>
         </tr>
         <tr>
             <td><a href="/server/framework/atlassian-sdk/atlas-release">atlas-release</a></td>
             <td><code>atlas-release [options]</code></td>
             <td><p>Performs a release of the current plugin. Runs <code>mvn release:prepare release:perform</code>.</p>
              <p>Passes all parameters straight through to Maven.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-release-rollback">atlas-release-rollback</a></td>
            <td><code>atlas-release-rollback [options]</code></td>
            <td><p>Rolls back a release of the current plugin. Runs <code>mvn release:rollback</code>.</p> 
            <p>Passes all parameters straight through to Maven.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-run">atlas-run</a></td>
             <td><code>atlas-run [options]</code></td>
             <td><p>Runs the application with your plugin installed. Runs <code>mvn amps:run</code>. </p>
             <p>Interpreted parameters: <code>version</code>, <code>container</code>, <code>http-port</code>, <code>context-path</code>, <code>server</code>, <code>jvmargs</code>, <code>log4j</code>, <code>test-version</code>, <code>sal-version</code>, <code>rest-version</code>, <code>plugins</code>, <code>lib-plugins</code>, <code>bundled-plugins</code>, <code>product</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-run-standalone">atlas-run-standalone</a></td>
            <td><code>atlas-run-standalone [options]</code></td>
            <td><p>Runs an Atlassian application standalone, without a plugin project (that is, not requiring atlas-create-&lt;product&gt;-plugin)</p>. 
            <p>Interpreted parameters: <code>version</code>, <code>container</code>, <code>http-port</code>, <code>context-path</code>, <code>server</code>, <code>jvmargs</code>, <code>log4j</code>, <code>test-version</code>, <code>sal-version</code>, <code>rest-version</code>, <code>plugins</code>, <code>lib-plugins</code>, <code>bundled-plugins</code>, <code>product</code>.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-unit-test">atlas-unit-test</a></td>
            <td><code>atlas-unit-test [options]</code></td>
            <td><p>Runs the unit tests for your plugin. Runs <code>mvn test</code>.</p>
            <p>Passes all parameters straight through to Maven.</p></td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-update">atlas-update</a></td>
            <td><code>atlas-update [options]</code></td>
            <td>Updates the Atlassian Plugin SDK.</td>
         </tr>
         <tr>
            <td><a href="/server/framework/atlassian-sdk/atlas-version">atlas-version</a></td>
            <td><code>atlas-version</code></td>
            <td><p>Displays version and runtime information for the Atlassian Plugin SDK. Runs <code>mvn --version</code>.</p></td>
         </tr>
    </tbody>
</table>
   
{{% warning %}}
Found a bug with one of the above commands? You can report it at [ecosystem.atlassian.net](https://ecosystem.atlassian.net/projects/ATLASSDK/issues?filter=allissues)
{{% /warning %}}
