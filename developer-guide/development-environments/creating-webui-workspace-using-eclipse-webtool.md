---
description: Instructions on how to setup Eclipse to allow debugging of the web interface.
---

# Creating WebUI Workspace using Eclipse Webtool

## Configuring Eclipse for the WebUI

This article is a follow-on to [Development Environments](./) and describes how to modify the ADempiere project and your development environment to enable debugging of the zk webui using the Eclipse Webtool. Eclipse Webtool support was added in version 341. This additions allows you to run or debug the Zk web client using the Eclipse webtool \(Europa JEE and above \) and Apache Tomcat.

### Setup the Project to Include the Webtool Support

Before you start, see [Development Environments](./) and ensure you can build and debug the SWING client.

Additional checklist items

* If you do not have an Eclipse Java EE version, you have to install the following plugin in your Eclipse, otherwise you will not see nor be able to configure the Server view in Eclipse:
  * Eclipse Java EE Tools, 
  * JST Server Adapters and 
  * JST Server Adapters Extensions. 
* If you do need to install the plugins, make sure you call the menu entry **Help/Install new Software** and in the field "Work with", select the url for your version of eclipse, e.g. for Luna: [http://download.eclipse.org/releases/luna](http://download.eclipse.org/releases/luna).
* It may be necessary that you have to configure Tomcat manually \(according to [http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html](http://www.coreservlets.com/Apache-Tomcat-Tutorial/tomcat-7-with-eclipse.html)\): Copy the directory /your-tomcat-base-directory/webapps/ROOT to /your-workspace/.metadata/.plugins/org.eclipse.wst.server.core/tmp0/wtpwebapps.

### Setup the Webtool

As the webtool is not setup by default, there is a bit of work to do each time you update the main project branch. Here are the steps:

1. Checkout the ADempiere branch of interest and build it using the ant build in utils\_dev/build.xml.
2. Open the Properties for the ADempiere project
3. Select Project Facets and, if its not already in faceted form, click the link, "Convert to faceted form..."
4. Confirm that Dynamic Web Module is selected \(Version 2.5 or higher is OK.\)
5. Confirm that Java is selected \(select a JAVA version compatible with the code in the project\)
6. Close the Project Facets and click Web Project Settings in the Project Properties dialog.  You should see the web context root as "webui".  If it shows an error "Context Root cannot be empty". This is a problem with the eclipse luna version and you'll need to check that the following "natures" are included in the eclipse .project file \(there may be others but you need at least these two\):
   1. &lt;nature&gt;org.eclipse.wst.common.modulecore.ModuleCoreNature&lt;/nature&gt;
   2. &lt;nature&gt;org.eclipse.wst.common.project.facet.core.nature&lt;/nature&gt;
7. Refresh the project and look at the Project Properties, Web Project Settings again. You should see the context root as "webui".
8. Now add servers to Eclipse. Its easiest to do this by right clicking in the server tab and selecting "New" or clicking the link to add servers if you see it. In the dialog that appears you can select the server you want to use and download it to a directory. Apache Tomcat V6.0. installed in a directory like c:\dev\apache will work. The server should identify the available web projects and you can add the ADempiere project to the server.
9. Right click the server and select Run. Note that this won't work but it will publish the project and create a launch configuration for it.  Stop the sever if it doesn't stop automatically.
10. Edit the launch configuration and add the following to the arguments: -DPropertyFile=${adempierePropertiesFile} -DADEMPIERE\_HOME=${ADEMPIERE\_HOME} \(Note: These arguments use variables but you could replace the variable with the relevant paths. The adempiere.properties file needs to exist which is why you need to build and install ADempiere before you can debug the webui.\)
11. Save the configuration.
12. Run the server launcher again from the debug configuration. Check the console for errors. It should startup normally.
13. Once the server has started, open a browser and go to localhost:port/webui. Usually, Tomcat uses port 8080. You should see the standard login page. You can now insert breakpoints in the webui code and interact with the code from the browser.
14. To make it easier to reproduce these steps, make a stash of these changes in git and reapply them from the stash when you switch to a new branch.

To customize the zk interface, see [Create your ADempiere customization environment](http://wiki.adempiere.net/Create_your_ADempiere_customization_environment).

If you have any questions, please join our [chat](http://www.adempiere.net/web/guest/chat-on-line).

### Opening the Web Interface in Eclipse

If you want that ADempiere ZK opens in Eclipse

* Select ADempiere Project
* Right mouse click
* Select either Run As/Run on Server or Debug As/Debug on Server
* In the opening dialog select server and resource, press finish
* The Adempiere ZK login dialog opens in an Eclipse view.

## See Also

* [Youtube: Servlet development using Eclipse and Tomcat](http://www.youtube.com/watch?v=EOkN5IPoJVs)
* [Create and Run Your First ZK Application with Eclipse](http://books.zkoss.org/wiki/ZK_Installation_Guide/Quick_Start/Create_and_Run_Your_First_ZK_Application_with_Eclipse_and_ZK_Studio)
* Q: [Debugging ZK webUI](http://sourceforge.net/projects/adempiere/forums/forum/610548/topic/4852616)

