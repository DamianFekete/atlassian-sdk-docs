---
aliases:
- /server/framework/atlassian-sdk/downloads-13633001.html
- /server/framework/atlassian-sdk/downloads-13633001.md
category: devguide
confluence_id: 13633001
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=13633001
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=13633001
date: '2017-12-08'
legacy_title: Downloads
platform: server
product: atlassian-sdk
subcategory: intro
title: Downloads
---
# Downloads

{{% note %}}

Additional Requirements


-   All installations require **version 1.8.x of the JDK**. Please ensure this is installed first.
-   The Atlassian Plugin SDK *does not support OpenJDK*.

{{% /note %}}

## Use an installer

We recommend that you use one of our installers to get the Atlassian SDK onto your local development system. 

Just check your pre-requisites on [Windows](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/set-up-the-sdk-prerequisites-on-a-windows-system) or [Linux / Mac OS X](https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/set-up-the-sdk-prerequisites-for-linux-or-mac), then download and run the installer appropriate for your operating system:  

## First time users

If you're installing the Atlassian SDK for the first time, you may want to follow the more detailed instructions. 

› [Set up the Atlassian SDK and Build a Project](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project)

------------------------------------------------------------------------

## Other options

### Installing from Package Managers

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

4.  Then, run the install:

    ``` bash
    sudo apt-get update
    sudo apt-get install atlassian-plugin-sdk
    ```

### RPM / RHEL / CentOS / Fedora (Yum)

To install on systems that use the Yum package manager:

1.  Download the repo files to your /etc/yum.repos.d/ folder:

    ``` bash
    cd /etc/yum.repos.d/
    sudo wget https://sdkrepo.atlassian.com/atlassian-sdk-stable.repo
    ```

2.  Install the SDK:

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

If you need to install an earlier version of the SDK for any reason, you can do that by downloading the version you want from <a href="https://marketplace.atlassian.com" class="external-link">Atlassian Marketplace</a>.  

1.  Remove an existing install, if necessary, using the method appropriate for your operating system. For example, for Debian / Ubuntu Linux, enter the command:

    ``` bash
    sudo apt-get --purge remove atlassian-plugin-sdk
    ```

2.  Download the version you want from the Atlassian Marketplace:
    -   Debian / Ubuntu Linux: <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-deb/versions" class="uri external-link">marketplace.atlassian.com/plugins/atlassian-plugin-sdk-deb/versions</a>
    -   Microsoft Windows: <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-windows/versions" class="uri external-link">marketplace.atlassian.com/plugins/atlassian-plugin-sdk-windows/versions</a>
    -   Linux RPM: <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-rpm/versions" class="uri external-link">marketplace.atlassian.com/plugins/atlassian-plugin-sdk-rpm/versions</a>
    -   Mac OS X: <a href="https://marketplace.atlassian.com/plugins/atlassian-plugin-sdk-mac/versions" class="uri external-link">marketplace.atlassian.com/plugins/atlassian-plugin-sdk-mac/versions</a>

    {{% note %}}
The Atlassian Marketplace contains only relatively recent version of the Atlassian Plugin SDK. If you need an older version than what is available on the Marketplace, you can get it from the <a href="https://maven.atlassian.com/index.html#nexus-search;quick%7Eatlassian-plugin-sdk" class="external-link">Atlassian Maven repository</a>.

    {{% /note %}}
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
