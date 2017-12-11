---
aliases:
- /server/framework/atlassian-sdk/-context-provider-element-852079.html
- /server/framework/atlassian-sdk/-context-provider-element-852079.md
category: devguide
confluence_id: 852079
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=852079
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=852079
date: '2017-12-11'
legacy_title: _Context-Provider Element
platform: server
product: atlassian-sdk
subcategory: other
title: _Context-Provider Element
---
# \_Context-Provider Element

|            |                                                                       |
|------------|-----------------------------------------------------------------------|
| Available: | Atlassian Plugins 2.5, Confluence 2.5, Bamboo 3.0, JIRA 4.2 and later |

The `context-provider` element must contain a class attribute with the fully-qualified name of a Java class. The referenced class:The context-provider element adds to the Velocity context available to the [web section](/server/framework/atlassian-sdk/web-section-plugin-module) and [web item](/server/framework/atlassian-sdk/web-item-plugin-module) modules. You can add what you need to the context, to build more flexible section and item elements. Currently only one context-provider can be specified per module. Additional context-providers are ignored.

-   must implement `com.atlassian.plugin.web.ContextProvider`, and
-   will be auto-wired by Spring before any additions to the Velocity context.

For example, the following context-provider will add `historyWindowHeight` and `filtersWindowHeight` to the context.

In the following example, `HeightContextProvider` extends `AbstractJiraContextProvider`, which is only available in JIRA and happens to implement `ContextProvider`. The `AbstractJiraContextProvider` conveniently extracts the `User` and `JiraHelper` from the context map, which you would otherwise have to do manually.

``` java
public class HeightContextProvider extends AbstractJiraContextProvider
{
    private final ApplicationProperties applicationProperties;

    public HeightContextProvider(ApplicationProperties applicationProperties)
    {
        this.applicationProperties = applicationProperties;
    }

    public Map getContextMap(User user, JiraHelper jiraHelper)
    {
        int historyIssues = 0;
        if (jiraHelper != null && jiraHelper.getRequest() != null)
        {
            UserHistory history = (UserHistory) jiraHelper.getRequest().getSession().getAttribute(SessionKeys.USER_ISSUE_HISTORY);
            if (history != null)
            {
                historyIssues = history.getIssues().size();
            }
        }
        int logoHeight = TextUtils.parseInt(applicationProperties.getDefaultBackedString(APKeys.JIRA_LF_LOGO_HEIGHT));
        String historyHeight = String.valueOf(80 + logoHeight + (25 * historyIssues));
        String filterHeight = String.valueOf(205 + logoHeight);
        return EasyMap.build("historyWindowHeight", historyHeight,
                             "filtersWindowHeight", filterHeight);
    }
}
```

The above `HeightContextProvider` can be used by nesting the following element in a web item module.

``` xml
<context-provider class="com.atlassian.jira.plugin.web.contextproviders.HeightContextProvider" />
```

The newly added context entries `historyWindowHeight` and `filtersWindowHeight` can be used in the XML module descriptors just like normal velocity context variables, by prefixing them with the dollar symbol ($):

``` xml
<!-- pass the value of historyWindowHeight as a parameter called windowHeight (see param element above for its usage) -->
<param name="windowHeight">$historyWindowHeight</param>

<!-- set the link's label to print the value of filtersWindowHeight -->
<label>filter window height is: $filtersWindowHeight</label>
```










































