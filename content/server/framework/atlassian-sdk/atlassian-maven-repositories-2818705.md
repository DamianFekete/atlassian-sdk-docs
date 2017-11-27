---
title: Atlassian Maven Repositories 2818705
aliases:
    - /server/framework/atlassian-sdk/atlassian-maven-repositories-2818705.html
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=2818705
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=2818705
confluence_id: 2818705
platform:
product:
category:
subcategory:
---
# Documentation : Atlassian Maven Repositories

Atlassian provides various Maven repositories for Plugin Developers.We recommend using the [Atlassian Plugin SDK](/server/framework/atlassian-sdk/working-with-the-sdk) to make sure you've got the correct settings to use our servers.

The Plugin SDK handles almost all of this Maven tweaking for you. The SDK includes an embedded Maven installation and correct `settings.xml` that will be kept up to date as necessary. We believe it makes the plugin development process much easier. For more information, see [here](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project).

## Atlassian Maven Proxy 

The Atlassian Maven proxy sits in front of all of our other Maven repositories, as well as third-party repositories like iBiblio and Codehaus. This should provide all artifacts needed to build our products and plugins. In the basic case, this is the only repository you need to know about.

-   <a href="https://packages.atlassian.com/maven/repository/public" class="uri external-link">https://packages.atlassian.com/maven/repository/public</a>

``` xml
<repository>
      <id>atlassian-public</id>
      <url>https://packages.atlassian.com/maven/repository/public</url>
      <snapshots>
        <enabled>true</enabled>
        <updatePolicy>never</updatePolicy>
        <checksumPolicy>warn</checksumPolicy>
      </snapshots>
       <releases>
         <enabled>true</enabled>
         <checksumPolicy>warn</checksumPolicy>
      </releases>
</repository>
```

### Atlassian 3rdParty Repository

The third-party directory contains jars that we are allowed to re-distribute or re-host but we do not own.

-   <a href="https://packages.atlassian.com/maven/3rdparty" class="uri external-link">https://packages.atlassian.com/maven/3rdparty</a>

It is contained in <a href="https://packages.atlassian.com/maven/repository/public" class="uri external-link">https://packages.atlassian.com/maven/repository/public</a>.

### Atlassian Public Repository

The Atlassian public repository contains all artifacts owned by Atlassian necessary to build a plugin for our products. It contains binaries, source and javadoc of our opensource components, and binaries and javadoc for our closed-source components.

-   <a href="https://packages.atlassian.com/maven/public" class="uri external-link">https://packages.atlassian.com/maven/public</a>
-   <a href="https://packages.atlassian.com/maven/public-snapshot" class="uri external-link">https://packages.atlassian.com/maven/public-snapshot</a>

It is contained in <a href="https://packages.atlassian.com/maven/repository/public" class="uri external-link">https://packages.atlassian.com/maven/repository/public</a>

{{% warning %}}

We are in the process of deprecating all <a href="https://maven.atlassian.com" class="external-link">maven.atlassian.com</a> urls. If you are using any of those, please change them to a url mentioned above as soon as practical. We will update the developer community more widely when we expect to decommision the old maven.atlassian.com urls permanently.

{{% /warning %}}
















































































































































































































































































































