---
aliases:
- /server/framework/atlassian-sdk/extending-the-speakeasy-plugin-2818151.html
- /server/framework/atlassian-sdk/extending-the-speakeasy-plugin-2818151.md
category: devguide
confluence_id: 2818151
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818151
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818151
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: Extending the Speakeasy Plugin 2818151
---
# Extending the Speakeasy plugin

If you so desire to improve the Speakeasy plugin itself, here are some steps to do so. Note that you don't need to hack on the Speakeasy plugin to enter the contest.

Take the following steps to install the Speakeasy plugin:

1.  Clone (or fork) the <a href="https://github.com/mrdon/speakeasy-plugin" class="external-link">github speakeasy-plugin</a> project via:

    ``` bash
    git clone https://github.com/mrdon/speakeasy-plugin.git
    ```

2.  Start the plugin in the desired product:
    -   Refapp:

        ``` bash
        mvn refapp:debug
        ```

    -   Confluence:

        ``` bash
        mvn refapp:debug -Dproduct=confluence
        ```

    -   JIRA:

        ``` bash
        mvn refapp:debug -Dproduct=jira
        ```

3.  Open pom.xml in IDEA
4.  Start the cli for rapid deployments:
    -   Refapp:

        ``` bash
        mvn refapp:cli
        ```

    -   Confluence:

        ``` bash
        mvn refapp:cli -Dproduct=confluence
        ```

    -   JIRA:

        ``` bash
        mvn refapp:cli -Dproduct=jira
        ```

5.  Visit the user profile page of Speakeasy:
    -   Refapp:

        ``` bash
        firefox http://localhost:5990/refapp/plugins/servlet/speakeasy/user
        ```

    -   Confluence:

        ``` bash
        firefox http://localhost:1990/confluence/plugins/servlet/speakeasy/user
        ```

    -   JIRA:

        ``` bash
        firefox http://localhost:2990/jira/plugins/servlet/speakeasy/user
        ```

To try out extensions, you can create a new one or work on the testing plugin found in src/test/resources. It is deployed via the tpi cli command (stands for 'test plugin install')









































































































































































































































































































