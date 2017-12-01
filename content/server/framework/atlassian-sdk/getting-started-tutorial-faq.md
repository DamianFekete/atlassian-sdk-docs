---
aliases:
- /server/framework/atlassian-sdk/getting-started-tutorial-faq-43648385.html
- /server/framework/atlassian-sdk/getting-started-tutorial-faq-43648385.md
category: devguide
confluence_id: 43648385
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=43648385
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=43648385
legacy_url: https://developer.atlassian.com/docs/faq/getting-started-tutorial-faq
new_url: /server/framework/atlassian-sdk/getting-started-tutorial-faq
platform: server
product: atlassian-sdk
subcategory: faq
title: Getting started tutorial FAQ
---
# Getting started tutorial FAQ

Here you will find a list of Frequently Asked Questions about the '[Set up the Atlassian Plugin SDK and Build a Project](/server/framework/atlassian-sdk/set-up-the-atlassian-plugin-sdk-and-build-a-project)' Tutorial.

# How do I check if Oracle Java SE Development Kit 8 (JDK) is installed?

You can check which version of JAVA you have installed on your system by opening a Terminal window and running the following command:

``` bash
javac -version
```

If you're running the Oracle JAVA 8 you'll see a response like 

``` bash
javac 1.8.0_101
```

 

If you see an error like 'command not found' or just no response, then you'll need to install the Java SE Development Kit.  

You can get this at <a href="http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html" class="external-link">Oracle Java SE Development Kit 8 Downloads</a>.

# I get a BUILD FAILURE Error with 'Please verify you invoked Maven from the correct directory'

### Symptoms

You might come across the following error when you try to start up your plugin using the `atlas-run` command if you have not changed to the directory with the plugin skeleton you created:

``` bash
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 0.135 s
[INFO] Finished at: 2016-09-30T15:29:49+10:00
[INFO] Final Memory: 5M/245M
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal com.atlassian.maven.plugins:maven-amps-dispatcher-plugin:6.2.6:run (default-cli): Goal requires a project to execute but there is no POM in this directory (/Users/mpaisley/Test). Please verify you invoked Maven from the correct directory. -> [Help 1]
```

### How to fix it

Make sure you're in **your plugin directory** and make sure the **`pom.xml`** file has been created. 

# I get a BUILD FAILURE error with 'Unsupported major.minor version 52.0'

### Symptoms

You may see the following error if you are using the Oracle Java SE Development Kit 7 with the latest version of the Atlassian Plugin SDK:

``` bash
[INFO] ------------------------------------------------------------------------
[INFO] BUILD FAILURE
[INFO] ------------------------------------------------------------------------
[INFO] Total time: 2.102 s
[INFO] Finished at: 2016-09-30T14:50:03+10:00
[INFO] Final Memory: 18M/245M
[INFO] ------------------------------------------------------------------------
[ERROR] Failed to execute goal com.atlassian.maven.plugins:maven-jira-plugin:6.2.9-SNAPSHOT:compress-resources (default-compress-resources) on project myPlugin: Execution default-compress-resources of goal com.atlassian.maven.plugins:maven-jira-plugin:6.2.9-SNAPSHOT:compress-resources failed: Unable to load the mojo 'compress-resources' in the plugin 'com.atlassian.maven.plugins:maven-jira-plugin:6.2.9-SNAPSHOT' due to an API incompatibility: org.codehaus.plexus.component.repository.exception.ComponentLookupException: com/atlassian/maven/plugins/jira/JiraCompressResourcesMojo : Unsupported major.minor version 52.0
```

The latest version of the Atlassian Plugin SDK requires Oracle Java SE Development Kit 8.  

### How to confirm

You can check which version of JAVA you are using by entering the following command:

``` bash
atlas-version
```

The output will look something like:

``` bash
ATLAS Version:    6.2.9
ATLAS Home:       /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec
ATLAS Scripts:    /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/bin
ATLAS Maven Home: /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/apache-maven-3.2.1
AMPS Version:     6.2.6
--------
Executing: /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/apache-maven-3.2.1/bin/mvn --version -gs /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/apache-maven-3.2.1/conf/settings.xml
Apache Maven 3.2.1 (ea8b2b07643dbb1b84b6d16e1f08391b666bc1e9; 2014-02-15T04:37:52+10:00)
Maven home: /usr/local/Cellar/atlassian-plugin-sdk/6.2.4/libexec/apache-maven-3.2.1
Java version: 1.7.0_75, vendor: Oracle Corporation
Java home: /Library/Java/JavaVirtualMachines/jdk1.7.0_75.jdk/Contents/Home/jre
Default locale: en_US, platform encoding: UTF-8
OS name: "mac os x", version: "10.11.6", arch: "x86_64", family: "mac"
```

Lines 10 and 11 in the above output show the Java version is 1.7.x rather than 1.8.x

### How to fix it

#### Step 1. Install Oracle Java SE JDK 8

You can download the install files for the latest version on the Oracle website at <a href="http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html" class="uri external-link">http://www.oracle.com/technetwork/java/javase/downloads/jdk8-downloads-2133151.html</a>.

Follow the instructions on the Oracle website to install Java for your system. 

#### Step 2. Set your JAVA\_HOME variable

##### Windows 

The `JAVA_HOME` environment variable specifies the location of the JDK on your system. For Windows users, the default directory is `C:\Program Files\Java\jdk1.8.x_y` , where x\_y is the Java JDK 8 version you have installed*. *To set JAVA\_HOME:

1.  Browse to the `C:\Program Files\Java\jdk1.8.x_y `folder on your system and copy the path to the folder.
2.  Open **Control Panel **&gt; **System**&gt;**Advanced System Settings.**
3.  On the **Advanced** tab click **Environment Variables.**
4.  Locate the **System variables** section and click **New.**
5.  Enter JAVA\_HOME in the **Variable name** field and paste the folder path you copied into the **Variable value** field.
6.  Click **OK** to close the dialog.
7.  Click on **Path** variable in the **System variables ** section and click **Edit**. 
8.  Click **New **and type `%JAVA_HOME%\bin `in the available space.
9.  Close all dialog windows.
10. Open a new  **Command Prompt** window, and run the following command:

    ``` bash
    C:\Users\manthony>javac -version
    javac 1.8.0_91
    ```

     verify that your output is similar to what appears above.

##### Mac / Linux

The `JAVA_HOME` environment variable specifies the location of the JDK on your system. On Mac OS X, if you accepted the defaults when you installed the JDK, this is `/Library/Java/JavaVirtualMachines/1.8.0.jdk/Contents/Home`. On Linux, it may be `/usr/local/jdk`, or a similar location. You should add the JDK's `bin` directory to your `PATH` environment variable as well. This ensures your environment is configured and can locate the `javac` command.

To set your `PATH` and `JAVA_HOME` variables:

1.  Edit the `.bashrc` file in your home directory using your favourite editor (we use vi in this example).

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

5.  Verify you are now seeing the correct result when you enter the command `javac -version` in **terminal**

    ``` bash
    host:~ test$ javac -version
    javac 1.8.0_91 
    ```

Still Stuck? Request support at <a href="https://ecosystem.atlassian.net/servicedesk/customer/portal/14" class="external-link">Developer Technical Support Portal</a>























































































