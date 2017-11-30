---
aliases:
- /server/framework/atlassian-sdk/installing-active-objects-5669200.html
- /server/framework/atlassian-sdk/installing-active-objects-5669200.md
category: devguide
confluence_id: 5669200
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=5669200
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=5669200
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/atlassian-platform-common-components/active-objects/installing-active-objects
new_url: /server/framework/atlassian-sdk/installing-active-objects
platform: server
product: atlassian-sdk
subcategory: learning
title: Installing Active Objects
---
# Installing Active Objects

This page describes how to install the Atlassian [Active Objects](https://developer.atlassian.com/display/AO/Active+Objects) plugin into the Atlassian products, such as JIRA or Confluence. Where supported, the relevant version of Active Objects is bundled with the product.

{{% warning %}}

Atlassian does not recommend that you install or upgrade Active Objects in a production environment, unless instructed by the Atlassian support team.

{{% /warning %}}

## Active Objects in JIRA

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compatibility</p></td>
<td><ul>
<li>The Active Objects plugin is compatible with JIRA 4.3 and later.</li>
<li>A developer preview of Active Objects is bundled with the JIRA 4.4.x series. This version of Active Objects is used by GreenHopper and by plugin developers for testing.</li>
<li>A production-ready version of Active Objects is bundled with JIRA 5.0 and later. There is therefore no need to install it unless you need a later version. See <a href="/server/framework/atlassian-sdk/how-to-upgrade-ao-to-0-18-x-in-jira-5">How to upgrade AO to 0.18.x in JIRA 5</a>.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>Notes</p></td>
<td><p>If you are planning to release a plugin that uses Active Objects, please target JIRA 5.0 or later. You should not ship a plugin for JIRA 4.4 that uses Active Objects. You should also not ask a customer to upgrade their version of Active Objects to suit your plugin.</p></td>
</tr>
</tbody>
</table>

To install Active Objects in JIRA:

1.  Download the latest version of the Active Objects <a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/activeobjects/activeobjects-plugin/" class="external-link">plugin JAR</a>.
2.  Download the appropriate version of the JIRA SPI plugin for Active Objects JAR:
    -   for <a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/activeobjects/activeobjects-jira43-spi" class="external-link">JIRA 4.3</a>
    -   for <a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/activeobjects/activeobjects-jira-spi/" class="external-link">JIRA 4.4 and later</a>
3.  Install the JIRA SPI plugin using the <a href="http://confluence.atlassian.com/display/JIRA043/Managing+JIRA%27s+Plugins#ManagingJIRA%27sPlugins-Installingyourownplugin" class="external-link">manual plugin installation process</a>.
4.  Install the JIRA Active Objects plugin using the <a href="http://confluence.atlassian.com/display/JIRA043/Managing+JIRA%27s+Plugins#ManagingJIRA%27sPlugins-Installingyourownplugin" class="external-link">manual plugin installation process</a>.

{{% note %}}

If you had previously installed a plugin which depends on Active Objects you may need to re-enable it.

{{% /note %}}

See also [How to upgrade AO to 0.18.x in JIRA 5](/server/framework/atlassian-sdk/how-to-upgrade-ao-to-0-18-x-in-jira-5).

## Active Objects in Confluence

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compatibility</p></td>
<td><ul>
<li>The Active Objects plugin is compatible with Confluence 3.4 and later.</li>
<li>Active Objects in Confluence does not support DB2.</li>
<li>A production-ready version of Active Objects is bundled with Confluence 4.3 and later. There is no need to install it unless you need a later version.</li>
</ul></td>
</tr>
<tr class="even">
<td><p>Note</p></td>
<td><p>If you are planning to release a plugin that uses Active Objects, please target Confluence 4.3 or later. You should not ship a plugin for Confluence 4.2 or earlier that uses Active Objects. You should also not ask a customer to upgrade their version of Active Objects to suit your plugin.</p></td>
</tr>
</tbody>
</table>

To install Active Objects:

1.  Download the latest version of the Active Objects <a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/activeobjects/activeobjects-plugin/" class="external-link">plugin JAR</a>.
2.  Download the <a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/activeobjects/activeobjects-confluence-spi" class="external-link">latest version of the Confluence SPI plugin for Active Objects JAR</a>.
3.  Install the Confluence SPI plugin using the <a href="http://confluence.atlassian.com/display/DOC/Installing+a+Plugin#InstallingaPlugin-Uploadingyourownplugin" class="external-link">manual plugin installation process</a>.
4.  Install the Active Objects plugin using the <a href="http://confluence.atlassian.com/display/DOC/Installing+a+Plugin#InstallingaPlugin-Uploadingyourownplugin" class="external-link">manual plugin installation process</a>.

## Active Objects in FishEye/Crucible

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compatibility</p></td>
<td><p>Active Objects is bundled with FishEye/Crucible 2.7 and later.</p></td>
</tr>
<tr class="even">
<td><p>Note</p></td>
<td><p>The implementation of Active Objects in FishEye/Crucible is still a <strong>development preview</strong>. You should not ship a plugin for FishEye/Crucible that uses Active Objects, nor ask a customer to install Active Objects into FishEye/Crucible to suit your plugin.</p></td>
</tr>
</tbody>
</table>

Active Objects 0.15 is bundled by default. To install the latest version:

1.  Download <a href="https://maven.atlassian.com/content/repositories/atlassian-public/com/atlassian/activeobjects/activeobjects-plugin/" class="external-link">the Active Objects plugin JAR</a>.
2.  Follow the <a href="http://confluence.atlassian.com/display/FISHEYE/Installing+a+Plugin" class="external-link">manual plugin installation process</a> to install the plugin in FishEye/Crucible.

## Active Objects in Bamboo

<table>
<colgroup>
<col style="width: 50%" />
<col style="width: 50%" />
</colgroup>
<tbody>
<tr class="odd">
<td><p>Compatibility</p></td>
<td><p>Active Objects is compatible with Bamboo 3.4 and later.</p></td>
</tr>
<tr class="even">
<td>Note</td>
<td>If you are planning to release a plugin that uses Active Objects, it's recommended to target Bamboo 5.4 or later.</td>
</tr>
</tbody>
</table>

Active Objects plugin is bundled by default.












































































































































































































































































