---
aliases:
- /server/framework/atlassian-sdk/plugin-module-index-2818387.html
- /server/framework/atlassian-sdk/plugin-module-index-2818387.md
category: reference
confluence_id: 2818387
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818387
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818387
legacy_url: https://developer.atlassian.com/docs/getting-started/plugin-modules/plugin-module-index
new_url: /server/framework/atlassian-sdk/plugin-module-index
platform: server
product: atlassian-sdk
subcategory: modules
title: Plugin module Index
---
# Plugin module Index

 

# What this is

This page lists the plugin modules for Atlassian applications. The idea is for the plugin developer to quickly identify the plugin module they need and give them an outline of what to expect and what they can change.

Each plugin module listed here comes with:

-   A brief description of what it's for
-   Glosses for the crucial configuration elements
-   An example of its use in `atlassian-plugin.xml`

The name of each module is a link to its full description in the product development hub. If you decide to write one of the modules listed below, you **must** read the full description at the link to succeed.

## Modules common to all applications

These modules are provided by the plugin framework and operate identically in all applications.

### Code sharing

The [DEVNET:Component](#devnet:component) and [DEVNET:Component Import](#devnet:component-import) module types are for modularizing and sharing code within a plugin and between plugins:

#### [Component](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Component+Plugin+Module)

Declares that a class in the plugin is available for dependency injection within that plugin, and optionally, available for dependency injection in other plugins in the application.

**Frequently used attributes:**

-   `class`: The class providing the implementation for the component to inject.
-   `public`: Whether this implementation is available for dependency injection into other plugins, via the [DEVNET:Component Import](#devnet:component-import) declaration.

**Frequently used elements:**

-   `interface`: The interface for the component to inject.

 

**Example 1**

``` xml
<!-- declare a component for injection in this plugin -->
<component
    key="helloWorldService"
    class="com.myapp.DefaultHelloWorldService">
  <description>Provides hello services.</description>
  <interface>com.myapp.HelloWorldService</interface>
</component>
```

**Example 2**

``` xml
<!-- declare a component shared with other plugins -->
<component
    key="goodbyeWorldService"
    class="com.myapp.DefaultGoodbyeWorldService"
    public="true">
  <description>Provides goodbye services.</description>
  <interface>com.myapp.GoodbyeWorldService</interface>
</component>
```

------------------------------------------------------------------------

#### [Component Import](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Component+Import+Plugin+Module)

Requests that some implementation of a specific interface, exported either by another plugin using a [DEVNET:Component](#devnet:component) declaration or by the host application, be made available for dependency injection into this plugin.

**Frequently used attributes:**

-   `interface`: The interface for the component to inject.

**Frequently used elements:**

-   `interface`: The interface for the component to inject (identical to the `interface` attribute).

 

 

**Example**

``` xml
<!-- import a component shared by another plugin -->
<component-import
    key="helloWorldService"
    interface="com.myapp.HelloWorldService">
  <description>Provides hello services.</description>
</component>
```

------------------------------------------------------------------------

### JEE container integration

#### [Servlet Context Listener](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Servlet+Context+Listener+Plugin+Module)

Deploys the specified class as a <a href="http://download.oracle.com/javaee/6/api/javax/servlet/ServletContextListener.html" class="external-link">Java EE servlet context listener</a>.

**Frequently used attributes:**

-   `class`: The class to use as a servlet context listener.

 

 

**Example**

``` xml
<!-- declare a custom servlet context listener -->
<servlet-context-listener
    key="myServletContextListener"
    interface="com.myapp.MyServletContextListener">
  <description>Custom listener for the servlet context in this application.</description>
</servlet-context-listener>
```

 

 

------------------------------------------------------------------------

#### [Servlet Context Parameter](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Servlet+Context+Parameter+Plugin+Module)

Sets the specified name and value as a parameter in the <a href="http://download.oracle.com/javaee/6/api/javax/servlet/ServletContext.html" class="external-link">Java EE servlet context</a>.

**Frequently used elements:**

-   `param-name`: The name of the parameter.
-   `param-value`: The value of the parameter.

 

 

**Example**

``` xml
<!-- declare a custom servlet context parameter -->
<servlet-context-param
    key="myServletContextParam">
  <description>Custom parameter for the servlet context in this application.</description>
  <param-name>myParam</param-name>
  <param-value>myParamValue</param-value>
</servlet-context-param>
```

------------------------------------------------------------------------

#### [Servlet Filter](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Servlet+Filter+Plugin+Module)

Deploys the specified <a href="http://download.oracle.com/javaee/6/api/javax/servlet/Filter.html" class="external-link">Java EE servlet filter</a> in the product.

**Frequently used attributes:**

-   `class`: The class to use as a servlet filter,

**Frequently used elements:**

-   `url-pattern`: The URL pattern this servlet filter should be applied to.

 

 

**Example**

``` xml
<!-- declare a custom servlet filter -->
<servlet-filter
    key="myServletFilter"
    class="com.myapp.MyServletFilter">
  <description>Custom parameter for the servlet context in this application.</description>
  <url-pattern>/myapp</url-pattern>
</servlet-filter>
```

 

 

------------------------------------------------------------------------

#### [Servlet](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Servlet+Plugin+Module)

Deploys the specified <a href="http://download.oracle.com/javaee/6/api/javax/servlet/Servlet.html" class="external-link">Java EE servlet</a> in the product.

**Frequently used attributes:**

-   `class`: The servlet class to use.

**Frequently used elements:**

-   `url-pattern`: The URL pattern this servlet should be deployed to.

 

 

**Example**

``` xml
<!-- declare a custom servlet filter -->
<servlet
    key="myServletFilter"
    class="com.myapp.MyServlet">
  <description>Servlet to deploy in this application.</description>
  <url-pattern>/myapp</url-pattern>
</servlet>
```

 

 

------------------------------------------------------------------------

### User interface

#### [Web Item](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Web+Item+Plugin+Module)

Defines a new link in an application menu.

**Frequently used attributes:**

-   `section`: The [DEVNET:web section](#devnet:web-section) to insert this web item into.

**Frequently used elements:**

-   `label`: Points to an internationalized resource property that contains the display text of the link.
-   `link`: Defines where the link should point.

 

 

**Example**

``` xml
<!-- declare a web item -->
<web-item
    key="myWebItem"
    section="system.admin/example1">
  <description>Example link appearing in the system admin menu.</description>
  <label key="atlassian.home"/>
  <link>http://atlassian.com</link>
</web-item>
```

 

 

------------------------------------------------------------------------

#### [Web Section](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Web+Section+Plugin+Module)

Defines a new section in an application menu.

**Frequently used attributes:**

-   `section`: The [DEVNET:web section](#devnet:web-section) to insert this web section into.
-   `weight`: The order in which this section should appear in the menu relative to other items; heavier weights display lower in the menu.

**Frequently used elements:**

-   `label`: Points to an internationalized resource property that contains the user-visible name of this section.

 

 

**Example**

``` xml
<!-- declare a web section -->
<web-section
    key="myWebItem"
    section="system.admin/example1"
    weight="100">
  <description>Example web section appearing in the system admin menu.</description>
  <label key="example1.web.section.name"/>
</web-section>
```

 

 

------------------------------------------------------------------------

#### [Web Panel](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Web+Panel+Plugin+Module)

Defines a web panel - a set of HTML content that can be inserted verbatim into a page.

**Frequently used attributes:**

-   `location`: The product-specific location to insert this web section. Locations are different between products.

**Frequently used elements:**

-   `resource`: The HTML [resource](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Adding+Resources+to+your+Project) to use for the panel's contents.

 

 

**Example**

``` xml
<!-- declare a web panel -->
<web-panel
    key="myWebPanel"
    location="atl.confluence.comments">
  <description>Example web panel appearing in the Confluence comments.</description>
  <resource name="view" type="velocity" location="templates/comments-web-panel.vm"/>
</web-panel>
```

 

 

------------------------------------------------------------------------

#### [Web Panel Renderer](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Web+Panel+Renderer+Plugin+Module)

Defines a custom rendering engine for a `<web-panel>`.

**Frequently used attributes:**

-   `class`: The class that implements the web panel renderer.

 

 

**Example**

``` xml
<!-- web panel renderer example -->
<web-panel-renderer
    key="myWebPanelRenderer"
    class="com.myapp.FreemarkerWebPanelRenderer"/>
```

 

 

------------------------------------------------------------------------

#### [Web Resource](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Web+Resource+Plugin+Module)

Defines downloadable resources (files) for a plugin, such as CSS or JavaScript files.

**Frequently used elements:**

-   `resource`: Specifies the [resources](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Adding+Resources+to+your+Project) that should be made available for download.

 

 

**Example**

``` xml
<!-- web resource example -->
<web-resource
    key="myWebResources">
  <resource name="mylib.js" type="download" location="js/mylib.js"/>
  <resource name="mylib2.js" type="download" location="js/mylib2.js"/>
</web-resources>
```

 

 

------------------------------------------------------------------------

#### [Web Resource Transformer](https://developer.atlassian.com/display/PLUGINFRAMEWORK/Web+Resource+Transformer+Plugin+Module) 

Defines transformers which allow changing web resources before being served to the browser.

**Frequently used attributes:**

-   `class`: The class to create and use as a transformer.

 

 

**Example**

``` xml
<!-- web resource transformer example -->
<web-resource-transformer
  key="template"
  class="com.atlassian.labs.template.TemplateTransformer" />
```

 

 

------------------------------------------------------------------------

### Other types

#### <a href="/pages/createpage.action?spaceKey=PLUGINFRAMEWORK&amp;title=REST+Plugin+Module" class="createlink">REST</a>

Exposes data and services as REST resources.

**Frequently used attributes:**

-   `path`: Path to the API defined by these resources.
-   `version`: Version of the REST API being exposed at this path.

 

 

**Example**

``` xml
<!-- REST module example -->
<rest
  key="helloWorldRest"
  path="/helloworld"
  version="1.0">
  <description>Provides hello world services.</description>
</rest>
```

 

 

------------------------------------------------------------------------

#### [Gadget](https://developer.atlassian.com/display/GADGETS)

Defines an <a href="http://confluence.atlassian.com/display/GADGETS" class="external-link">Atlassian gadget</a> provided by this plugin.

**Frequently used attributes:**

-   `location`: Path to the gadget XML specification in this plugin.

 

 

**Example**

``` xml
<!-- gadget module example -->
<gadget
  key="myGadget"
  location="gadgets/public/myGadget.xml"/>
```

 

 

## Product-specific modules

These modules are unique to the product they originate in.

## JIRA

### Adding custom remote APIs

#### [SOAP](https://developer.atlassian.com/display/JIRADEV/RPC+Endpoint+Plugin+Module)

{{% warning %}}

JIRA's SOAP and XML-RPC remote APIs will be deprecated in JIRA 6.0.

[Read the announcement for more information.](https://developer.atlassian.com/display/JIRADEV/SOAP+and+XML-RPC+API+Deprecation+Notice)

{{% /warning %}}

Adds custom SOAP services to JIRA in addition to the [builtin SOAP services](https://developer.atlassian.com/display/JIRADEV/JIRA+RPC+Services). 

**Frequently used attributes:**

-   `class`: The SOAP service implementing the published interface (see below).

**Frequently used elements:**

-   `service-path`: The path (under /rpc/soap) the service will be published at.
-   `published-interface`: The interface implemented by the service class and exposed to the end user.

 

 

**Example**

``` xml
<rpc-soap
  key="mySoapService"
  class="com.myapp.MySoapServiceImpl">
    <description>Custom SOAP services for this installation.</description>
    <service-path>customsoap-v1</service-path>
    <published-interface>
        com.myapp.MySoapService
    </published-interface>
</rpc-soap>
```

 

 

------------------------------------------------------------------------

#### [XML-RPC](https://developer.atlassian.com/display/JIRADEV/RPC+Endpoint+Plugin+Module)

{{% warning %}}

JIRA's SOAP and XML-RPC remote APIs will be deprecated in JIRA 6.0.

[Read the announcement for more information.](https://developer.atlassian.com/display/JIRADEV/SOAP+and+XML-RPC+API+Deprecation+Notice)

{{% /warning %}}

Adds custom XML-RPC services to JIRA in addition to the [builtin XML-RPC service](https://developer.atlassian.com/display/JIRADEV/JIRA+RPC+Services). 

**Frequently used attributes:**

-   `class`: The class to publish as an XML-RPC service

**Frequently used elements:**

-   `service-path`: The path (under /rpc/xmlrpc) the service will be published at.

 

 

**Example**

``` xml
<rpc-xmlrpc
  key="myXmlRpcService"
  class="com.myapp.MyXmlRpcService">
    <description>Custom XML-RPC services for this installation.</description>
    <service-path>custom-xmlrpc</service-path>
</rpc-xmlrpc>
```

 

 

------------------------------------------------------------------------

### Adding operations to tabs, views or screens

#### [Project tab panel](https://developer.atlassian.com/display/JIRADEV/Project+Tab+Panel+Plugin+Module)

Adds new tabs to the <a href="#browse-projects" class="unresolved">Browse Projects</a> page. 

**Frequently used attributes:**

-   `class`: The class implementing the project tab panel.

**Frequently used elements:**

-   `label`: The user-visible name of the label on the page. Can be specified directly in the element content or picked up from the i18n resource by attribute key.
-   `order`: The order in which the label should appear in the menu.
-   `resource` (velocity): The template which renders the HTML for the project tab.
-   `resource` (i18n): The .properties file containing i18n values for user-visible text.

 

 

**Example**

``` xml
<project-tabpanel key="roadmap-panel" name="Road Map Panel"
  class="com.atlassian.jira.plugin.projectpanel.impl.VersionsProjectTabPanel">
    <description key="projectpanels.roadmap.description">
      A roadmap of the upcoming versions in this project.
    </description>
    <label key="common.concepts.roadmap" />
    <order>20</order>
    <resource type="velocity" name="view"
      location="templates/plugins/jira/projectpanels/roadmap-panel.vm" />
    <resource type="i18n" name="i18n"
      location="com.atlassian.jira.plugins.projectpanels.roadmap" />
</project-tabpanel>
```

 

 

------------------------------------------------------------------------

#### [Component tab panel](https://developer.atlassian.com/display/JIRADEV/Component+Tab+Panel+Plugin+Module)

Adds new tabs to the <a href="#browse-projects" class="unresolved">Browse Component</a> page. 

**Frequently used attributes:**

-   {{class: The class implementing the component tab panel.

**Frequently used elements:**

-   `label`: The user-visible name of the label on the page. Can be specified directly in the element content or picked up from the i18n resource by attribute key.
-   `order`: The order in which the label should appear in the menu.
-   `resource` (velocity): The template which renders the HTML for the component tab.
-   `resource` (i18n): The .properties file containing i18n values for user-visible text.

 

 

**Example**

``` xml
<!-- module example -->
<component-tabpanel
  key="component-openissues-panel"
  i18n-name-key="componentpanels.openissues.name"
  name="Open Issues Panel"
  class="com.atlassian.jira.plugin.componentpanel.impl.GenericTabPanel">
    <description
      key="componentpanels.openissues.description">
      Show the open issues for this component.
    </description>
    <label key="common.concepts.openissues"/>
    <order>10</order>
    <resource type="velocity" name="view"
      location="templates/plugins/jira/projectentitypanels/openissues-component-panel.vm"/>
    <resource type="i18n" name="i18n"
      location="com.atlassian.jira.plugins.componentpanels.openissues"/>
</component-tabpanel>
```

 

 

------------------------------------------------------------------------

#### [Version tab panel](https://developer.atlassian.com/display/JIRADEV/Version+Tab+Panel+Plugin+Module)

Adds new tabs to the <a href="#browse-projects" class="unresolved">Browse Version</a> page. 

**Frequently used attributes:**

-   `class`: The class implementing the version tab panel.

**Frequently used elements:**

-   `label`: The user-visible name of the label on the page. Can be specified directly in the element content or picked up from the i18n resource by attribute key.
-   `order`: The order in which the label should appear in the menu.
-   `resource` (velocity): The template which renders the HTML for the version tab.
-   `resource` (i18n): The .properties file containing i18n values for user-visible text.

 

 

**Example**

``` xml
<!-- module example -->
<version-tabpanel
  key="version-openissues-panel"
  i18n-name-key="versionpanels.openissues.name"
  name="Open Issues Panel"
  class="com.atlassian.jira.plugin.versionpanel.impl.GenericTabPanel">
    <description key="versionpanels.openissues.description">Show the open issues for this version.</description>
    <label key="common.concepts.openissues"/>
    <order>10</order>
    <resource type="velocity" name="view"
      location="templates/plugins/jira/projectentitypanels/openissues-version-panel.vm"/>
    <resource type="i18n" name="i18n" location="com.atlassian.jira.plugins.versionpanels.openissues"/>
</version-tabpanel>
```

 

 

------------------------------------------------------------------------

#### [Issue tab panel](https://developer.atlassian.com/display/JIRADEV/Issue+Tab+Panel+Plugin+Module)

Adds new tabs to the <a href="#browse-projects" class="unresolved">View Issue</a> panel. 

**Frequently used attributes:**

-   {{class}: The class implementing the issue tab panel.

**Frequently used elements:**

-   `label`: The user-visible name of the label on the page.
-   `resource`: The template which renders the HTML for the issue tab.

 

 

**Example**

``` xml
<!-- issue tab panel example -->
<issue-tabpanel
  key="environment-tabpanel"
  name="Environment Tab Panel"
  class="com.icontact.jira.environmentmanor.issuetabpanels.EnvironmentPanelPlugin">
   <description>Show Environment Status and controls in an issue tab panel.</description>
   <label>Environment Control Panel</label>
   <resource type="velocity" name="view"
     location="templates/plugins/environmentmanor/issuetabpanels/environment.vm"/>
</issue-tabpanel>
```

 

 

------------------------------------------------------------------------

#### [Search request view](https://developer.atlassian.com/display/JIRADEV/Search+Request+View+Plugin+Module)

Allows display of search results in the <a href="#browse-projects" class="unresolved">issue navigator</a> in custom formats (such as XML or MS Excel format).

**Frequently used attributes:**

-   `class`: The class implementing the search request view.
-   `contentType`: The MIME content type to return when displaying this view.

**Frequently used elements:**

-   `resource` (header): The header to render for this view.
-   `resource` (singleissue): What to render for each individual issue in this view.
-   `resource` (footer): The footer to render for this view.

 

 

**Example**

``` xml
<!-- search request view example -->
<search-request-view
  key="simple-searchrequest-xml"
  name="Simple XML"
  class="com.atlassian.jira.sample.searchrequest.SimpleSearchRequestXmlView"
  state='enabled'
  fileExtension="xml"
  contentType="text/xml">
    <resource type="velocity" name="header" location="templates/searchrequest-xml-header.vm"/>
    <resource type="velocity" name="singleissue" location="templates/searchrequest-xml-singleissue.vm"/>
    <resource type="velocity" name="footer" location="templates/searchrequest-xml-footer.vm"/>
    <order>100</order>
</search-request-view>
```

 

 

------------------------------------------------------------------------

### Custom workflow operations

#### [Workflow conditions](https://developer.atlassian.com/display/JIRADEV/Workflow+Plugin+Modules#WorkflowPluginModules-Conditions)

Checks whether a user can perform a <a href="#browse-projects" class="unresolved">workflow transition</a>.

**Frequently used attributes:**

-   `class`: The class implementing the workflow condition (usually a builtin product class rather than one the plugin developer writes)

**Frequently used elements:**

-   `condition-class`: The class implementing the condition's logic.
-   `resource`: Renders the view for the condition.

 

 

**Example**

``` xml
<!-- workflow condition example -->
<workflow-condition key="onlyassignee-condition"
  name="Only Assignee Condition"
  i18n-name-key="admin.workflow.condition.onlyassignee.display.name"
  class="com.atlassian.jira.plugin.workflow.WorkflowAllowOnlyAssigneeConditionFactoryImpl">
    <description key="admin.workflow.condition.onlyassignee">Condition to allow only the assignee to execute a transition.</description>
    <condition-class>com.atlassian.jira.workflow.condition.AllowOnlyAssignee</condition-class>
    <resource type="velocity" name="view"
        location="templates/jira/workflow/com/atlassian/jira/plugin/onlyassignee-condition-view.vm"/>
</workflow-condition>
```

 

 

------------------------------------------------------------------------

#### [Workflow validators](https://developer.atlassian.com/display/JIRADEV/Workflow+Plugin+Modules#WorkflowPluginModules-Validators)

Checks that the data supplied to a workflow transition is valid.

**Frequently used attributes:**

-   `class`: The class implementing the workflow validator (usually a builtin product class rather than one the plugin developer writes)

**Frequently used elements:**

-   `validator-class`: The class implementing the validator's logic.
-   `resource`: Renders the view for the condition.

 

 

**Example**

``` xml
<!-- workflow validator example -->
<workflow-validator
  key="permission-validator"
  name="Permission Validator"
  class="com.atlassian.jira.plugin.workflow.WorkflowPermissionValidatorPluginFactory">
    <description>Validates that the user has a permission.</description>
    <validator-class>
        com.atlassian.jira.workflow.validator.PermissionValidator
    </validator-class>
    <resource type="velocity" name="view"
        location="templates/jira/.../permission-validator-view.vm"/>
    <resource type="velocity" name="input-parameters"
        location="templates/jira/.../permission-validator-input-params.vm"/>
</workflow-validator>
```

 

 

------------------------------------------------------------------------

#### [Workflow functions](https://developer.atlassian.com/display/JIRADEV/Workflow+Plugin+Modules#WorkflowPluginModules-Functions)

Performs actions after a workflow transition has executed.

**Frequently used attributes:**

-   `class`: The class implementing the workflow function (usually a builtin product class rather than one the plugin developer writes)

**Frequently used elements:**

-   `function-class`: The class implementing the function's logic.
-   `resource`: Renders the view for the condition.

 

 

**Example**

``` xml
<!-- workflow function example -->
<workflow-function key="update-issue-field-function"
  name="Update Issue Field"
  class="com.atlassian.jira.plugin.workflow.UpdateIssueFieldFunctionPluginFactory">
    <description>Updates a simple issue field to a given value.</description>
    <function-class>
        com.atlassian.jira.workflow.function.issue.UpdateIssueFieldFunction
    </function-class>
    <orderable>true</orderable>
    <unique>false</unique>
    <deletable>true</deletable>
    <resource type="velocity" name="view"
        location="templates/jira/.../update-issue-field-function-view.vm"/>
    <resource type="velocity" name="input-parameters"
        location="templates/jira/.../update-issue-field-function-input-params.vm"/>
</workflow-function>
```

 

 

------------------------------------------------------------------------

### Custom fields

#### [Custom field types](https://developer.atlassian.com/display/JIRADEV/Custom+field+plugin+module)

Defines a <a href="#browse-projects" class="unresolved">custom field</a> and its type.

**Frequently used attributes:**

-   `class`: The class that implements the custom field and its behaviors.

**Frequently used elements:**

-   `resource` (view): Template for rendering this custom field on the View Issue page.
-   `resource` (edit-userpicker): Template for rendering this custom field on the Create/Edit Issue page.
-   `resource` (xml): Template for rendering this custom field in XML.

 

 

**Example**

``` xml
<!-- custom field type example -->
<customfield-type key="userpicker" name="User Picker"
class="com.atlassian.jira.issue.customfields.impl.UserCFType">
   <description>
      Choose a user from the user base via a popup picker window.
   </description>
   <resource type="velocity" name="view"
     location="templates/plugins/fields/view-user.vm" />
   <resource type="velocity" name="edit"
     location="templates/plugins/fields/edit-userpicker.vm" />
   <resource type="velocity" name="xml"
     location="templates/plugins/fields/xml-user.vm" />
</customfield-type>
```

 

 

------------------------------------------------------------------------

#### [Custom field searchers](https://developer.atlassian.com/display/JIRADEV/Custom+field+plugin+module)

Defines a search method for indexing a custom field.

**Frequently used attributes:**

-   `class`: The class implementing this custom field searcher.

**Frequently used elements:**

-   `valid-customfield-type`: Defines the custom field this searcher applies to.
-   `resource`: Renders this searcher on the issue navigator search form.

 

 

**Example**

``` xml
<!-- custom field searcher example -->
<customfield-searcher key="userpickersearcher" name="User Picker Searcher"
class="com.atlassian.jira.issue.customfields.searchers.UserPickerSearcher">
   <description>
      Allow to search for a user using a userpicker.
   </description>
   <resource type="velocity" name="search"
     location="templates/plugins/fields/search-userpicker.vm" />
   <valid-customfield-type
     package="com.atlassian.jira.plugin.system.customfieldtypes" key="userpicker" />
</customfield-searcher>
```

 

 

------------------------------------------------------------------------

### Other types

#### [Reports](https://developer.atlassian.com/display/JIRADEV/Report+Plugin+Module)

Defines a <a href="#browse-projects" class="unresolved">report</a> in JIRA.

**Frequently used attributes:**

-   `class`: The class implementing this report.

**Frequently used elements:**

-   `label`: The user-visible name of the label on the page.
-   `resource` (view): Renders the HTML version of the report.
-   `resource` (i18n): Provides the i18n values for the keys in the report displays.
-   `properties`: Properties this report requires to run correctly.

 

 

**Example**

``` xml
<!-- report example -->
<report key="time-tracking"
  name="Time Tracking Report"
  class="com.atlassian.jira.plugin.report.impl.TimeTrackingReport">
    <description key="report.timetracking.description">
        This report shows the time tracking details for a specific project.
    </description>
    <label key="report.timetracking.label" />
    <resource type="velocity" name="view"
        location="templates/plugins/jira/reports/time-tracking-report.vm" />
    <resource type="i18n" name="i18n"
        location="com.atlassian.jira.plugins.reports.timetracking" />
    <properties>
        <property>
            <key>versionId</key>
            <name>common.concepts.version</name>
            <description>report.timetracking.version.description</description>
            <type>select</type>
            <values class="com.atlassian.jira.portal.VersionOptionalValuesGenerator"/>
        </property>
    </properties>
</report>
```

 

 

------------------------------------------------------------------------

#### [Custom actions](https://developer.atlassian.com/display/JIRADEV/Webwork+plugin+module)

Defines custom WebWork actions (functionality that can be triggered by visiting a URL) or overrides an existing JIRA action.

**Frequently used elements:**

-   `actions`: Defines the WebWork actions this module will provide.

 

 

**Example**

``` xml
<!-- webwork example -->
<webwork1
  key="qquserissue"
  name="Quick Create User Issue"
  class="java.lang.Object">
    <actions>
        <action
          name="com.atlassian.jira.toolkit.action.QuickCreateUserIssueAction"
          alias="QuickCreateUserIssue">
            <view name="createuserissue">/templates/quickcreateuser.vm</view>
        </action>
    </actions>
</webwork1>
```

 

 

------------------------------------------------------------------------

#### [JQL functions](https://developer.atlassian.com/display/JIRADEV/JQL+Function+Plugin+Module)

Defines new functions for use in the <a href="#browse-projects" class="unresolved">JIRA Query Language (JQL)</a>.

**Frequently used attributes:**

-   `class`: The class implementing the JQL function logic.

**Frequently used elements:**

 

 

**Example**

``` xml
<!-- jql example -->
<jql-function
  key="role-members"
  i18n-name-key="rolefunc.name"
  name="Role Members Function"
  class="com.atlassian.example.jira.jqlfunc.RoleFunction">
    <resource type="i18n" name="i18n"
      location="com.atlassian.example.jira.jqlfunc.RoleFunction" />
    <description key="rolefunc.description">
      JQL function to return the members of a particular role
    </description>
</jql-function>
```

 

 

------------------------------------------------------------------------

## Confluence

### Custom remote APIs

#### [SOAP](https://developer.atlassian.com/display/CONFDEV/RPC+Module)

Adds custom SOAP services to Confluence in addition to the [builtin SOAP services](https://developer.atlassian.com/display/CONFDEV/Confluence+XML-RPC+and+SOAP+APIs).

**Frequently used attributes:**

-   `class`: The SOAP service implementing the published interface (see below).

**Frequently used elements:**

-   `service-path`: The path (under /rpc/soap) the service will be published at.
-   `published-interface`: The interface implemented by the service class and exposed to the end user.

 

 

**Example**

``` xml
<!-- SOAP example -->
<rpc-soap
  key="mySoapService"
  class="com.myapp.MySoapServiceImpl">
    <description>Custom SOAP services for this installation.</description>
    <service-path>customsoap-v1</service-path>
    <published-interface>
        com.myapp.MySoapService
    </published-interface>
</rpc-soap>
```

 

 

------------------------------------------------------------------------

#### [XML-RPC](https://developer.atlassian.com/display/CONFDEV/RPC+Module)

Adds custom XML-RPC services to Confluence in addition to the [builtin XML-RPC service](https://developer.atlassian.com/display/CONFDEV/Confluence+XML-RPC+and+SOAP+APIs).

**Frequently used attributes:**

-   `class`: The class to publish as an XML-RPC service

**Frequently used elements:**

-   `service-path`: The path (under /rpc/xmlrpc) the service will be published at.

 

 

**Example**

``` xml
<rpc-xmlrpc
  key="myXmlRpcService"
  class="com.myapp.MyXmlRpcService">
    <description>Custom XML-RPC services for this installation.</description>
    <service-path>custom-xmlrpc</service-path>
</rpc-xmlrpc>
```

 

 

------------------------------------------------------------------------

### Custom markup

#### [User macros](https://developer.atlassian.com/display/CONFDEV/User+Macro+Module)

Defines simple <a href="#browse-projects" class="unresolved">user macros</a> as plugin modules without requiring any new Java code. 

**Frequently used elements:**

-   `template`: The body of the user macro (in HTML). Can access the Velocity context.

 

 

**Example**

``` xml
<!-- user macro example -->
<user-macro
  name='helloworld'
  key='helloworld'>
    <description>Hello, user macro</description>
    <template><![CDATA[Hello, $body!]]></template>
</user-macro>
```

 

 

------------------------------------------------------------------------

#### [Custom macros](https://developer.atlassian.com/display/CONFDEV/Macro+Module)

Defines a <a href="#browse-projects" class="unresolved">macro</a> -- a piece of code that can be invoked from inside a page. Usually this code is replaced in the rendered page by its output.

**Frequently used attributes:**

-   `class`: The class implementing the macro

**Frequently used elements:**

 

 

**Example**

``` xml
<!-- macro example -->
<macro
  name='tasklist'
  class='com.atlassian.confluence.extra.tasklist.TaskListMacro'
     key='tasklist'>
    <description>Creates a very simple task list, with user checkable tasks</description>
</macro>
```

 

 

------------------------------------------------------------------------

#### [Code formatting](https://developer.atlassian.com/display/CONFDEV/Code+Formatting+Module)

Adds support for new languages to the <a href="#browse-projects" class="unresolved">builtin code macro</a>.

**Frequently used attributes:**

-   `class`: Class implementing the new code formatter.

 

 

**Example**

``` xml
<!-- code formatter example -->
<codeformatter
  name="ruby"
  key="ruby"
  class="com.example.confluence.formatters.RubyFormatter">
    <description>Code formatter for the Ruby programming language</description>
</codeformatter>
```

 

 

------------------------------------------------------------------------

### System tasks

#### [Job](https://developer.atlassian.com/display/CONFDEV/Job+Module)

Adds repeatable tasks to Confluence which can be scheduled by <a href="#browse-projects" class="unresolved">triggers</a>.

**Frequently used attributes:**

-   `class`: Class implementing the job.

 

**Example**

``` xml
<!-- job example -->
<job
  key="myJob"
  name="My Job"
  class="com.example.myplugin.jobs.MyJob"/>
```

------------------------------------------------------------------------

#### [Lifecycle](https://developer.atlassian.com/display/CONFDEV/Lifecycle+Module)

Adds tasks to be run on Confluence startup and shutdown.

**Frequently used attributes:**

-   `class`: Implements the lifecycle module for startup or shutdown.

 

 

**Example**

``` xml
<!-- lifecycle example -->
<lifecycle
  key="frobozz"
  name="Frobozz Service"
  class="com.example.frobozz.Lifecycle"
  sequence="1200">
    <description>Start and stop the Frobozz service</description>
</lifecycle>
```

 

 

------------------------------------------------------------------------

#### [Triggers](https://developer.atlassian.com/display/CONFDEV/Trigger+Module)

Schedules [DEVNET:jobs](#devnet:jobs) to run.

**Frequently used elements:**

-   `job`: The key of the job module to schedule.
-   `schedule`: When to run the job. Can be expressed as a cron job or by repeat intervals.

 

 

**Example**

``` xml
<!-- trigger example -->
<trigger
  key="myTrigger"
  name="My Trigger">
   <job key="myJob" />
   <schedule
     repeat-interval="3600000"
     repeat-count="5" />
</trigger>
```

 

 

------------------------------------------------------------------------

### Look and feel

#### [Decorators](https://developer.atlassian.com/display/CONFDEV/Decorator+Module)

Allows the user to add Sitemesh Velocity <a href="#browse-projects" class="unresolved">decorators</a> around Confluence pages.

**Frequently used attributes:**

-   `page`: Name of the Velocity template to render as the decorator.

**Frequently used elements:**

-   `pattern`: The URL pattern for which pages should have this decorator applied.

 

 

**Example**

``` xml
<!-- decorator example -->
<decorator
  name="myDecorator"
  page="myDecorator.vmd"
  key="myDecorator">
    <description>My sample decorator.</description>
    <pattern>/plugins/sampleplugin/*</pattern>
</decorator>
```

 

 

------------------------------------------------------------------------

#### [Language](https://developer.atlassian.com/display/CONFDEV/Language+Module)

Defines new languages for the Confluence UI.

**Frequently used attributes:**

-   `language`: The language defined by this module (must exist in java.util.Locale)
-   `country`: The country this language is intended for

**Frequently used elements:**

-   `resource` (download): Defines a flag image to show for this resource.

 

 

**Example**

``` xml
<!-- language example -->
<language
  name="German"
  key="de_DE"
  language="de"
  country="DE">
    <resource
      name="de_DE.gif"
      type="download"
      location="templates/languages/de_DE/de_DE.gif">
        <property
          key="content-type"
          value="image/gif"/>
    </resource>
</language>
```

 

 

------------------------------------------------------------------------

#### [Theme](https://developer.atlassian.com/display/CONFDEV/Theme+Module)

Defines a new theme (of stylesheets and images) for Confluence.

**Frequently used attributes:**

-   `class`: The class implementing the theme. (Don't change this.)

**Frequently used elements:**

-   `resource` (download): CSS stylesheets implementing the theme (and images)
-   `resource` (icon): Theme icon image used in the Choose Theme menu.

 

 

**Example**

``` xml
<!-- theme example -->
<theme
  key="simple-theme"
  name="Simple Demo Theme"
  class="com.atlassian.confluence.themes.BasicTheme">
    <resource type="download"
      name="default-theme.css"
      location="/includes/css/default-theme.css"/>
    <resource type="download"
      name="image-theme.css"
      location="image-theme.css"/>
    <resource type="download"
      name="home-16.png"
      location="home-16.png"/>
    <resource key="icon"
      name="themeicon.gif"
      type="download"
      location="your-theme-icon.gif"/>
</theme>
```

 

 

------------------------------------------------------------------------

#### [Keyboard shortcuts](https://developer.atlassian.com/display/CONFDEV/Keyboard+Shortcut+Module)

Defines a <a href="#browse-projects" class="unresolved">keyboard shortcut</a> within Confluence.

**Frequently used elements:**

-   `order`: The order in which this shortcut appears in the Keyboard Shortcuts dialog box.
-   `description`: A human-readable description of this shortcut.
-   `shortcut`: The keyboard shortcut keystroke sequence.
-   `operation`: The target of the keyboard shortcut.
-   `context`: Which pages this shortcut will be active on.

 

 

**Example**

``` xml
<!-- keyboard shortcut example -->
<keyboard-shortcut
  key="goto.space"
  i18n-name="admin.keyboard.shortcut.goto.space.name"
  name="Browse Space">
    <order>20</order>
    <description key="admin.keyboard.shortcut.goto.space.desc">Browse Space</description>
    <shortcut>gs</shortcut>
    <operation type="followLink">#space-pages-link</operation>
    <context>global</context>
</keyboard-shortcut>
```

 

 

------------------------------------------------------------------------

### Custom actions

#### [XWork/WebWork](https://developer.atlassian.com/display/CONFDEV/XWork-WebWork+Module)

Defines new XWork/WebWork actions, adding URL-addressable functionality to Confluence.

**Frequently used elements:**  
The body of the `<xwork>` element contains XWork action markup. An example is below.

 

 

**Example**

``` xml
<!-- xwork example -->
<xwork
  name="livesearchaction"
  key="livesearchaction">
    <package
      name="livesearch"
      extends="default"
      namespace="/plugins/livesearch">
        <default-interceptor-ref name="defaultStack" />

        <action name="livesearch"
          class="com.atlassian.confluence.extra.livesearch.LiveSearchAction">
            <result name="success" type="velocity">
              /templates/extra/livesearch/livesearchaction.vm
            </result>
        </action>
    </package>
</xwork>
```

------------------------------------------------------------------------

### Other types

#### [Search index extractor](https://developer.atlassian.com/display/CONFDEV/Extractor+Module)

Defines an extractor for adding information to the Confluence search index.

**Frequently used attributes:**

-   `class`: The class implementing the extractor.
-   `priority`: The order in which the extractor is run; lower-priority extractors run first.

 

 

**Example**

``` xml
<!-- extractor example -->
<extractor
  name="Page Metadata Extractor"
  key="pageMetadataExtractor"
  class="com.atlassian.confluence.extra.extractor.PageMetadataExtractor"
  priority="1000">
    <description>Extracts certain keys from a page's metadata and adds them to the search index.</description>
</extractor>
```

 

 

------------------------------------------------------------------------

#### [Path converters](https://developer.atlassian.com/display/CONFDEV/Path+Converter+Module)

Defines path converters which provide custom path mapping in a plugin.

**Frequently used attributes:**

-   `class`: The class implementing the path converter.
-   `weight`: The order in which this path converter is executed relative to any other converters.

 

 

**Example**

``` xml
<!-- path converter example -->
<path-converter
  weight="10"
  key="example-converter"
  class="com.mycompany.confluence.plugin.ExamplePathConverter"/>
```

 

 

------------------------------------------------------------------------

#### [Velocity context](https://developer.atlassian.com/display/CONFDEV/Velocity+Context+Module)

Defines new components to be added to the [Confluence Velocity context](https://developer.atlassian.com/display/CONFDEV/Confluence+Objects+Accessible+From+Velocity).

**Frequently used attributes:**

-   `class`: The class representing the component to be added.
-   `context-key`: The Velocity variable that will be created to reference this component.

 

 

**Example**

``` xml
<!-- velocity context example -->
<velocity-context-item
  key="myVelocityHelper"
  name="My Plugin's Velocity Helper"
  context-key="myVelocityHelper"
  class="com.example.myplugin.helpers.MyVelocityHelper" />
```




































































