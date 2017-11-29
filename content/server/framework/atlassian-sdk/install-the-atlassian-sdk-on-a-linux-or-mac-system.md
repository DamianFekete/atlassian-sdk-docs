---
aliases:
- /server/framework/atlassian-sdk/install-the-atlassian-sdk-on-a-linux-or-mac-system-11305014.html
- /server/framework/atlassian-sdk/install-the-atlassian-sdk-on-a-linux-or-mac-system-11305014.md
category: devguide
confluence_id: 11305014
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=11305014
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=11305014
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/install-the-atlassian-sdk-on-a-linux-or-mac-system
new_url: /server/framework/atlassian-sdk/install-the-atlassian-sdk-on-a-linux-or-mac-system
platform: server
product: atlassian-sdk
subcategory: learning
title: Install the Atlassian SDK on a Linux or Mac system
---
# Install the Atlassian SDK on a Linux or Mac system

{{% note %}}

Not using Linux / Mac?

Windows users should see [Install the Atlassian SDK on a Windows system](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Windows+System)

{{% /note %}}

 

, you install the SDK on your Linux or Mac system. You also configure your operating system to recognize the SDK commands in your environment.

 

 

## Step 1: Configure your environment

{{% note %}}

This assumes that you have the Java JDK1.8.x installed as described in [Before you begin](https://developer.atlassian.com/display/DOCS/Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project)

{{% /note %}}

Verify that you JAVA\_HOME is set in your system by running echo $JAVA\_HOME from the **terminal**

``` text
host:~ test$ echo $JAVA_HOME
/Library/Java/JavaVirtualMachines/jdk1.8.0_65.jdk/Contents/Home
```

If the output resembles the above skip ahead to [Step 2: Download and Install the SDK](#step-2:-download-and-install-the-sdk)

The `JAVA_HOME` environment variable specifies the location of the JDK on your system. On Mac OS X, if you accepted the defaults when you installed the JDK, this is `/Library/Java/JavaVirtualMachines/1.8.0.jdk/Contents/Home`. On Linux, it may be `/usr/local/jdk`, or a similar location. You should add the JDK's `bin` directory to your `PATH` environment variable as well. This ensures your environment is configured and can locate the `javac` command.

To set your `PATH` and `JAVA_HOME` variables:

1.  Edit the `.bashrc` file in your home directory using your favourite editor (we use vi in this example).

    ``` bash
    host:~ test$ vi ~/.bash_profile
    ```

2.  Add the following lines at the end of the file:

    ``` bash
    JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0.0_91.jdk/Contents/Home
    export JAVA_HOME
    export PATH=$PATH:$JAVA_HOME/bin
    ```

    {{% note %}}

The path in Line 1 will be the path for the JDK on **your system**.

For Mac OS X this is usually `/Library/Java/JavaVirtualMachines/1.8.x.jdk`. On Linux it may be `/usr/local/jdk` or similar.

{{% /note %}}

3.  Save and close the file.
4.  Enter the following at the command line to pick up your changes:

    ``` bash
    host:~ test$ source ~/.bash_profile
    ```

5.  Verify you are now seeing the correct result when you enter the command `javac -version` in **terminal**

    ``` text
    host:~ test$ javac -version
    javac 1.8.0_91 
    ```

## Step 2: Download and install the SDK

There are native installers for a number of operating systems available, as well as a TGZ (GZipped tar file) which can be used for manual installation.  

{{% note %}}

**Last updated 04 Dec 2015**

By downloading and/or using this SDK you agree to the <span class="underline">[Atlassian Developer Terms](Atlassian-Developer-Terms_37879876.html)</span>

{{% /note %}}

 

 

Select the installation instructions that best suit you:

-   [Mac OSX](#mac-osx)
-   [Homebrew](#homebrew)
-   [Debian, Ubuntu Linux](#debian,-ubuntu-linux)
-   [Red Hat Enterprise Linux, CentOS, Fedora (RPM)](#red-hat-enterprise-linux,-centos,-fedora-(rpm))
-   [.tgz File](#.tgz-file)

### Mac OSX

PKG File

1.  <a href="https://marketplace.atlassian.com/download/plugins/atlassian-plugin-sdk-mac" class="external-link">Download the PKG file</a>.
2.  Double click the PKG file to launch the installer.
3.  Follow the prompts to complete the installation.
4.  [Next: Verify that you have set up the SDK correctly](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

### Homebrew

1.  Open a Terminal window and add the Atlassian "Tap" to your Brew using the command:

    ``` text
    brew tap atlassian/tap
    ```

2.  Then install the SDK via the atlassian/tap using the command:

    ``` text
    brew install atlassian/tap/atlassian-plugin-sdk
    ```

3.  [Next: Verify that you have set up the SDK correctly](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

### Debian, Ubuntu Linux

On a Debian based Linux like Ubuntu, you can install the Atlassian Plugin SDK using `apt-get` or `aptitude`, but first you have to set up the Atlassian repositories. You only need to do this once and it requires `sudo` privileges.

To set up the Atlassian repositories,

1.  Open a **terminal** window and enter the following:

    ``` text
    sudo sh -c 'echo "deb https://sdkrepo.atlassian.com/debian/ stable contrib" >>/etc/apt/sources.list'
    ```

2.  After the prompt returns, add the public key:

    ``` text
    sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv-keys B07804338C015B73
    ```

3.  Once you have set up the Atlassian repositories, enter the following to install the SDK:

    ``` text
    sudo apt-get install apt-transport-https
    sudo apt-get update
    sudo apt-get install atlassian-plugin-sdk
    ```

    Note: You can use the same  `apt`  tools to upgrade the SDK to a new version when an update becomes available.

    The first command makes sure that you have     `apt-transport-https`  package installed to make     `apt`  be able to access https repositories.

4.  [Next: Verify that you have set up the SDK correctly](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

### Red Hat Enterprise Linux, CentOS, Fedora (RPM)

{{% note %}}

The instructions below use `dnf` to install the SDK. If you are on an older version you might not have `dnf` and should use `yum` instead.

{{% /note %}}

All you should have to do to download the latest version of the SDK is:

``` bash
sudo dnf install atlassian-plugin-sdk
```

If this does not work, try downloading and installing manually:

1.  <a href="https://marketplace.atlassian.com/download/plugins/atlassian-plugin-sdk-rpm/version/42380" class="external-link">Download the Atlassian Plugin SDK - RPM</a>

2.  Then, open a Terminal window and start the installation:

    ``` bash
    sudo dnf localinstall <PATH_TO_DOWNLOADED_FILE>
    ```

    remember that you will need to modify your path in the above example, it should be something like ~/Downloads/atlassian-plugin-sdk-6.2.9.noarch.rpm

As always[, Next: Verify that you have set up the SDK correctly.](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

### .tgz File

To install the latest version of SDK, do the following:

1.  <a href="https://marketplace.atlassian.com/download/plugins/atlassian-plugin-sdk-tgz" class="external-link">Download a TGZ (GZipped tar file) of the SDK</a>
2.  Locate the downloaded SDK file. 
3.  Extract the file to your local directory.

    ``` text
    sudo tar -xvzf atlassian-plugin-sdk-4.0.tar.gz -C /opt
    ```

4.  Rename the extracted folder to  `atlassian-plugin-sdk` .

    ``` text
    sudo mv /opt/atlassian-plugin-sdk-4.0 /opt/atlassian-plugin-sdk 
    ```

    If you are comfortable working with symbolic links, you can set up a symbolic link instead of renaming the directory.

5.  [Next: Verify that you have set up the SDK correctly](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

## Step 3: Verify that you have set up the SDK correctly

Open a **terminal** window and run the following command:

``` text
atlas-version
```

You should see something similar to:

``` text
ATLAS Version:    6.2.9
ATLAS Home:       /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec
ATLAS Scripts:    /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/bin
ATLAS Maven Home: /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/apache-maven-3.2.1
AMPS Version:     6.2.6
--------
Executing: /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/apache-maven-3.2.1/bin/mvn --version -gs /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/apache-maven-3.2.1/conf/settings.xml
Java HotSpot(TM) 64-Bit Server VM warning: ignoring option MaxPermSize=256M; support was removed in 8.0
Apache Maven 3.2.1 (ea8b2b07643dbb1b84b6d16e1f08391b666bc1e9; 2014-02-15T04:37:52+10:00)
Maven home: /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/apache-maven-3.2.1
Java version: 1.8.0_45, vendor: Oracle Corporation
Java home: /Library/Java/JavaVirtualMachines/jdk1.8.0_45.jdk/Contents/Home/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "10.11.6", arch: "x86_64", family: "mac"
```

{{% note %}}

Look for `Maven home `and note that you are running the version of Maven that is installed with the SDK.

{{% /note %}}

## Next step

You now have a local development environment configured for the Atlassian SDK and you're ready to build your first plugin!

**[Create a Plugin](https://developer.atlassian.com/display/DOCS/Create+a+HelloWorld+Plugin+Project)**

## Additional Resources

Need help? Request support at <a href="https://ecosystem.atlassian.net/servicedesk/customer/portal/14" class="external-link">Developer Technical Support Portal</a>







































































































































