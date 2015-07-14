Deploying IBM i2 Intelligence Analysis Platform Developer Essentials
====================================================================

IBM i2 Intelligence Analysis Platform Developer Essentials is a set of files and example projects that build on the standard Deployment Toolkit. You can deploy Developer Essentials on a single workstation.

Before you begin
----------------

IBM i2 Intelligence Analysis Platform Developer Essentials has a longer and more specific set of requirements than the platform itself. Before you begin, you must have access to all of the following software:
-   IBM Installation Manager 1.8
-   IBM i2 Intelligence Analysis Platform 3.0.11
-   IBM DB2 10.5 Express Edition (or Express-C Edition)
-   Web Server Plug-ins for IBM WebSphere Application Server 8.5.5
-   IBM HTTP Server 8.5
-   Eclipse Luna (Eclipse IDE for Java EE Developers)

About this task
---------------

The deployment process for Intelligence Analysis Platform Developer Essentials follows the same sequence as the deployment process for the Intelligence Analysis Platform. As a result, many of the steps in these instructions make reference to the Intelligence Analysis Platform Deployment Guide. It is helpful to keep that guide open as you read the steps in this document.

Procedure
---------

In the first part of the procedure, you use Developer Essentials to create a custom version of the Deployment Toolkit. The libraries and settings that you add enable development for the Intelligence Analysis Platform on a single computer.

1.  <span class="ph cmd">Install IBM i2 Intelligence Analysis Platform 3.0.11 according to the instructions in the release notes.</span> If you accept all of the default settings, the Deployment Toolkit is installed to `C:\IBM\iap`.
2.  <span class="ph cmd">Install all the other prerequisite software and accept all of the default settings, apart from the target directory for IBM HTTP Server that should be set to `C:\IBM\HTTPServer`, and the Web Server Plug-ins for IBM WebSphere Application Server that should be set to `C:\IBM\WebSphere\Plugins`.</span>
    <span class="notetitle">Note:</span> Developer Essentials uses IBM DB2 Express Edition, which does not create Windows groups when you install it. Record the details of the `db2admin` user that DB2 creates; you need them later in this procedure.

3.  <span class="ph cmd">Extract Intelligence Analysis Platform Developer Essentials, and copy the `SDK` directory into the `C:\IBM\iap\` directory.</span>
4.  <span class="ph cmd">Check the following files to ensure that the default settings match your environment:</span>
    -   `SDK\sdk-projects\master\toolkit-overides\configuration\environment\iap\environment.properties`
    -   `SDK\sdk-projects\master\toolkit-overides\configuration\environment\http-server.properties`
    -   `SDK\sdk-projects\master\toolkit-overides\configuration\environment\topology.xml`

5.  <span class="ph cmd">Open the file at `SDK\sdk-projects\master\toolkit-overrides\configuration\environment\credentials.properties` in a text editor, and add the user name and password for DB2.</span>

At this stage, configuration of the development version of the Intelligence Analysis Platform is complete. You can now deploy the platform.

1.  <span class="ph cmd"> Open a command prompt as Administrator, and navigate to the `SDK\sdk-projects\master` directory.</span>
2.  <span class="ph cmd">Run the following command:</span>

    ``` pre
    build -t deployExample
    ```

    <span class="notetitle">Note:</span> The development version of the Intelligence Analysis Platform uses a file-based registry of users and groups. Developer Essentials includes definitions of users and groups that correspond to the example security schema. The default users are:
    -   Analyst
    -   Manager
    -   Demo

    For each of these users, the password is password.

Now, the development version of the Intelligence Analysis Platform is ready for use. The remaining steps configure the Eclipse development environment to interact with the platform.

1.  <span class="ph cmd">Start Eclipse Luna, and then open a web browser and navigate to https://developer.ibm.com/wasdev/.</span> This website contains tools and information for developing web applications for WebSphere Application Server Liberty Profile.
2.  <span class="ph cmd">Click **Downloads** and then **Download in Eclipse** to open the tools download page. Follow the instructions on the page to install the tools for **WAS Liberty Profile**.</span>
3.  <span class="ph cmd">In Eclipse, click <span class="ph menucascade">**Window** \> **Preferences**</span> to open the <span class="keyword wintitle">Preferences</span> window.</span>
4.  Optional: <span class="ph cmd">If IBM Java is not the default JRE on your computer, then you must configure it as the default JRE in Eclipse.</span>
    1.  <span class="ph cmd">In the <span class="keyword wintitle">Preferences</span> window, click <span class="ph menucascade">**Java** \> **Installed JREs** \> **Add**</span> to open the <span class="keyword wintitle">Add JRE</span> window.</span>
    2.  <span class="ph cmd">Use the <span class="keyword wintitle">Add JRE</span> window to add a **Standard VM** named **IBM Java**. The default home directory for this JRE is `C:\IBM\iap\deploy-dev\java`.</span>
    3.  <span class="ph cmd">Select the check box that makes IBM Java the default JRE in Eclipse.</span>

5.  <span class="ph cmd">Create a server runtime environment in which the Intelligence Analysis Platform application will run.</span>
    1.  <span class="ph cmd">In the <span class="keyword wintitle">Preferences</span> window, click <span class="ph menucascade">**Server** \> **Runtime Environments** \> **Add**</span> to open the <span class="keyword wintitle">New Server Runtime Environment</span> window.</span>
    2.  <span class="ph cmd">In the <span class="keyword wintitle">New Server Runtime Environment</span> window, click <span class="ph menucascade">**IBM** \> **WebSphere Application Server Liberty Profile**</span>, and then click **Next**.</span>
    3.  <span class="ph cmd">Set the **Path** of the new server runtime environment to `C:\IBM\iap\deploy-dev\wlp`, instruct it to use the default JRE, and then click **Finish**.</span>

6.  <span class="ph cmd">Click **OK** to close the <span class="keyword wintitle">Preferences</span> window.</span>
7.  <span class="ph cmd">Create a server in Eclipse that represents the Intelligence Analysis Platform deployment.</span>
    1.  <span class="ph cmd">In the Eclipse application window, click the **Servers** tab.</span>

        <span class="notetitle">Note:</span> If the **Servers** tab is not visible, click <span class="ph menucascade">**Window** \> **Show View** \> **Servers**</span> to open it.

    2.  <span class="ph cmd">Right-click inside the tab, and then click <span class="ph menucascade">**New** \> **Server**</span> to open the <span class="keyword wintitle">New Server</span> window.</span>
    3.  <span class="ph cmd">In the <span class="keyword wintitle">New Server</span> window, click <span class="ph menucascade">**IBM** \> **WebSphere Application Server Liberty Profile**</span> to select the server type.</span>
    4.  <span class="ph cmd">Change the **Server name** to `iap`, and then click **Next**.</span>
    5.  <span class="ph cmd">From the **Liberty profile server** list, select **iap**, and then click **Finish**.</span>

8.  <span class="ph cmd">Start the development version of the Intelligence Analysis Platform.</span>
    1.  <span class="ph cmd">Inside the **Servers** tab, double-click the **iap** server.</span> A new **iap** tab opens in the top part of the Eclipse application window.
    2.  <span class="ph cmd">Modify the settings in the iap tab:</span>
        -   Clear the **Run applications directly from the workspace** check box
        -   Click <span class="ph menucascade">**Publishing** \> **Never publish automatically**</span>
        -   Press Ctrl+S to save the settings

        <span class="notetitle">Note:</span> These settings mean that in order for any changes that you make to become apparent, you must manually publish your new code to the server.

    3.  <span class="ph cmd">Back inside the **Servers** tab, start the server.</span> When the startup process completes, you have a running instance of the Intelligence Analysis Platform that you can control through Eclipse.

9.  <span class="ph cmd">To test the platform, open a web browser and navigate to http://localhost/apollo. You can log in to the Intelligence Portal with any of the default users.</span>

**Parent topic:** [IBM i2 Intelligence Analysis Platform Developer Essentials](developer_essentials_welcome.html "IBM i2 Intelligence Analysis Platform Developer Essentials contains tools, libraries, and examples that enable development and deployment of custom extensions to the Intelligence Analysis Platform.")

------------------------------------------------------------------------

© Copyright IBM Corporation 2014, 2015.

