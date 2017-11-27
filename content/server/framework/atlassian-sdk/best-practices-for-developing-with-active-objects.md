---
aliases:
- /server/framework/atlassian-sdk/best-practices-for-developing-with-active-objects-8946892.html
- /server/framework/atlassian-sdk/best-practices-for-developing-with-active-objects-8946892.md
category: devguide
confluence_id: 8946892
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=8946892
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=8946892
learning: guides
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/developing-your-plugin-with-active-objects/best-practices-for-developing-with-active-objects
new_url: /server/framework/atlassian-sdk/best-practices-for-developing-with-active-objects
platform: server
product: atlassian-sdk
subcategory: learning
title: Best practices for developing with Active Objects
---
# Best practices for developing with Active Objects

This page contains some guidelines for best practices when developing a plugin that uses the Atlassian [Active Objects](https://developer.atlassian.com/display/AO/Active+Objects) (AO) plugin to store and retrieve data. The information takes the form of a quick reference sheet with links to pages containing further information.

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th><p>Summary of best practice</p></th>
<th><p>More information</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td><p>BLOB data</p></td>
<td><p>Currently, the Atlassian Active Object framework does not support binary large objects (BLOBs). Plugins that work with BLOBs fail. Until there is full support, do not write AO plugins that manipulate BLOBs.</p></td>
</tr>
<tr class="even">
<td><p>Specify table names in annotations</p></td>
<td><p>Use the <code>@Table</code> annotation to specify your table names so that you can freely rename the entity interface. For example, <code>@Table(&quot;MyEntity&quot;)</code>. See <a href="/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates">Upgrading your plugin and handling data model updates</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Do not remove column names from Java code on upgrade</p></td>
<td><p>When upgrading your plugin to a new version, do not remove columns unless you are aware of the consequences. Active Objects will make the database match the entity interface in the Java code. It alters tables to match the current interface. Removing columns will result in data loss. For that reason, we recommend that you do not delete tables or columns, only add them. See <a href="/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates">Upgrading your plugin and handling data model updates</a>.<br />
<br />
If your plugin needs a different table structure after the upgrade, your upgrade task should:</p>
<ul>
<li>Define a new table.</li>
<li>Copy the data into the new structure.</li>
<li>Move the old interface to an upgrade task &quot;attic&quot;. For example, put the old Java code into a package with a name like 'old' or 'archive'. It is safer never to remove this code, because you do not know which old version of your plugin people are upgrading from. They may need the archived code in order for the upgrade task to run.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>Take care when renaming entities</p></td>
<td><p>The Active Objects framework does not know about renaming. So if you change the name of an entity, it will remove the other entity and create a new one. All the data in the entity will be lost. See <a href="/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates">Upgrading your plugin and handling data model updates</a>.</p></td>
</tr>
<tr class="odd">
<td><p>When changing data type, migrate the data as part of the upgrade process</p></td>
<td><p>When migrating from one data type to another, the recommended approach is not to use an in-place type conversion. Instead, create a new column and migrate the data during the upgrade process. See <a href="/server/framework/atlassian-sdk/upgrading-your-plugin-and-handling-data-model-updates">Upgrading your plugin and handling data model updates</a>.</p></td>
</tr>
<tr class="even">
<td><p>Column names are case-sensitive</p></td>
<td><p>If you need to specify the raw column names in create or find operations, letter case is important. See <a href="/server/framework/atlassian-sdk/column-names">Column names</a>.</p></td>
</tr>
<tr class="odd">
<td><p>Column names should be in quotes</p></td>
<td><p>Active Objects doesn't automatically add quotes to column names in ORDER BY clauses. Depending on which database you are using, this may cause errors. For instance, this works on HSQLDB (the SDK default), but it does not work in PostgreSQL.</p>
<p>To avoid errors, we recommend that you always put column names within quotes in your ORDER BY statements, such as:</p>
<p>ORDER BY &quot;COLUMN_NAME&quot;</p></td>
</tr>
<tr class="even">
<td><p>Use 'stream' rather than 'find' or 'get' methods for large amounts of data</p></td>
<td><p>When reading a large amount of data, do not use the 'find' of 'get' methods. Instead, use the 'stream' methods. See this blog post: <a href="http://blogs.atlassian.com/2011/09/activeobjects_streaming_api/" class="external-link">ActiveObjects streaming API</a>.</p>
<p>The 'find' and 'get' methods read everything into memory as editable AO objects, which is very memory intensive. The 'stream' methods return read-only objects, which are cheaper to create, and give them to you one-by-one.</p></td>
</tr>
<tr class="odd">
<td><p>Delete all related data in the right order</p></td>
<td><p>When deleting object graphs, or data from related tables, you will need to delete them in the right order. Make sure you delete the children before the parents. AO does not support cascading.</p></td>
</tr>
<tr class="even">
<td><p>Use lazy initialisation with synchronisation</p></td>
<td><p>The Active Objects framework cannot be used during plugin startup. The easiest way to get around this is to perform any initialisation tasks only during the first HTTP request. As ActiveObjects service is not thread-safe during first call, it is also important to ensure other HTTP request threads are blocked while initialisation is being performed.</p></td>
</tr>
</tbody>
</table>

## Community-Authored Guidelines

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<thead>
<tr class="header">
<th>Summary of best practice</th>
<th><p>More information</p></th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>Operators must be space-delimited in WHERE clauses</td>
<td><p>When using an operator in a <code>WHERE</code> clause (such as the equals (&quot;=&quot;) operator or the greater than (&quot;&gt;&quot;) operator, spaces must be used to separate the operator from its operands. In other words, the following code is incorrect:</p>
<p>Wrong</p>
<div class="panel pdl code" style="border-width: 1px;">
<div class="panelContent pdl codeContent">
<pre class="sourceCode java" id="cb1" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence"><code class="sourceCode java"><div class="sourceLine" id="cb1-1" data-line-number="1"><span class="bu">Query</span>.<span class="fu">select</span>().<span class="fu">where</span>(<span class="st">&quot;FOO=&#39;bar&#39;&quot;</span>);</div></code></pre>
</div>
</div>
<p> </p>
<p>While this code is correct:</p>
<p>Right</p>
<div class="panel pdl code" style="border-width: 1px;">
<div class="panelContent pdl codeContent">
<pre class="sourceCode java" id="cb2" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence"><code class="sourceCode java"><div class="sourceLine" id="cb2-1" data-line-number="1"><span class="bu">Query</span>.<span class="fu">select</span>().<span class="fu">where</span>(<span class="st">&quot;FOO = &#39;bar&#39;&quot;</span>);</div></code></pre>
</div>
</div></td>
</tr>
<tr class="even">
<td>Column names in WHERE clauses must be in upper case</td>
<td>Mixed or lower-case column names in the <code>WHERE</code> clause will cause errors when running on PostgreSQL.</td>
</tr>
<tr class="odd">
<td>Boolean literals in WHERE clauses</td>
<td><p>Do not embed the boolean literal string <code>TRUE</code> or <code>FALSE</code> in a WHERE clause using Active Objects. This may cause incompatibilities with Microsoft SQL Server, such as the following error:</p>
<div class="panel pdl code" style="border-width: 1px;">
<div class="panelContent pdl codeContent">
<pre class="sourceCode xml" id="cb3" data-syntaxhighlighter-params="brush: plain; gutter: false; theme: Confluence" data-theme="Confluence"><code class="sourceCode xml"><div class="sourceLine" id="cb3-1" data-line-number="1">java.sql.SQLException: Invalid column name &#39;TRUE&#39;.</div></code></pre>
</div>
</div>
<p> </p>
<p>Instead, use a substitution variable and supply the value <code>Boolean.TRUE</code> or <code>Boolean.FALSE</code>, like so:</p>
<div class="panel pdl code" style="border-width: 1px;">
<div class="panelContent pdl codeContent">
<pre class="sourceCode java" id="cb4" data-syntaxhighlighter-params="brush: java; gutter: false; theme: Confluence" data-theme="Confluence"><code class="sourceCode java"><div class="sourceLine" id="cb4-1" data-line-number="1"><span class="bu">Query</span>.<span class="fu">select</span>().<span class="fu">where</span>(<span class="st">&quot;SOME_COLUMN IS ?&quot;</span>, <span class="bu">Boolean</span>.<span class="fu">TRUE</span>);</div></code></pre>
</div>
</div>
<p>See <a href="https://answers.atlassian.com/questions/216174/active-objects-mssql-boolean-issue" class="external-link">this question</a> on Atlassian Answers for more detail.</p></td>
</tr>
</tbody>
</table>

 

##### RELATED TOPICS

[Active Objects](https://developer.atlassian.com/display/AO/Active+Objects)




























































































































































































































































































