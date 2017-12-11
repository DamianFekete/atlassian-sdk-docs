---
aliases:
- /server/framework/atlassian-sdk/16974434.html
- /server/framework/atlassian-sdk/16974434.md
category: devguide
confluence_id: 16974434
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=16974434
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=16974434
date: '2017-12-11'
legacy_title: What happened to studio.plugins.atlassian.com?
platform: server
product: atlassian-sdk
subcategory: faq
title: What happened to studio.plugins.atlassian.com?
---
# What happened to studio.plugins.atlassian.com?

Information for plugin developers and Atlassian customers regarding plugin projects that used to be hosted on Atlassian's JIRA Studio instance for plugin developers, <a href="https://studio.plugins.atlassian.com" class="uri external-link">https://studio.plugins.atlassian.com</a>.

## Legacy JIRA Studio Shutdown

The **Atlassian Plugins JIRA Studio** service (<a href="https://studio.plugins.atlassian.com)" class="uri external-link">https://studio.plugins.atlassian.com)</a> was a JIRA Studio server that Atlassian offered to third-party plugin developers as a location to host their plugin development efforts for free.

In February 2013, this service was decommissioned as the "JIRA Studio" product was retired from service in favor of Atlassian's new hosted offering, <a href="https://www.atlassian.com/software#cloud-products" class="external-link">Atlassian Cloud</a>. As the size of the Atlassian add-on ecosystem continues to grow, it became impractical to offer project hosting to every vendor on a single system.

Going forward, Atlassian now offers discounted cloud subscriptions for bonafide contributors to the Atlassian Marketplace. For more information, please consult our documentation on the [Marketplace Contributor discount](https://developer.atlassian.com/display/MARKET/Marketplace+Contributor+discount).

## Existing Projects Have Been Relocated

Atlassian contacted the project lead of every project hosted on the Atlassian Plugins JIRA Studio and assisted with relocation efforts for each project as requested. The following table below details each project that was historically located on the server and its eventual resting place.

**Please Note:** Many projects hosted on the server were subject to long periods of inactivity and the project lead did not respond to emails about the system shutdown. These projects have not been backed up by Atlassian and will not be accessible any longer.

<table>
<colgroup>
<col style="width: 33%" />
<col style="width: 33%" />
<col style="width: 33%" />
</colgroup>
<thead>
<tr class="header">
<th>Project Key</th>
<th>Project Name</th>
<th>Migration Outcome</th>
</tr>
</thead>
<tbody>
<tr class="odd">
<td>JHG</td>
<td>JIRA Mercurial Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<p>Available in the Marketplace as a commercial product.</p>
<p>Contact <a href="mailto:support@servicerocket.com" class="external-link">support@servicerocket.com</a></p></td>
</tr>
<tr class="even">
<td>JCNF</td>
<td>Conditional Notifications for JIRA</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<p>Deprecated<br />
Matt Doar (<a href="mailto:mdoar@pobox.com" class="external-link">mdoar@pobox.com</a>)</p></td>
</tr>
<tr class="odd">
<td>JCLIMD</td>
<td>JIRA Command Line Interface (Python)</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<p>Deprecated in favour of<a href="http://jira-python.readthedocs.org/en/latest/" class="external-link">jira-python</a>.</p>
<p>Matt Doar (<a href="mailto:mdoar@pobox.com" class="external-link">mdoar@pobox.com</a>)</p></td>
</tr>
<tr class="even">
<td>JFTS</td>
<td>JIRA Enhanced FreeText Search Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Deprecated
</div>
Matt Doar (<a href="mailto:mdoar@pobox.com" class="external-link">mdoar@pobox.com</a>)</td>
</tr>
<tr class="odd">
<td>JASF</td>
<td>JIRA ASF Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Deprecated
</div>
Matt Doar (<a href="mailto:mdoar@pobox.com" class="external-link">mdoar@pobox.com</a>)</td>
</tr>
<tr class="even">
<td>WSMPL</td>
<td>Webwork Sample Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Moved to <a href="https://bitbucket.org/mdoar/webwork-sample" class="external-link">BitBucket: Webwork Sample</a>
</div>
Matt Doar (<a href="mailto:mdoar@pobox.com" class="external-link">mdoar@pobox.com</a>)</td>
</tr>
<tr class="odd">
<td>PJD</td>
<td>Practical JIRA Development</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Moved to <a href="https://bitbucket.org/mdoar/practical-jira-plugins" class="external-link">BitBucket: Practical JIRA plugins</a>
</div>
Matt Doar (<a href="mailto:mdoar@pobox.com" class="external-link">mdoar@pobox.com</a>)</td>
</tr>
<tr class="even">
<td>TMCT</td>
<td>JIRA Timecharts Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Available in the Marketplace as a commercial product.
</div>
<p>Contact <a href="mailto:support@servicerocket.com" class="external-link">support@servicerocket.com</a></p></td>
</tr>
<tr class="odd">
<td>JCLP</td>
<td>JIRA Create and Link Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Available in the Marketplace as a commercial product.
</div>
<p>Contact <a href="mailto:support@servicerocket.com" class="external-link">support@servicerocket.com</a></p></td>
</tr>
<tr class="even">
<td>MDSF</td>
<td>Multiple Dependent Select Field</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Available in the Marketplace as a commercial product.
</div>
<p>Contact <a href="mailto:support@servicerocket.com" class="external-link">support@servicerocket.com</a></p></td>
</tr>
<tr class="odd">
<td>NUMHEAD</td>
<td>Numbered Headings</td>
<td><p><a href="https://bitbucket.org/avisi/numbered-headings/" class="external-link">Moved to Atlassian Bitbucket</a></p></td>
</tr>
<tr class="even">
<td>PUML</td>
<td>Confluence PlantUML Plugin</td>
<td><p><a href="https://avono-support.atlassian.net/browse/PUML" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="odd">
<td>CONFSU</td>
<td>Confluence SU</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/CONFSU" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="even">
<td>CHTMLIR</td>
<td>Confluence HTML Include Replace</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/CHTMLIR" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="odd">
<td>CLDAP</td>
<td>LDAP Util Library</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/CLDAP" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="even">
<td>CLATEX</td>
<td>LaTeX Plugin</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/CLATEX" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="odd">
<td>CASCII</td>
<td>Confluence ASCII Math Plugin</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/CASCII" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="even">
<td>JEMH</td>
<td>JIRA Enterprise Mail Handler</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/JEMH" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="odd">
<td>JSU</td>
<td>JIRA Switch User Plugin</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/JSU" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="even">
<td>JDIGEST</td>
<td>JIRA Notification Digester</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/JDIGEST" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="odd">
<td>JJPFL</td>
<td>thepluginpeople JIRA Post Function Library</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/JJPFL" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="even">
<td>SMILE</td>
<td>Confluence Smilies</td>
<td><p><a href="https://thepluginpeople.atlassian.net/browse/SMILE" class="external-link">Moved to Atlassian Cloud</a></p></td>
</tr>
<tr class="odd">
<td>CMUP</td>
<td>Confluence Mail Utilities Plugin</td>
<td><a href="https://akeles.jira.com/browse/CMUP" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>JTMPO</td>
<td>JIRA Tempo Plugin</td>
<td><a href="https://tempoplugin.jira.com/browse/JTMPO" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>LANGUAGE</td>
<td>Language Plugin</td>
<td><a href="https://bitvoodoo.atlassian.net/browse/LANGUAGE" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>NAVITABS</td>
<td>Navitabs Plugin</td>
<td><a href="https://bitvoodoo.atlassian.net/browse/NAVITABS" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>PANELBOX</td>
<td>Panel Box Plugin</td>
<td><a href="https://bitvoodoo.atlassian.net/browse/PANELBOX" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>VIEWTRACKER</td>
<td>Viewtracker Plugin</td>
<td><a href="https://bitvoodoo.atlassian.net/browse/VIEWTRACKER" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>VOODOO</td>
<td>Voodoo Plugin</td>
<td><a href="https://bitvoodoo.atlassian.net/browse/VOODOO" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>RWOT</td>
<td>Refined Wiki Original Theme</td>
<td><a href="http://issues.refinedwiki.com/browse/RWOT" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>RWMI</td>
<td>Refined Wiki Mobile Interface</td>
<td><a href="https://refinedwiki.atlassian.net/browse/RWMI" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>JWFT</td>
<td>JIRA Workflow Toolbox</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Fidel Castro Armario (<a href="mailto:fcarmario@gmail.com" class="external-link">fcarmario@gmail.com</a>)
</div></td>
</tr>
<tr class="odd">
<td>GRV</td>
<td>Groovy Runner</td>
<td><a href="https://jamieechlin.atlassian.net/browse/GRV" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>JBHV</td>
<td>JIRA Behaviours Plugin</td>
<td><a href="https://jamieechlin.atlassian.net/browse/JBHV" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>TIME</td>
<td>JIRA Timesheet Plugin</td>
<td><a href="https://bitbucket.org/azhdanov/jiratimesheet" class="external-link">Moved to Atlassian Bitbucket</a></td>
</tr>
<tr class="even">
<td>JWPLN</td>
<td>WorkPlan Report</td>
<td><a href="https://bitbucket.org/azhdanov/jiraworkplan" class="external-link">Moved to Atlassian Bitbucket</a></td>
</tr>
<tr class="odd">
<td>TMRPT</td>
<td>JIRA Time Tracking Reports</td>
<td><a href="https://jplugs.atlassian.net/browse/TMRPT" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>GANTT</td>
<td>JIRA Gantt Chart Plugin</td>
<td><a href="https://jplugs.atlassian.net/browse/GANTT" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>RSK</td>
<td>JIRA RiskManagement Plugin</td>
<td><a href="https://jplugs.atlassian.net/browse/RSK" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>FLTR</td>
<td>JIRA Saved Filter with Columns Plugin</td>
<td><a href="https://jplugs.atlassian.net/browse/FLTR" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>TIMTAM</td>
<td>TimTam Eclipse Client for Confluence</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Thomas Menzel (<a href="mailto:dev.tom.menzel@gmx.net" class="external-link">dev.tom.menzel@gmx.net</a>)
</div></td>
</tr>
<tr class="even">
<td>JMWE</td>
<td>JIRA Misc Workflow Extensions</td>
<td><a href="https://innovalog.atlassian.net/browse%20/JMWE" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>JMCF</td>
<td>JIRA Misc Custom Fields</td>
<td><a href="https://innovalog.atlassian.net/browse/JMCF" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>JMH</td>
<td>JIRA Advanced Mail Handler</td>
<td> 
<p><strong>Backup supplied to project owner</strong></p>
 
<div>
Brice Copy (<a href="mailto:brice.copy@cern.ch" class="external-link">brice.copy@cern.ch</a>)
</div></td>
</tr>
<tr class="odd">
<td>EZGMH</td>
<td>EZGooey Mail Handler</td>
<td><a href="https://capitalplugins.atlassian.net/browse/EZGMH" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>LSTCMT</td>
<td>Last Comment Custom Field</td>
<td><a href="https://capitalplugins.atlassian.net/browse/LSTCMT" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>JMETA</td>
<td>JIRA Metadata Plugin</td>
<td><a href="https://aevolu.atlassian.net/browse/JM" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>JSUTIL</td>
<td>JIRA Suite Utilities</td>
<td><a href="https://jsutil.atlassian.net/browse/JSUTIL" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>META</td>
<td>Confluence Metadata Plugin</td>
<td><a href="https://comalatech.jira.com/browse/META" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>CCPP</td>
<td>Confluence Content Publishing Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="odd">
<td>CDB</td>
<td>Database Integrity Checker Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="even">
<td>CWUP</td>
<td>Confluence Workflow Utilities Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="odd">
<td>APRV</td>
<td>Ad hoc Workflows</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="even">
<td>VIADUCT</td>
<td>Comalatech Viaduct Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="odd">
<td>CSTKY</td>
<td>Confluence Sticky Notes &amp; Snip-Edit Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="even">
<td>CMUS</td>
<td>Confluence Macro Usage Status Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="odd">
<td>TGLNK</td>
<td>Confluence Taglinks Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="even">
<td>SUSR</td>
<td>Confluence Space User Manageent Plugin</td>
<td><a href="https://github.com/sillycat/confluence-space-user-management" class="external-link">Moved to GitHub</a></td>
</tr>
<tr class="odd">
<td>SHBL</td>
<td>Confluence Shibboleth Authenticator</td>
<td><a href="https://github.com/chauth/confluence_http_authenticator" class="external-link">Moved to GitHub</a></td>
</tr>
<tr class="even">
<td>UWC</td>
<td>Universal Wiki Converter</td>
<td><a href="https://bitbucket.org/appfusions/universal-wiki-converter" class="external-link">Moved to Atlassian Bitbucket</a></td>
</tr>
<tr class="odd">
<td>CMEP</td>
<td>Confluence Multi-Excerpt Plugin</td>
<td><a href="https://artemis.atlassian.net/browse/CMEP" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>RR</td>
<td>Confluence RoadRunner</td>
<td><a href="https://artemis.atlassian.net/browse/RR" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>EMLPG</td>
<td>Confluence Send Email To Page Plugin</td>
<td><a href="https://artemis.atlassian.net/browse/EMLPGOLD" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>CHK</td>
<td>Confluence Checklists Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Ulrich Kunhardt (<a href="mailto:ulrich@comalatech.com" class="external-link">ulrich@comalatech.com</a>)
</div></td>
</tr>
<tr class="odd">
<td>JUP</td>
<td>User Picker From Project Role - Issue Alternative Assignee</td>
<td><a href="https://jamieechlin.atlassian.net/wiki/display/JUP" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>JVIZ</td>
<td>JIRA Workflow Visualization Plugin</td>
<td><a href="https://jamieechlin.atlassian.net/wiki/display/JVIZ" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="odd">
<td>JSQL</td>
<td>JIRA SQL Plugin</td>
<td><a href="https://jamieechlin.atlassian.net/wiki/display/JSQL" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>CSI</td>
<td>Confluence SharePoint Connector</td>
<td><a href="https://jira.atlassian.com/browse/CSI" class="external-link">Moved to jira.atlassian.com</a></td>
</tr>
<tr class="odd">
<td>CSSP</td>
<td>Confluence Subspace Plugin</td>
<td><a href="https://jira.communardo.de/browse/CSSP" class="external-link">Moved to Atlassian Cloud</a></td>
</tr>
<tr class="even">
<td>CSRVY</td>
<td>Confluence Survey Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Frank Stiller (<a href="mailto:drohne1673@gmail.com" class="external-link">drohne1673@gmail.com</a>)
</div></td>
</tr>
<tr class="odd">
<td>JITTER</td>
<td>Jitter for JIRA</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Viðar Svansson (<a href="mailto:vidarsvans@gmail.com" class="external-link">vidarsvans@gmail.com</a>)
</div></td>
</tr>
<tr class="even">
<td>COO</td>
<td>Confluence Open Office Extractor Plugin</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Sven Panko (<a href="mailto:sven.panko@gmail.com" class="external-link">sven.panko@gmail.com</a>)
</div></td>
</tr>
<tr class="odd">
<td>JSS</td>
<td>JIRA Scripting Suite</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Alexander Shchagin (<a href="mailto:shchagin@quisapps.com" class="external-link">shchagin@quisapps.com</a>)
</div></td>
</tr>
<tr class="even">
<td>SCAFF</td>
<td>ServiceRocket Scaffolding</td>
<td><p><strong>Backup supplied to project owner</strong></p>
<div>
Available in the Marketplace as a commercial product.
</div>
<p>Contact <a href="mailto:support@servicerocket.com" class="external-link">support@servicerocket.com</a></p></td>
</tr>
</tbody>
</table>

## My Project Has Disappeared

If your project was hosted on <a href="https://studio.plugins.atlassian.com" class="uri external-link">https://studio.plugins.atlassian.com</a> and has now disappeared, please contact us to discuss the situation. Our contact information is on the [How to Access Developer Support](https://developer.atlassian.com/display/SUPPORT/How+to+Access+Developer+Support) page.





































































































































































































































