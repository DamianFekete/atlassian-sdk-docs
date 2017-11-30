---
aliases:
- /server/framework/atlassian-sdk/developing-speakeasy-extensions-2818113.html
- /server/framework/atlassian-sdk/developing-speakeasy-extensions-2818113.md
category: devguide
confluence_id: 2818113
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818113
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818113
learning: guides
legacy_url: https://developer.atlassian.com/docs/advanced-topics/speakeasy/developing-speakeasy-extensions
new_url: /server/framework/atlassian-sdk/developing-speakeasy-extensions
platform: server
product: atlassian-sdk
subcategory: learning
title: Developing Speakeasy extensions
---
# Developing Speakeasy extensions

 

## What can extensions do?

Speakeasy lets you to write a special, simple type of Atlassian Plugin, called an extension. The extension can then be shared with others by allowing them to opt-in, or enable, the extension on a person-by-person basis. This dramatically reduces the risk to server operation and other users, while giving you an opportunity to try out our plugin idea with production data and use it on a daily basis.

Extensions are currently limited to all things client-side:

-   JavaScript
-   CSS
-   Web items/sections/panels
-   Images
-   HTML

As such, you can do things like:

-   Add, modify, or remove UI elements
-   Provide shortcuts for sets of operations via XHR automatation
-   Incorporate external data via consumption of JSONP

Even better, take a look at the [Speakeasy Extension Examples](https://developer.atlassian.com/display/SPEAK/Speakeasy+Extension+Examples) for ideas.

Great, but what can they *NOT* do? Since no server-side code is allowed, your extension cannot:

-   Implement arbitrary application plugin modules
-   Access product information not exposed via REST, XML-RPC, or SOAP
-   Provide new URLs
-   Retrieve data from remote servers that don't support JSONP

You can work around the last two limitations if you get creative. In the first case, you can hijack an existing URL and pass additional data via query parameters or anchors, then rewriting the DOM. For the second, if the remote server is public, you can use YQL to access that server and repackage the data into JSONP.

## Getting started

To create your extension, you have two options: fork an existing plugin or start from scratch. For Codegeist all extensions will start from scratch.

{{% note %}}

To try out your idea, before getting into extension development and packaging, you may find it useful to use Firefox with the Firebug extension. With this, you can try out JavaScript scripts using its multi-line editor, running them on the current page. Once you work out all the kinks, you can follow these instructions to package it as a Speakeasy extension.

{{% /note %}}

### Starting from scratch

When starting from scratch, you can use the extension wizard to create a new conventions-based, or "zip", extension:

1.  [Install the Speakeasy plugin](/server/framework/atlassian-sdk/installing-speakeasy) on an instance of Confluence or JIRA
2.  Navigate to your Speakeasy page, by clicking "Extensions" in the username dropdown:  
    <img src="/server/framework/atlassian-sdk/images/extensions-link---jira.png" width="300" />

    {{% note %}}

    You may see a warning saying 'No one has access to this page. Click here to change these settings.' You'll need to click on the link to configure access for your extensions first before proceeding.

    {{% /note %}}

3.  To start creating your Extension, click on the **+ Install** button, and then click on the "use the wizard" link
4.  Fill in the key, name, and description of your new extension
5.  Click "submit" and you'll see your new extension in the list
6.  Click on "Enable" and refresh the page to see the banner your new extension is displaying

If you click on "Edit", you'll see this plugin have the following files, assuming your extension key is 'myext':

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p><strong>File</strong></p></th>
<th><p><strong>Description </strong></p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>atlassian-extension.json </p></td>
<td><p>The manifest for the extension.  The only required attributes are &quot;key&quot; and &quot;version&quot;. </p>
<p><strong>Required</strong></p></td>
</tr>
<tr class="even">
<td><p>screenshot.png</p></td>
<td><p>The screenshot to show in the extension list. Referred to in the descriptor. Must be a 175 x 80 pixel gif.</p></td>
</tr>
<tr class="odd">
<td><p>js/myext/main.js </p></td>
<td><p>The JavaScript module to execute on the default context of &quot;atl.general&quot;.  The example puts a banner on the top of every non-admin page with an image. </p></td>
</tr>
<tr class="even">
<td><p>css/main.css </p></td>
<td><p>The CSS file to be displayed whenever the JavaScript is executed.  The example hides the second banner that says &quot;Bye&quot;. </p></td>
</tr>
<tr class="odd">
<td><p>images/projectavatar.png </p></td>
<td><p>An image file that is referenced in the JavaScript </p></td>
</tr>
<tr class="even">
<td><p>ui/web-items.json </p></td>
<td><p>A list of web items.  The example is one that puts a &quot;Yahoo&quot; link on the Speakeasy page </p></td>
</tr>
</tbody>
</table>

### Getting started by forking an existing extension

If you see an extension you like and want to tweak, or just want to do something similar, you may want to fork an existing extension following these steps:

1.  Find an extension that you find useful but want to customise and click "Fork"
2.  Type a description of what this fork will do
3.  Click "Edit" to modify the extension right in the browser
4.  Press "Save" and try it out

Once you get the hang of it, you can create your own extension.

## Developing your extension

To develop your extension, you have two options: the web IDE or offline.

### Using the Web IDE

Speakeasy has a very simple text editor built into the plugin. With it, you can edit your extension right in the browser, with each save causing the plugin to be rebuilt and upgraded into the product. However, with this editor, you will be unable to delete, add, or rename files.

### Developing Offline

If you need to make several changes and don't want to interrupt your users, you can write your extension with just a text editor and a zip tool. These instructions assume working from the terminal, though GUI tools could be used as well.

1.  Find your extension on the Speakeasy page and click "Download"
2.  Click the "Download" link to download the artifact
3.  Unzip the artifact, whether it is a jar or zip, into a new directory
4.  With your text editor, start working on your extension
5.  When ready to test, run:

    ``` bash
    zip -r ../my-extension.zip *
    ```

    *Make sure you preserve your file extension*

6.  Visit the Speakeasy page in your target application and upload your newly created extension zip or jar.

Be aware that any upgrades or live edits to your extension will immediately be seen by all those that enabled your extension.

#### Using IDEA

If you want to use IDEA and have created a zip extension that doesn't include a "Download as SDK Project" link, you can still use IDEA to modify your extension:

1.  Download then unzip the extension to a new directory
2.  Create an IDEA project from existing sources
3.  Add the "js", "css", "ui", and "images" directories as source directories
4.  Now, you should be able to code like normal, using an external script for deployment

#### Using git

New in 0.10, you can interact with your extension via git as Speakeasy acts as a git server for each extension. Operations include:

1.  `git clone` - Checkout a copy of the extension repository ready for deployment
2.  `git pull` - Keep up-to-date with deployed versions as well as bring in changes from forking extensions
3.  `git push` - Deploy extension changes from the command-line

During development on a remote server, `git push` can be a useful technique for rapidly deploying locally-developed changes:

``` bash
git commit -a -m "Local changes" && git push
```

## Advanced Topics

This sections covered a few advanced topics you may encounter in Speakeasy development.

### Using Web Items

Web items are defined in the file `ui/web-items.json` as a list of web item objects. The following properties are allowed on web item objects:

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Name</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>section</p></td>
<td><p>Where the web item will show up.</p>
<p><strong>Required</strong></p></td>
</tr>
<tr class="even">
<td><p>label</p></td>
<td><p>The text to show for the web item.</p>
<p><strong>Required</strong></p></td>
</tr>
<tr class="odd">
<td><p>url</p></td>
<td><p>The URL for the link to point to.</p>
<p><strong>Required</strong></p></td>
</tr>
<tr class="even">
<td><p>cssId</p></td>
<td><p>The CSS ID of the link anchor (0.12.2 or later)</p></td>
</tr>
<tr class="odd">
<td><p>cssClass</p></td>
<td><p>The CSS class or set of classes for the link anchor</p></td>
</tr>
<tr class="even">
<td><p>weight</p></td>
<td><p>The weight of the web item</p></td>
</tr>
<tr class="odd">
<td><p>tooltip</p></td>
<td><p>The text to show for the tool tip, if applicable</p></td>
</tr>
<tr class="even">
<td><p>icon</p></td>
<td><p>The object describing the icon. Valid properties are:</p>
<ul>
<li><code>width</code> - The width of the icon</li>
<li><code>height</code> - The height of the icon</li>
<li><code>url</code> - The url of the icon</li>
</ul></td>
</tr>
</tbody>
</table>

### Referencing Images in CSS

{{% note %}}

This feature is new in version 0.9

{{% /note %}}

You can reference an image in your CSS by using a special token that will be replaced at runtime: @imagesPrefix. For example, you could refer to a background image in your CSS like this:

``` css
#foo {
 background-image: url(@imagesPrefix/myimage.png);
}
```

### Using CommonJS Modules

Your first plugin created with the extension wizard contains a JavaScript file that is loaded as a CommonJS module.  CommonJS is a set of standards for JavaScript, of which their Module spec is the one used here.  A module fundamentally can import other modules and selectively expose properties or functions to other modules.  Each module is loaded in its own scope, so you don't need to worry about global variable clashes.

#### Contextualizing modules

Entry point modules will need to tell Speakeasy on which page they should be included. This is done via the "@context" annotation in the top JavaDoc-style comment on the module. For example:

``` javascript
/**
 * @context dashboard
 */
... module code here ...
```

This example is configured to have its module loaded when on the Confluence dashboard page. These contexts are also known as 'web resource contexts', as they are the same used for scoping web resources such as JavaScript and CSS for normal Atlassian plugins. For more information about contexts, see the following links:

-   <a href="http://confluence.atlassian.com/display/PLUGINFRAMEWORK/Web+Resource+Plugin+Module#WebResourcePluginModule-WebResourceContexts" class="external-link">Contexts in all products</a>
-   <a href="http://confluence.atlassian.com/display/JIRA/Web+Resource+Plugin+Module#WebResourcePluginModule-WebResourceContextsinJIRA" class="external-link">JIRA contexts</a>
-   <a href="http://confluence.atlassian.com/display/CONFDEV/Web+Resource+Module#WebResourceModule-WebResourceContextsinConfluence" class="external-link">Confluence contexts</a>

#### Consuming modules

Most extensions will interact with CommonJS through consuming other modules, usually ones provided by Speakeasy.  The "CommonJS Modules" tab shows those and all other public modules available for consumption.

Modules can be consumed via the "require(moduleId)" syntax.  Here is an example of consuming the 'speakeasy/jquery' module, which exports the 'jQuery' property:

``` javascript
var $ = require('speakeasy/jquery').jQuery;
```

Module ids can be specified as absolute ids or relative to your current module. Therefore, if you had a module 'myext/util' that you wanted to consume from 'myext/main', you could consume it via:

``` javascript
var util = require('./util');
```

The right modules will be automatically delivered to your page via the Speakeasy plugin. Therefore, you don't need to worry whether the module is in your extension or another extension, although the end user will need to have enabled the dependent extension in order to use yours.

#### Providing modules

Modules are private to your extension by default. If you want to create a 'myext/util', just create a js/myext/util.js file in your extension and consume it from another module as described above. The goal is to make it really easy to decompose your extension into modules, making it easier to maintain and eventually share with others.

If you want to provide your module to other extensions, you can do so by adding the "@public" annotation to your module's JsDoc (the JavaDoc-like comment at the top):

``` javascript
/**
  * This is a public module
  * @public
  */
exports.foo = "Foo";
```

This module will now show up in the "CommonJS Modules" tab and be available for other extensions to import.

{{% note %}}

It is recommended that any hack you have to do to retrieve data from the application or manipulate the page be extracted into their own modules. This way, the extension is easier to maintain or tweak by forkers as the ugly bits aren't mixed in with the extension logic, and if you decide to share your hack, you already have a shareable module ready to annotate.

{{% /note %}}

### Using the Plugin SDK

If your extension is a "jar" extension, so in other words, a normal OSGi plugin that has an atlassian-plugin.xml, you can use the <a href="http://confluence.atlassian.com/display/DEVNET/Developing+your+Plugin+using+the+Atlassian+Plugin+SDK" class="external-link">Plugin SDK</a> to develop your extension.

1.  Click on the "Download" link by your extension and click "Download as SDK Project"
2.  Unzip the SDK Project into a new directory
3.  In a terminal window, run:

    ``` bash
    mvn confluence:run
    ```

    Note, replace "confluence" with the desired target product.

4.  In another terminal window, run:

    ``` bash
    mvn confluence:cli
    ```

    Again, replace "confluence" with the desired target product.

5.  Navigate to <a href="http://localhost:1990/confluence&amp;nbsp;in" class="uri external-link">http://localhost:1990/confluence&amp;nbsp;in</a> your browser. See the Plugin SDK docs for other product URLs.
6.  Login with a username of "admin" and password of "admin"
7.  Move your cursor to your username on the top banner and click "Speakeasy". You should see your extension.
8.  In your text editor, open files src/main/resources and start working on your extension. Most changes should be visible immediately, but others will require you to switch to your terminal window running the cli and enter 'pi'

If your extension is a "zip" extension, you can still use the Plugin SDK to develop your extension, albeit in a more limited fashion:

1.  Click on the "Download" link by your extension and click "Download"
2.  Unzip the artifact into a new directory
3.  Run <a href="http://confluence.atlassian.com/display/DEVNET/atlas-run-standalone" class="external-link">atlas-run-standalone</a> to start the Atlassian product. In this example, we start Confluence 3.5.3:

    ``` bash
    atlas-run-standalone --product confluence --version 3.5.2 --jvmargs "-Dplugin.resource.directories=. -Xmx512m -XX:MaxPermSize=128m" --plugins com.atlassian.labs:speakeasy-plugin:0.10.2
    ```

4.  Upload or push your extension to your local Confluence running at <a href="http://localhost:1990/confluence" class="uri external-link">http://localhost:1990/confluence</a> and start developing. JS and CSS changes that don't require a plugin reinstallation can be seen immediately via a reload (thanks to that 'plugin.resource.directories' system prop)

## Under the covers

A Speakeasy extension, at a technical level, is an OSGi plugin that contains only Speakeasy-provided dynamic module descriptors. These include:

-   scoped-web-resources
-   scoped-web-item
-   scoped-modules

The custom module types are necessary to ensure the plugin can be enabled on a per-user basis. Any other module descriptors, or even files considered not appropriate for such a plugin, will result in extension installation rejection. Inappropriate files include JAR files, Java class files, and Spring XML descriptor files. Since Speakeasy extensions are real plugins, they can be viewed, managed, and uninstalled from the Plugin Management UI in each product.

{{% note %}}

Keep in mind the idea is the application should work 100% correctly if your extension is not enabled. This means you shouldn't do things like create psuedo Confluence macros that show useful information for your extension users but blank screens or gibberish for all others.

{{% /note %}}



























