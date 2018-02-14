---
aliases:
- /server/framework/atlassian-sdk/install-the-atlassian-sdk-on-a-linux-or-mac-system-11305014.html
- /server/framework/atlassian-sdk/install-the-atlassian-sdk-on-a-linux-or-mac-system-11305014.md
category: devguide
confluence_id: 11305014
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=11305014
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=11305014
date: '2017-12-08'
guides: tutorials
legacy_title: Install the Atlassian SDK on a Linux or Mac system
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

On this page, you install the SDK on your Linux or Mac system. You also configure your operating system to recognize the SDK commands in your environment.

## Step 1: Configure your environment

{{% note %}}

This assumes that you have the Java JDK1.8.x installed as described in [Before you begin](https://developer.atlassian.com/display/DOCS/Set+up+the+Atlassian+Plugin+SDK+and+Build+a+Project)

{{% /note %}}

Verify that you JAVA\_HOME is set in your system by running echo $JAVA\_HOME from the **terminal**

``` text
host:~ test$ echo $JAVA_HOME
/Library/Java/JavaVirtualMachines/jdk1.8.0_65.jdk/Contents/Home
```

If the output resembles the above skip ahead to [Step 2: Download and Install the SDK](#step-2-download-and-install-the-sdk)

The `JAVA_HOME` environment variable specifies the location of the JDK on your system. On Mac OS X, if you accepted the defaults when you installed the JDK, this is `/Library/Java/JavaVirtualMachines/1.8.0.jdk/Contents/Home`. On Linux, it may be `/usr/local/jdk`, or a similar location. You should add the JDK's `bin` directory to your `PATH` environment variable as well. This ensures your environment is configured and can locate the `javac` command.

To set your `PATH` and `JAVA_HOME` variables:

1.  Edit the `.bashrc` file in your home directory using your favourite editor (we use vi in this example).

    ``` bash
    host:~ test$ vi ~/.bash_profile
    ```

1.  Add the following lines at the end of the file:

    ``` bash
    JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0.0_91.jdk/Contents/Home
    export JAVA_HOME
    export PATH=$PATH:$JAVA_HOME/bin
    ```

    {{% note %}}

The path in Line 1 will be the path for the JDK on **your system**.

For Mac OS X this is usually `/Library/Java/JavaVirtualMachines/1.8.x.jdk`. On Linux it may be `/usr/local/jdk` or similar.

    {{% /note %}}

1.  Save and close the file.
1.  Enter the following at the command line to pick up your changes:

    ``` bash
    host:~ test$ source ~/.bash_profile
    ```

1.  Verify you are now seeing the correct result when you enter the command `javac -version` in **terminal**

    ``` bash
    host:~ test$ javac -version
    javac 1.8.0_91 
    ```

## Step 2: Download and install the SDK

There are native installers for a number of operating systems available, as well as a TGZ (GZipped tar file) which can be used for manual installation.  

{{% note %}}

**Last updated 04 Dec 2015**

By downloading and/or using this SDK you agree to the <span class="underline">[Atlassian Developer Terms](Atlassian-Developer-Terms_37879876.html)</span>

{{% /note %}}

## Select the installation instructions that best suit you

### Mac OSX

PKG File

1.  <a href="https://marketplace.atlassian.com/download/plugins/atlassian-plugin-sdk-mac" class="external-link">Download the PKG file</a>.
1.  Double click the PKG file to launch the installer.
1.  Follow the prompts to complete the installation.
1.  [Next: Verify that you have set up the SDK correctly](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

### Homebrew

1.  Open a Terminal window and add the Atlassian "Tap" to your Brew using the command:

    ``` bash
    brew tap atlassian/tap
    ```

1.  Then install the SDK via the atlassian/tap using the command:

    ``` bash
    brew install atlassian/tap/atlassian-plugin-sdk
    ```

1.  [Next: Verify that you have set up the SDK correctly](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

### Debian, Ubuntu Linux

On a Debian based Linux like Ubuntu, you first need to download the package, then unpack and install it via `dpkg` (requires `sudo`). You can download it using the URL and a web request service like wget or curl.

To download the package,

1.  Open a **terminal** window and enter the following (replacing X.X.X with the SDK version number you are going to use):

    ``` bash
    curl https://packages.atlassian.com/list/atlassian-sdk-deb/deb-archive/atlassian-plugin-sdk_X.X.X_all.deb -O
    
    ```

1.  After the prompt returns and the SDK installer has downloaded, use `dkpg` to unpack and install the SDK:

    ``` bash
    sudo dpkg -i /path/to/atlassian-plugin-sdk_X.X.X_all.deb
    ```

1.  [Next: Verify that you have set up the SDK correctly](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

### Red Hat Enterprise Linux, CentOS, Fedora (RPM)

Similarly, on Red Hat based Linux distributions, download and install the package, using RPM Package Manager (`rpm`).

1.  To download the latest version of the SDK (replace X.X.X with the version number):
    
    ``` bash
    curl https://packages.atlassian.com/atlassian-sdk-rpm/rpm-stable/atlassian-plugin-sdk-X.X.X.noarch.rpm -O
    ```
1.  Use the RPM Package Manager (`rpm`) to unpack and install the SDK:

    ``` bash
    sudo rpm -i /path/to/atlassian-plugin-sdk-X.X.X.noarch.rpm
    ```
    
1.  As always,[Verify that you have set up the SDK correctly.](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

{{% note %}}
If you have a previous version of the SDK installed, first uninstall it with:
``` bash
sudo rpm -e atlassian-plugin-sdk
```
{{% /note %}}
### .tgz File

To install the latest version of SDK, do the following:

1.  <a href="https://marketplace.atlassian.com/download/plugins/atlassian-plugin-sdk-tgz" class="external-link">Download a TGZ (GZipped tar file) of the SDK</a>
1.  Locate the downloaded SDK file. 
1.  Extract the file to your local directory.

    ``` bash
    sudo tar -xvzf atlassian-plugin-sdk-4.0.tar.gz -C /opt
    ```

1.  Rename the extracted folder to  `atlassian-plugin-sdk` .

    ``` bash
    sudo mv /opt/atlassian-plugin-sdk-4.0 /opt/atlassian-plugin-sdk 
    ```

    If you are comfortable working with symbolic links, you can set up a symbolic link instead of renaming the directory.

1.  [Next: Verify that you have set up the SDK correctly](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system#InstalltheAtlassianSDKonaLinuxorMacsystem-step3Step3:VerifythatyouhavesetuptheSDKcorrectly)

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

{{% note %}}

**[Create a Plugin](https://developer.atlassian.com/display/DOCS/Create+a+HelloWorld+Plugin+Project)**

{{% /note %}}

## Additional Resources

Need help? Request support at <a href="https://ecosystem.atlassian.net/servicedesk/customer/portal/14" class="external-link">Developer Technical Support Portal</a>
