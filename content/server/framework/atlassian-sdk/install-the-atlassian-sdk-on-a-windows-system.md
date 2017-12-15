---
aliases:
- /server/framework/atlassian-sdk/install-the-atlassian-sdk-on-a-windows-system-10421945.html
- /server/framework/atlassian-sdk/install-the-atlassian-sdk-on-a-windows-system-10421945.md
category: devguide
confluence_id: 10421945
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=10421945
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=10421945
date: '2017-12-08'
guides: tutorials
legacy_title: Install the Atlassian SDK on a Windows System
platform: server
product: atlassian-sdk
subcategory: learning
title: Install the Atlassian SDK on a Windows system
---
# Install the Atlassian SDK on a Windows system

{{% note %}}

Not using Windows?

Linux and Mac users should see I[nstall the Atlassian SDK on a Linux or Mac system](https://developer.atlassian.com/display/DOCS/Install+the+Atlassian+SDK+on+a+Linux+or+Mac+system)

{{% /note %}}

Before we dive into creating a plugin, you'll need to configure a local development environment so you can use the Atlassian SDK.  

Note: these instructions are for Windows 10.

## Step1. Set JAVA\_HOME and update Path variables

The `JAVA_HOME` environment variable specifies the location of the JDK on your system. For Windows users, the default directory is `C:\Program Files\Java\jdk1.8.x_y` , where x\_y is the Java JDK 8 version you have installed*. *

To set these environment variables:

1.  Browse to the `C:\Program Files\Java\jdk1.8.x_y `folder on your system and copy the path to the folder.
2.  Open **Control Panel** &gt; **System**&gt;**Advanced System Settings.**
3.  On the **Advanced** tab click **Environment Variables.**
4.  Locate the **System variables** section and click **New.**
5.  Enter JAVA\_HOME in the **Variable name** field and paste the folder path you copied into the **Variable value** field.
6.  Click **OK** to close the dialog.
7.  Click on **Path** variable in the **System variables ** section and click **Edit**. 
8.  Click **New **and type `%JAVA_HOME%\bin `in the available space.
9.  Close all dialog windows.
10. Open a new  **Command Prompt** window, and run the following command:

    ``` text
    C:\Users\manthony>javac -version
    javac 1.8.0_91
    ```

     verify that your output is similar to what appears above.

## Step 2. Install the SDK

{{% note %}}

**Atlassian Developer Terms last updated 04 Dec 2015**

By downloading and/or using this SDK you agree to the <span class="underline">[Atlassian Developer Terms](https://developer.atlassian.com/display/MARKET/Atlassian+Developer+Terms)</span>

{{% /note %}}

1.  <a href="https://marketplace.atlassian.com/download/plugins/atlassian-plugin-sdk-windows" class="external-link">Download the latest version of the SDK</a> 
2.  Locate the downloaded file and double-click to launch the installer
3.  Follow the prompts to install the SDK

## Step 3. Verify the SDK is installed

Open a  **Command Prompt** window, and run the following command:

``` text
atlas-version
```

You should see something similar to:

``` text
ATLAS Version:    6.2.9
ATLAS Home:       C:\Applications\Atlassian\atlassian-plugin-sdk-6.2.9
ATLAS Scripts:    C:\Applications\Atlassian\atlassian-plugin-sdk-6.2.9\bin
ATLAS Maven Home: C:\Applications\Atlassian\atlassian-plugin-sdk-6.2.9\apache-maven-3.2.1
AMPS Version:     6.2.6
--------
Executing: "C:\Applications\Atlassian\atlassian-plugin-sdk-6.2.9\apache-maven-3.2.1\bin\mvn.bat" --version -gs C:\Applications\Atlassian\atlassian-plugin-sdk-6.2.9\apache-maven-3.2.1/conf/settings.xml
Apache Maven 3.2.1 (ea8b2b07643dbb1b84b6d16e1f08391b666bc1e9; 2014-02-15T04:37:52+10:00)
Maven home: C:\Applications\Atlassian\atlassian-plugin-sdk-6.2.9\apache-maven-3.2.1\bin\..
Java version: 1.8.0_91, vendor: Oracle Corporation
Java home: C:\Program Files\Java\jdk1.8.0_91\jre
Default locale: en_AU, platform encoding: Cp1252
OS name: "windows 10", version: "10.0", arch: "amd64", family: "dos"
```

{{% note %}}

Note that you are running the version of Maven that comes with the SDK

{{% /note %}}

## Next step

You now have a local development environment configured for the Atlassian SDK and you're ready to build your first plugin!

{{% note %}}

**[Create a Plugin](https://developer.atlassian.com/display/DOCS/Create+a+HelloWorld+Plugin+Project)**

{{% /note %}}

## Additional Resources

Need help? Request support at <a href="https://ecosystem.atlassian.net/servicedesk/customer/portal/14" class="external-link">Developer Technical Support Portal</a>
