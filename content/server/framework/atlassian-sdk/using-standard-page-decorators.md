---
aliases:
- /server/framework/atlassian-sdk/using-standard-page-decorators-851983.html
- /server/framework/atlassian-sdk/using-standard-page-decorators-851983.md
category: devguide
confluence_id: 851983
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=851983
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=851983
guides: guides
platform: server
product: atlassian-sdk
subcategory: learning
title: Using Standard Page Decorators 851983
---
# Using standard page decorators

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Available:</p></td>
<td><p>Atlassian applications which support <a href="https://developer.atlassian.com/pages/viewpage.action?pageId=852134">Atlassian Plugin Framework 2.1</a> and later will also support standard page decorators.</p></td>
</tr>
</tbody>
</table>

 

## Purpose of the Standard Page Decorators

Atlassian applications support standard page decorators, allowing your plugin to generate new web pages with consistent decoration by the host application across the Atlassian products.

## Specifying a Decorator

Specify the decorator with an HTML `meta` tag in your `head` element:

``` xml
<html>
  <head>
    <meta name="decorator" content="atl.general"/>
  </head>
```

The following decorators are available.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Decorator</p></th>
<th><p>Description</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p><code>atl.admin</code></p></td>
<td><p>For application administration pages.</p>
<p><strong>Version of Atlassian Plugin Framework: 2.1 and later</strong></p></td>
</tr>
<tr class="even">
<td><p><code>atl.general</code></p></td>
<td><p>For the header and footer of general pages outside the administration UI.</p>
<p><strong>Version of Atlassian Plugin Framework: 2.1 and later</strong></p></td>
</tr>
<tr class="odd">
<td><p><code>atl.popup</code></p></td>
<td><p>For content that you want placed in a new browser popup window.</p>
<p><strong>Version of Atlassian Plugin Framework: 2.3 and later</strong></p></td>
</tr>
<tr class="even">
<td><p><code>atl.userprofile</code></p></td>
<td><p>For content on a page in the user profile.<br />
This decorator will generally be accompanied by a web item link or tab. The tab, if applicable, should be specified by the <code>tab</code> meta tag. For example:</p>
<p>In the above example, the value of the <code>content</code> attribute is the ID of the tab. Since plugins can be shared among applications, we recommend that cross-application plugins define their own tab to ensure the same ID will be used everywhere.</p>
<pre><code>&lt;html&gt;
  &lt;head&gt;
    &lt;meta name=&quot;decorator&quot; content=&quot;atl.userprofile&quot;/&gt;
    &lt;meta name=&quot;tab&quot; content=&quot;foo.bar&quot;&gt;
  &lt;/head&gt;
&lt;/html&gt;</code></pre>
<p>Note: The profile decorator is still experimental. In some applications it may function in the same way as <code>atl.general</code>. Tabs are not yet supported by all Atlassian applications. If not supported, the tab will simply be ignored.</p>
<p><strong>Version of Atlassian Plugin Framework: 2.3 and later</strong></p></td>
</tr>
</tbody>
</table>

































































































































































