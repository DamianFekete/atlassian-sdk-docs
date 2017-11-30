---
title: Getting Started with Remote APIs 2818681
aliases:
    - /server/framework/atlassian-sdk/getting-started-with-remote-apis-2818681.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818681
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818681
confluence_id: 2818681
platform:
product:
category:
subcategory:
---
# Documentation : Getting Started with Remote APIs

## JIRA Studio

This page complements the <a href="http://summit.atlassian.com/" class="external-link">Summit 2011</a> lightening talk "<a href="http://summit.atlassian.com/archives/plugin-devs/integrating-infrastructure-with-jira" class="external-link">Satellite Apps around the Cloud: Integrating your infrastructure with JIRA Studio</a>". It includes links and material about the remote APIs provided by Atlassian products.

{{% note %}}

The links below point to the remote API documentation for the versions of each product currently included in JIRA Studio. If you aren't using JIRA Studio, check that your product version matches the documentation that you are using.

{{% /note %}}

### JIRA

-   <a href="http://confluence.atlassian.com/display/JIRA043/JIRA+REST+API+%28Alpha%29+Tutorial" class="external-link">REST Tutorial</a>
    -   <a href="http://docs.atlassian.com/jira/REST/4.3/" class="external-link">REST API Reference</a>
-   <a href="http://confluence.atlassian.com/display/JIRA043/Creating+a+SOAP+Client" class="external-link">SOAP Overview</a>
    -   <a href="http://docs.atlassian.com/rpc-jira-plugin/4.3/index.html?com/atlassian/jira/rpc/soap/JiraSoapServiceImpl.html" class="external-link">SOAP API Reference</a>
-   <a href="http://confluence.atlassian.com/display/JIRA043/JIRA+XML-RPC+Overview" class="external-link">XML-RPC Overview</a>
    -   <a href="http://docs.atlassian.com/software/jira/docs/api/rpc-jira-plugin/4.3/index.html?com/atlassian/jira/rpc/xmlrpc/XmlRpcService.html" class="external-link">XML-RPC API Reference</a>

### Confluence

-   <a href="http://confluence.atlassian.com/display/CONFDEV/Confluence+REST+APIs" class="external-link">REST Overview</a>
    -   <a href="http://docs.atlassian.com/atlassian-confluence/REST/3.5/" class="external-link">REST API Reference</a>
-   <a href="http://confluence.atlassian.com/display/CONFDEV/Remote+API+Specification" class="external-link">SOAP &amp; XML-RPC API spec</a>

### Bamboo

-   <a href="http://confluence.atlassian.com/display/BAMBOO026/Using+the+Bamboo+REST+APIs" class="external-link">REST API Usage guide</a>
    -   <a href="http://confluence.atlassian.com/display/BAMBOO026/Bamboo+REST+Resources" class="external-link">REST API Reference</a>

### Fisheye / Crucible

-   <a href="http://confluence.atlassian.com/display/FECRUDEV/REST+API+Guide" class="external-link">REST guide (start here)</a>
    -   <a href="http://docs.atlassian.com/fisheye-crucible/latest/wadl/fisheye.html" class="external-link">Fisheye REST API Reference</a>
    -   <a href="http://docs.atlassian.com/fisheye-crucible/latest/wadl/crucible.html" class="external-link">Crucible REST API Reference</a>

## Code Samples

-   <a href="https://bitbucket.org/rewbs/satellites-talk-samples/src" class="external-link">Code samples from the presentation</a>.
-   <a href="http://confluence.atlassian.com/display/DISC/Scripts" class="external-link">Various examples of using Confluence's remote APIs</a> (many in Python)
-   See also the documentation links above - there are several code examples within the docs.

## Relevant Issues

-   <a href="https://jira.atlassian.com/browse/CONF-3877" class="external-link">CONF-3877</a>: Overloaded methods in Confluence's WSDL cause issues with some SOAP toolkits
    -   If you hit this, try the XML-RPC API instead, or <a href="http://stackoverflow.com/questions/6136953/how-to-consume-wsdl-that-defines-overloaded-functions-using-groovy-or-ruby" class="external-link">see here for some generic workarounds</a>.

## Interesting Projects

-   <a href="https://studio.atlassian.com/browse/MRVN" class="external-link">Marvin</a>: IRC chatbot providing an interface to JIRA. Uses JIRA's SOAP interface. Written in Scala.
-   <a href="https://studio.plugins.atlassian.com/wiki/display/ACLI/Atlassian+Command+Line+Interface" class="external-link">Atlassian CLI</a>: Re-exposes Atlassian products' remote APIs as a command-line interface. Written in Java.
-   <a href="http://confluence.atlassian.com/display/DISC/Confluence4r" class="external-link">Confluence4r</a>: Simple and useful wrapper around Confluence's XML-RPC for Ruby.
-   <a href="http://confluence.atlassian.com/display/DISC/Confluence4r+Rails+Plugin" class="external-link">Confluence4r Rails Plugin</a>: enhanced version of Confluence4r for Rails.
-   <a href="http://confluence.atlassian.com/display/Support/Hercules" class="external-link">Hercules</a> the support bot / log analysis tool


















































































































































































































































































































