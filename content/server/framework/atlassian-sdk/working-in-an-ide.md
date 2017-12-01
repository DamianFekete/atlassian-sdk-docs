---
aliases:
- /server/framework/atlassian-sdk/working-in-an-ide-2818616.html
- /server/framework/atlassian-sdk/working-in-an-ide-2818616.md
category: devguide
confluence_id: 2818616
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818616
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818616
learning: guides
legacy_url: https://developer.atlassian.com/docs/developer-tools/working-in-an-ide
new_url: /server/framework/atlassian-sdk/working-in-an-ide
platform: server
product: atlassian-sdk
subcategory: learning
title: Working in an IDE
---
# Working in an IDE

Most developers are accustomed to working within an IDE. The [getting started tutorial](https://developer.atlassian.com/display/DOCS/Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project) describes how to set up the project in Eclipse in [Windows](https://developer.atlassian.com/display/DOCS/Set+Up+the+Eclipse+IDE+for+Windows) and in [Linux](https://developer.atlassian.com/display/DOCS/Set+Up+the+Eclipse+IDE+for+Linux). If you are using **IntelliJ IDEA**, just open the POM in your IDE following [Configure IDEA to use the SDK](/server/framework/atlassian-sdk/configure-idea-to-use-the-sdk). If you are using **NetBeans**, see [Configure NetBeans to use the SDK](/server/framework/atlassian-sdk/configure-netbeans-to-use-the-sdk).

## What's happening

In general, IDEs use the project POM file to generate the resource files it understands to be a development project. When you import an Atlassian Plugins SDK project into an IDE, Maven downloads all of the dependencies referenced in your `pom.xml`, and then all the inherited dependencies from the parent POMs (unless it has already done so).

Your `settings.xml` specifies that Maven should download the JavaDoc and source artifacts as well, where available. This is likely to take quite a while. Depending on your plugin's host application, Maven will now download 100MB or more from the internet. Go relax, get some tea or coffee, read a blog. Fortunately, after you've downloaded these files for the first time, they are stored in your local Maven repository (`$HOME/.m2/repository/`) and need not be downloaded again unless they change.

After this is complete, Maven will construct project files that your IDE can understand. It will reference all the dependent JARs in the right projects, and attach the sources and Javadoc where they are available. Don't forget, when you're ready to check in your plugin, do not commit these project files. They are specific to each IDE and to your specific development environment.

## More information

The following pages provide additional information on using the Atlassian Plugins SDK with an IDE:

-   [Configure IDEA to use the SDK](/server/framework/atlassian-sdk/configure-idea-to-use-the-sdk)
-   [Configure NetBeans to use the SDK](/server/framework/atlassian-sdk/configure-netbeans-to-use-the-sdk)
-   [Creating a Remote Debug Target](/server/framework/atlassian-sdk/creating-a-remote-debug-target)























































































































































