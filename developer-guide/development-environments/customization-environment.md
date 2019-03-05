---
description: How to setup a customization environment for ADempiere software
---

# Customization Environment

This tutorial will show you how to customize the ADempiere core software without making changes to the ADempiere project directly. Customization changes are instead included in customization.jar and zkcustomization.jar which can be deployed in the ADempiere install.

## Introduction

Sometimes you realize that ADempiere does not perfectly suit your needs and you need to make some changes to parts of the source code. Some customizations are not possible to achieve through ADempiere’s [Application Dictionary](http://wiki.adempiere.net/Application_Dictionary) and you have to modify the source code for that. The recommended way of customizing the software is to do it in a separate project. There you can create your customized classes and generate customization jar archives that can be added to ADempiere during the installation build.

## How to setup up your environment

You will need to have two projects in your development environment: one for the ADempiere project and one for your customized code that will become the new application and will depend on the ADempiere project. A Customization Template is provided to help you get started.

### Create the ADempiere Project

1. If you haven't already done so, follow the [ADempiere Version Control](../adempiere-version-control.md) process to fork, clone and checkout the target branch of the ADempiere project you wish to customize.
2. [Create your ADempiere development environment](./) and, if you are modifying the zk interface, [setup your WebUI Workspace using Eclipse Webtool](creating-webui-workspace-using-eclipse-webtool.md).
3. Build the ADempiere application \(using utils\_dev/build.xml\), install, setup the software \(to create the .properties file\) and import the database seed.
4. Modify the launch configurations as required and test that you can run the client and zk interfaces for the ADempiere project.

You now have the main ADempiere project created. Changes to this project should be made as part of the [Software Development Procedure](../software-development-procedure.md) to fix bugs, add features and generate common code that will be shared by all ADempiere implementations.

### Create the Customization Project

Fork the customization template project on GitHub from here: [https://github.com/adempiere/Customization-Template](https://github.com/adempiere/Customization-Template).

Add the forked code as a new project to your IDE workspace that contains the ADempiere project you created above.

In the template, modify the utils\_dev/buildCustomization.properties file to point to the correct directories.

## General Customization

Most of the code in the ADempiere project can be customized by replacing the project classes with new ones archived in the customization.jar file in ADEMPIERE\_HOME/lib. This will not affect the server or the ZK interface which have to be dealt with differently.

In the IDE, it is sufficient to copy the target source code, following the same directory structure, from the ADempiere project into your customization project and modify it there. When you run the customized application, you should see your changes.

The template provide sample build scripts to archive the resulting customized class files into the customization.jar which you will need to add to your installation ADEMPIERE\_HOME/lib directory prior to running RUN\_Setup or RUN\_SilentSetup.

## Customization of the ZK interface

Customization and debugging of the ZK interface is a bit more involved as the IDE needs ALL the classes in one project to run them on a server. To keep the customizations separate from the main ADempiere project requires a bit of work. In general, all the ZK classes needed to run the WebUI have to be copied to the customization project but you only need to copy the source for the classes you are customizing. There are scripts provided to help with this.

As a demo, the template has only one file LoginPanel.java which changes the login header to "My Customization Works!". If you want to test with this demo, follow the instructions below but don't delete or overwrite this file in step 2 below.

1. Delete all the contents of the zkwebui folder in the template except for the build\_custom.xml file.
2. Copy the zkwebui directory from the ADempire project to the template. Be careful not to overwrite the build\_custom.xml file in the template. This will provide the same deployment structure as the main ADempiere project. \(This step is necessary and could be automated but risks overwriting your customization so it has been left as a manual process.\)
3. Delete the zkwebui/WEB-INF/src source tree, leaving only the files you wish to customize. 
4. Open the launch configuration "MyCustomizationProject InitializeZKCustomizations" which you will find in the directory tools/launchers. Replace the name of MyCustomizationProject with the actual name of your project in the launcher.  Run the launcher MyCustomizationProject InitializeZKCustomizations - this will copy all the classes needed from the adempiere project to the template. Depending on the version of ADempiere, you may need to modify the associated build.xml file. Note, if you run the build target by hand from the build file, don't forget to refresh the project files.
5. If you are customizing zk, add a server and add the cutomization project to the server. In the server launcher, the class path for the user entries needs to include the following:
6. C:/dev/apache/tomcat-6.0/bin/bootstrap.jar
7. adempiereTrunk/tools/lib/jnlp.jar
8. adempiereTrunk/tools/lib/javaee.jar
9. adempiereTrunk/tools/lib/jcommon-1.0.18.jar
10. adempiereTrunk/tools/lib/jfreechart-1.0.15.jar
11. adempiereTrunk/tools/lib/log4j.jar
12. adempiereTrunk/JasperReportsTools/lib/jasperreports-5.1.0.jar
13. adempiereTrunk/tools/lib/c3p0-0.9.1.2.jar
14. adempiereTrunk/tools/lib/iText-2.1.7.jar
15. adempiereTrunk/tools/lib/poi-3.9-20121203.jar
16. adempiereTrunk/lib/postgresql.jar
17. adempiereTrunk/tools/lib/commons-net-1.4.0.jar
18. adempiereTrunk/tools/lib/commons-collections-3.1.jar
19. adempiereTrunk/tools/lib/barbecue-1.5-beta1.jar

These are the defaults in the launcher included with the project. You will need to point the path in the launcher at the correct project name for the ADempiere project and you may have to add/change the libraries based on the version of ADempiere you are using.

## Testing with the template

With the setup complete, the template should be good to go. You may need to update the build files to adjust to ADempiere versions. If you customize other directories than build and client, also copy the build.xml files from those directories in the ADempiere project and modify them to add the customized classes to the jar files. Compare the build.xml from the base directory in both the template and the ADempiere project.

If you launch the server, you should see the changes in the zk files. If you make any changes, you will have to restart the server to see them.

The launcher for the client will run the client as per the main project. Here, most changes you make will be hot-swapped into the application which is really nice for development.

## Exporting the Customization Jars

When your customization is ready, there is a launcher to build the customization jars. The two files customization.jar and zkcustomization.jar will be added to the lib directory. You can add these to the lib directory of the ADempiere installation \(ADEMPIERE\_HOME/lib\) and execute the setup \(RUN\_Setup or RUN\_SilentSetup\) to see the changes.

**References**: [http://en.wikiversity.org/wiki/Adempiere\_Technical\_Training\#Project\_Customization\_Management\_Hints](http://en.wikiversity.org/wiki/Adempiere_Technical_Training#Project_Customization_Management_Hints)

Enjoy !

