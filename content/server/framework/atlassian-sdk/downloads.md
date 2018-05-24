---
aliases:
- /server/framework/atlassian-sdk/downloads-13633001.html
- /server/framework/atlassian-sdk/downloads-13633001.md
category: devguide
confluence_id: 13633001
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=13633001
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=13633001
date: '2018-05-23'
legacy_title: Downloads
platform: server
product: atlassian-sdk
subcategory: intro
title: Downloads
---
# Downloads

## Before you begin

{{% note %}}

Last updated 04 Dec 2015
By downloading and/or using this SDK you agree to the <span class="underline">[Atlassian Developer Terms](Atlassian-Developer-Terms_37879876.html)</span>

{{% /note %}}

To install the Atlassian Plugin SDK, you'll also need the following:

- Java SE Development Kit (JDK) 8 
- Your JAVA_HOME variable set

{{% note %}}

**A note on OpenJDK**

The Atlassian Plugin SDK *does not support OpenJDK*, please ensure you have the Oracle Java SE Development Kit installed and your JAVA_HOME variable referencing the Oracle JDK installation of Java.

{{% /note %}}


## First time users

If you're installing the Atlassian SDK for the first time, you can find detailed instructions for setting your JAVA_HOME, downloading and installing the Atlassian Plugin SDK and creating your first project. 

› [Set up the Atlassian SDK and Build a Project](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project)

## Download the installer

For Windows and macOS users, you can download the latest version of the installer via Atlassian Marketplace:

- [Atlassian Marketplace: Atlassian Plugin SDK - Windows](https://marketplace.atlassian.com/apps/1210950/atlassian-plugin-sdk-windows?hosting=server&tab=overview)
- [Atlassian Marketplace: Atlassian Plugin SDK - Mac OS X](https://marketplace.atlassian.com/apps/1210951/atlassian-plugin-sdk-mac-os-x?hosting=server&tab=overview)


## Installing from Package Managers

If you prefer you can use a suitable package manager for your operating system to install the Atlassian SDK. 

{{% note %}}

If you previously installed the SDK using `tar.gz` and added the SDK folder to your `PATH`, you'll need to remove it from your `PATH` before starting.

{{% /note %}}

### Debian / Ubuntu Linux

On a Debian-based Linux system like Ubuntu, you can install the SDK using `apt-get` or `aptitude`:

1.  First, set up the Atlassian SDK repositories:

    ``` bash
    sudo sh -c 'echo "deb https://packages.atlassian.com/atlassian-sdk-deb stable contrib" >>/etc/apt/sources.list'
    ```

1.  Download the public key using `curl` or `wget`:

    ``` bash
    wget https://packages.atlassian.com/api/gpg/key/public    
    ```
    
1.  Add the public key to `apt` to verify the package signatures automatically:

    ``` bash
    apt-key add public   
    ```

1.  Then, run the install:

    ``` bash
    sudo apt-get update
    sudo apt-get install atlassian-plugin-sdk
    ```
    

### RPM / RHEL / CentOS / Fedora (Yum)

To install on systems that use the Yum package manager:

1.  Create the repo file in your /etc/yum.repos.d/ folder:

    ``` bash
    sudo vi /etc/yum.repos.d/artifactory.repo
    ```

1. Configure the repository details:

    ```
    [Artifactory]
    name=Artifactory
    baseurl=https://packages.atlassian.com//atlassian-sdk-rpm/
    enabled=1
    gpgcheck=0
    ```

1.  Install the SDK:

    ``` bash
    sudo yum clean all
    sudo yum updateinfo metadata
    sudo yum install atlassian-plugin-sdk
    ```

### Homebrew (OS X)

As of 4.0, a `pkg` installer is available for OSX. It installs the SDK in `/usr/share` and adds links for the `atlas` commands into `/usr/local/bin`. An `uninstall.sh` script is also provided in `/usr/share/atlassian-plugin-sdk-N.N`

Alternatively Homebrew (aka, Brew) is an open source package manager for OS X and is an alternative to MacPorts. You can learn more about Homebrew and how to it install it at <a href="http://mxcl.github.com/homebrew/" class="uri external-link">http://mxcl.github.com/homebrew/</a>

To install the Atlassian Plugin SDK in Brew:

1.  Add the Atlassian "<a href="https://github.com/atlassian/homebrew-tap" class="external-link">Tap</a>" to your Brew:

    ``` bash
    brew tap atlassian/tap
    ```

2.  Next, install the SDK via the `atlassian/tap`:

    ``` bash
    brew install atlassian/tap/atlassian-plugin-sdk
    ```

This installs the SDK. Later, if you want to upgrade the SDK to a new version, use:

``` bash
brew update
brew upgrade atlassian/tap/atlassian-plugin-sdk
```

------------------------------------------------------------------------

### Installing an earlier version of the SDK

If you need to install an earlier version of the SDK for any reason, you will find it on the [Atlassian Marketplace](https://marketplace.atlassian.com/).  

{{% note %}}

The Atlassian Marketplace contains versions of the Atlassian Plugin SDK after 4.0. 
If you need an older version than what is available on the Marketplace, you can get it from the [Atlassian Public Maven repository](https://packages.atlassian.com/maven-public/com/atlassian/amps/atlassian-plugin-sdk/).

{{% /note %}}

1.  Remove an existing install, if necessary, using the method appropriate for your operating system. For example, for Debian / Ubuntu Linux, enter the command:

    ``` bash
    sudo apt-get --purge remove atlassian-plugin-sdk
    ```

2.  Download the version you want from the Atlassian Marketplace:
    -   [Atlassian Plugin SDK - Debian/Ubuntu](https://marketplace.atlassian.com/apps/1210992/atlassian-plugin-sdk-deb/version-history)
    -   [Atlassian Plugin SDK - Windows](https://marketplace.atlassian.com/apps/1210950/atlassian-plugin-sdk-windows/version-history)
    -   [Atlassian Plugin SDK - Linux RPM](https://marketplace.atlassian.com/apps/1210991/atlassian-plugin-sdk-rpm/version-history) 
    -   [Atlassian Plugin SDK - MacOS](https://marketplace.atlassian.com/apps/1210951/atlassian-plugin-sdk-mac-os-x/version-history)
    -   [Atlassian Plugin SDK - TGZ](https://marketplace.atlassian.com/apps/1210993/atlassian-plugin-sdk-tgz/version-history)

3.  Once you have the package for the version you want, install it using the method appropriate for your operating system. For example, for Debian / Ubuntu Linux, use:

    ``` bash
    sudo dpkg -i package_name
    ```

    Where package\_name is the name of the file you downloaded. For example:

    ``` bash
    sudo dpkg -i atlassian-plugin-sdk_4.1.5_all.deb
    ```

4.  The PATH isn't set automatically, so add the `bin` directory to your PATH manually, say in `etc/environment`:

    ``` bash
    /usr/share/atlassian-plugin-sdk-4.1.5/bin
    ```
