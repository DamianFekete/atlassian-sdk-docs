---
aliases:
- /server/framework/atlassian-sdk/explore-the-installed-sdk-and-the-atlas-commands-10421987.html
- /server/framework/atlassian-sdk/explore-the-installed-sdk-and-the-atlas-commands-10421987.md
category: devguide
confluence_id: 10421987
dac_edit_link: https://developer.atlassian.com/pages/editpage.action?cjm=wozere&pageId=10421987
dac_view_link: https://developer.atlassian.com/pages/viewpage.action?cjm=wozere&pageId=10421987
learning: tutorials
legacy_url: https://developer.atlassian.com/docs/getting-started/set-up-the-atlassian-plugin-sdk-and-build-a-project/explore-the-installed-sdk-and-the-atlas-commands
new_url: /server/framework/atlassian-sdk/explore-the-installed-sdk-and-the-atlas-commands
platform: server
product: atlassian-sdk
subcategory: learning
title: Explore the installed SDK and the atlas commands
---
# Explore the installed SDK and the atlas commands

You should understand the basic contents and functions of the SDK before you develop your first add-on. On this page, you get a summary of the SDK contents, a very brief intro to Apache Maven, and you run an Atlassian application through the SDK. The following topics are covered:

 

## Step 1: Browse the SDK contents and get introduced to Maven

Maven is a popular tool and you may already be using it. You don't need to be a Maven expert to use this tutorial. You do need to understand some Maven basics to develop with the SDK. Examine the contents of the SDK installation:

1.  Navigate to the directory where the Atlassian SDK (the ATLAS\_HOME) was installed.  
    Not sure where the SDK was installed? Use the `atlas-version` command.  If you are on a Mac or other Linux system you may need to preface your command with `sudo`.
2.  List the contents of the `ATLAS_HOME` directory.  
    The SDK contains the following directories:

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>Directory</p></th>
    <th><p>Description</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><code>apache-maven</code></p></td>
    <td><p>Contains the Apache Maven 2 installation. Maven is a popular build management tool. Atlassian built a suite tools around Maven called the Atlassian Maven Plugin Suite (AMPS). These tools automate many add-on development tasks.</p></td>
    </tr>
    <tr class="even">
    <td><p><code>bin</code></p></td>
    <td><p>Contains command-line wrappers for the most common AMPS calls. All of the commands start with the <code>atlas-</code> prefix.<br />
    In this tutorial, you do all your development with the wrapper commands. This is the typical case. Only very rarely, and then only for very advanced techniques, should you need to work with AMPS directly.</p></td>
    </tr>
    <tr class="odd">
    <td><p><code>repository</code></p></td>
    <td><p>Contains code repositories that the Atlassian SDK is dependent on. This directory is prepopulated during the SDK installation.</p></td>
    </tr>
    </tbody>
    </table>

3.  Take some time to list the contents of each of the three sub-directories.

Maven relies on the ability to navigate to external repositories URLs and obtain source packages required by your code. When you build an add-on such as a plugin using the SDK's `atlas-` commands, Maven is behind the scenes retrieving the latest Atlassian source files from Atlassian's public repositories. Atlassian preconfigures the location of these repositories in the `ATLAS_HOME/apache-maven/conf/settings.xml` file.

## Step 2: (Optional) Configure a &lt;proxy&gt; in the Maven `settings.xml`

If you're doing your development behind a corporate firewall, you may need to connect to the Internet through an HTTP proxy. If you know you do not have a firewall, skip this procedure. If you know your company requires you to use an HTTP proxy, you need to configure proxy settings in the `ATLAS_HOME/apache-maven/conf/settings.xml` file. Do the following:

1.  Ask your system administrator to provide you with the following information:  
    -   The proxy address `protocol://host:port`, for example `https://our.company:8080`.
    -   a username/password required for access
    -   a list of hosts that don't require a proxy
2.  Edit the `ATLAS_HOME/apache-maven/conf/settings.xml` file in your favorite editor.
3.  Locate the `<proxies>` section.  
    <img src="/server/framework/atlassian-sdk/images/proxies.png" width="700" />
4.  Uncomment the `proxy` element.
5.  Edit the `proxy` element and add the values provided by your system administrator.  
    When you are done, the element looks similar to the following:

    ``` xml
      <proxies>
        <proxy>
          <id>myproxy</id>
          <active>true</active>
          <protocol>http</protocol>
          <host>proxy.somewhere.com</host>
          <port>8080</port>
          <username>proxyuser</username>
          <password>somepassword</password>
          <nonProxyHosts>*.google.com|ibiblio.org</nonProxyHosts>
        </proxy>
      </proxies>
    ```

6.  Close and save the file.

**Have an Existing settings.xml File in Your .m2 Directory?**

If you have an existing local `settings.xml` file, you may encounter problems resolving dependencies required by the SDK commands. To prevent these problems, add the following `<pluginRepository>` block to your local `settings.xml` profile:

  Expand source

``` xml
<pluginRepository>
    <id>atlassian-plugin-sdk</id>
    <url>file://${env.ATLAS_HOME}/repository</url>
     <releases>
        <enabled>true</enabled>
        <checksumPolicy>warn</checksumPolicy>
      </releases>
      <snapshots>
         <enabled>false</enabled>
      </snapshots>
 </pluginRepository>
```

## Step 3: Try an atlas command

At this point, you've configured your environment and you are set to begin developing. This tutorial shows you how to add a very simple `helloworld` plugin to JIRA. Before you begin writing code, you should use an `atlas` command to run JIRA in standalone mode. You use the atlas-run-standalone command to start JIRA.

If you haven't already done so, open a command window and do the following:

1.  Navigate to the root of your drive (Windows) or home directory (Linux).

    <table>
    <colgroup>
    <col style="width: 50%" />
    <col style="width: 50%" />
    </colgroup>
    <thead>
    <tr class="header">
    <th><p>Windows</p></th>
    <th><p>Linux/Mac</p></th>
    </tr>
    </thead>
    <tbody>
    <tr class="odd">
    <td><p><code>cd C:</code></p></td>
    <td><p><code>cd ~</code></p></td>
    </tr>
    </tbody>
    </table>

2.  Create a directory called `atlastutorial`.

    ``` bash
    mkdir atlastutorial
    ```

3.  Change directory to your newly created directory.

    ``` bash
    cd atlastutorial
    ```

4.  Start latest version of JIRA on default port of 2990, by entering the following:

    ``` bash
    atlas-run-standalone --product jira
    ```

    After the command completes successfully you see a message similar to the following:

    ``` bash
    [INFO] Starting jira on the tomcat6x container on ports 2990 (http) and 52641 (rmi)
    [INFO] using codehaus cargo v1.2.3
    [INFO] [cargo:start]
    [INFO] [2.ContainerStartMojo] Resolved container artifact org.codehaus.cargo:cargo-core-container-tomcat:jar:1.2.3 for container tomcat6x
    [INFO] [stalledLocalDeployer] Deploying [/Users/manthony/atlastutorial/amps-standalone/target/jira/jira.war] to [/Users/manthony/atlastutorial/amps-standalone/target/container/tomcat6x/cargo-jira-home/webapps]...
    [INFO] [talledLocalContainer] Tomcat 6.x starting...
    [INFO] [talledLocalContainer] Tomcat 6.x started on port [2990]
    [INFO] jira started successfully in 249s at http://localhost:2990/jira
    [INFO] Type Ctrl-D to shutdown gracefully
    [INFO] Type Ctrl-C to exit
    ```

    The output message tells you the URL where JIRA was started.

5.  Open a browser and enter the JIRA URL.  
    You should see the URL for your installation displayed in the run output. For example, you might see `http://myhost.local:2990/jira` or `http://localhost:2990/jira`<a href="http://localhost:2990/jira" class="external-link"> depending on your environment. On successful launch, the browser displays the JIRA login page.</a>
6.  Enter `admin` for both the username and password.  
    Your browser displays the JIRA dashboard:  
    <img src="/server/framework/atlassian-sdk/images/jira-dash.png" width="700" />  
    You'll notice in the **Admin** section the **License** that you are running is a `Test license for plugin developers`.

### Go behind the scenes of atlas-run-standalone

When you issue the `atlas-run-standalone` command, it creates a directory called `amps-standalone` in the current directory - in this case `atlastutorial/amps-standalone`.  
JIRA runs as a Tomcat web application on your `localhost` -- the system on which you issue the command. So, the command actually runs a Maven build on your system. This build

-   creates a directory called `amps-standalone/target` in the current `atlastutorial` directory
-   downloads the latest JIRA product files to your machine
-   downloads any dependencies JIRA needs to run this version of JIRA
-   builds the JIRA application
-   creates a Tomcat 6 container
-   deploys JIRA in the container

The `amps-standalone/target/jira-5.0.log` file contains the details such as the environment variables set and used during this process. You'll notice from this log file that the JIRA test instance relies on an HSQL database. You would never use an HSQL database in a production system.

## Step 4: State is saved between runs

When you run a standalone instance, you can make changes in the instance. The system remembers what you do between sessions. At this point, you should still have your standalone JIRA instance up and running. Make sure you are logged in and do the following:

1.  Locate the Admin section on Dashboard.
2.  Choose the **create new** link from the **Projects** section.  
    The system opens the **Create New Project** page.
3.  Name your project `Test Project` and give it a key of `TEST`.  
    When you are done, the dialog looks similar to the following:  
    ![](/server/framework/atlassian-sdk/images/test-proj.png)
4.  Click **Add** to add the project.  
    Your standalone JIRA now has a TEST project. Test what happens to the project when you restart this standalone instance.
5.  Return to the command line where you started JIRA.
6.  Gracefully shutdown JIRA by pressing CTRL-Z (Windows) or CTRL-D (Linux).
7.  Browse to the default JIRA URL (`http://myhost.local:2990/jira or http://localhost:2990/jira)` with your browser.  
    Your browser should inform you that it could not get a connection to the server.
8.  Return to the command line (DOS prompt for Windows users).
9.  Make sure you are in the `atlastutorial` directory.
10. Restart JIRA standalone.

    ``` bash
    atlas-run-standalone --product jira
    ```

11. Log back in and locate your project.  
    The standalone instance has retained the data you created between restarts. This can be very useful when testing. You'll learn more about this later.

**Extra Exploration**

You can use the `atlas-run-standalone` command to run a particular version of a product. This is useful if, for instance, you want to test your code on an earlier version of JIRA or Confluence. Review the [command's reference page](/server/framework/atlassian-sdk/atlas-run-standalone) and try running an earlier version of JIRA.

## Next steps

At this point, you have some basic understanding of the SDK. Enough to go ahead in the [next tutorial section to create your own plugin project](/server/framework/atlassian-sdk/create-a-helloworld-plugin-project).








































































































































