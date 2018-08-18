---
description: Steps required to successfully install ADempiere on Windows and Linux servers
---

# Installing ADempiere Manually

## General Installation Instructions

The installation process is similar across operating systems with a few minor exceptions.

This installation instruction is intended for initial installations where the database, application server and client all run on the same machine and a desktop or GUI interface is being used.

* For more complex installations or command-line installations, see [Installation Steps](http://wiki.adempiere.net/Installation_Steps).
* If you already have an ADempiere installation running and you want to update to a newer version, see [Upgrading and Migration](http://wiki.adempiere.net/Upgrading_and_Migration).

An installation can take as little as 15 or 20 minutes.

### Required Downloads

Before you begin, download each of the following packages:

* **Java SE Development Kit** - Get the latest from [http://www.oracle.com/](http://www.oracle.com/technetwork/java/javase/downloads/index.html). You only need the JDK without JavaFX, EE or NetBeans bundles.
* A database. Either
  * **Postgre SQL** - Get the latest Windows install from [http://www.postgresql.org/download/](http://www.postgresql.org/download/) OR
  * **Oracle** - A free "express" version is available from Oracle at [http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html](http://www.oracle.com/technetwork/database/database-technologies/express-edition/downloads/index.html)
* **ADempiere Latest Release** - Download the latest ADempiere from [here](https://github.com/adempiere/adempiere/releases).
* **ADempiere Patches** - Any patches or customization jars to apply.

### Install the Pre-Requisites

#### JAVA

Install the JAVA JDK with the default installation settings. Say OK to install the follow-on JRE as well. Carefully note the full path for the JDK directory \(e.g: C:\Program Files\java\jdk1.5.0\_19\) and the JRE directory that you have just installed.

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**There may well be a number of JDK and JRE directories, so choose the right one! The JDK should include the JRE. |
> | :--- | :--- |

The ADempiere scripts rely on the existence of a system environment variable JAVA\_HOME. When the scripts call java, they use the full path as $JAVA\_HOME/bin/java so it is important that this variable exist.

Following the instructions for your system, add a new System Variable JAVA\_HOME for your new JDK directory:JAVA\_HOME use C:\Program Files\Java\jdk1.7.0\_25 \(or whatever your JDK directory is called\)Append the following JDK path to the system path: %JAVA\_HOME%\bin or $JAVA\_HOME/bin

#### Database

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**You can use an existing Oracle or PostgreSQL database if you already have one installed. If so, gather the passwords for the postgres or system user, check the environment variable and path, verify that the service is running and move on to the next step. |
> | :--- | :--- |

Install database software according to the installation instructions for your system using the defaults to keep things simple. Keep track of passwords and ports since you will need this information in the ADempiere setup.

The ADempiere scripts will need to find the database command line utilities, so set your path to point to the "bin" directory of the database install. You can do this in the same way JAVA\_HOME was used above. Create an environment variable such as DATABASE\_HOME set to the database install directory, and add DATABASE\_HOME/bin to your path according to the methods for your system.

> | [![Image:Caution.gif](http://wiki.adempiere.net/images/3/3f/Caution.gif)](http://wiki.adempiere.net/File:Caution.gif) | **Caution!**If for some twisted reason you also have Oracle running on the same machine as PostgreSQL, be aware that the two databases include some executables with the same name. If you have both POSTGRES\_HOME and the equivalent ORACLE\_HOME on the path, you might have errors when running some of the ADempiere scripts. Try to keep the path pointing to one or the other database at a time and switch between the two as required. |
> | :--- | :--- |

### Install the ADempiere Software

There is no install script. Just extract the ADempiere archive to a suitable location: \(e.g. c:\ or /u01/\). For reference, call this directory $ADEMPIERE\_ROOT. You should end up with the files in a folder like $ADEMPIERE\_ROOT\Adempiere. For reference, call this folder $ADEMPIERE\_HOME.

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:Avoid spaces in the directory path**. The batch scripts do not like directory names with spaces. If using a $ADEMPIERE\_ROOT with multiple directories, avoid directory names with spaces. |
> | :--- | :--- |

#### Apply the Patches

Patches are a combination of \*.jar files, which replace \*.jar files in the $ADEMPIERE\_HOME\lib directory, and migration scripts which update the database. In the Patches directory on Source Forge, there may be more than one type of \*.jar that needs patching. If you downloaded one or more patch files, replace the existing file with the downloaded one, changing its name to match. For example, copy the \*\_patches\_\*.jar file to $ADEMPIERE\_HOME\lib\patches.jar, overwriting the existing file. See the detailed instructions in [Patches Installation](http://wiki.adempiere.net/Patches_Installation).

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**It is a good idea to rename the existing \*.jar file to something like patches.jar.old before you replace it with the the new file |
> | :--- | :--- |

#### Apply Customizations, Packages and other Files

If you have a customization.jar with customized code or a packages.jar file with supporting \*.jar files, add them to the $ADEMPIERE\_HOME\lib directory, overwriting the existing files.

### Initial ADempiere Setup

A setup utility in ADempiere will prepare the software for use and create environment variables needed in the following steps.

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**The setup utility will need to make changes to environment variables. Execute the utility with sufficient permissions to do so. |
> | :--- | :--- |

Navigate to $ADEMPIERE\_HOME and execute RUN\_setup.\[sh\|bat\].

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**In linux systems you may need to change the executable rights of the \*.sh files in the $ADEMPIERE\_HOME directory. |
> | :--- | :--- |

If this is the first time you are installing ADempiere, a licence and security keys dialogs will appear. Accept the defaults.

The setup dialog will appear.

You will need to change:

* Database Server from &lt;your-computer-name&gt; to localhost
* Database Type according to your installed database: oracle, oracleXE or postgresql
* Database Name from xe to adempiere \(You can use another name here if you like\)
* DB Admin Password to postgres \(or whatever you entered above for the database administrator\)
* Database Password to adempiere
* Don't change anything in the Mail Server settings. These can be set up later.

You may also need to change the following:

* Adempiere Home to $ADEMPIERE\_HOME \(e.g. C:\Adempiere\) if somehow it has been set to the wrong location
* Application Server Web Port to 8080 and SSL to 8443 \(instead of 443\). Access to port 80 and 443 is often restricted to system administrators. If ports are already in use, you can choose other open ports. Check for your system how to find open/available ports.

**Press the Test button**

When the Test completes without errors and the Save button \(bottom, right\) is activated, click the Save button. Wait a few minutes until the Adempiere Server Setup screen disappears and the deployment is finished.

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**The database does not have a user adempiere or a database adempiere at this point, so these tests will not be checked. The user and database will be created in the next step. |
> | :--- | :--- |

If you are having problems, see the detailed instructions on this dialog in the pages [InstallServer](http://wiki.adempiere.net/InstallServer) and [ServerSetupHelp](http://wiki.adempiere.net/ServerSetupHelp)

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**The setup process will have created several files in the $ADEMPIERE\_HOME and $ADEMPIERE\_HOME\utils directories with names like adempiere.properties, adempiereEnv.properties and myEnvironment.bat. The adempiere.properties file can be copied to a new name and a different properties file created to, for example, create a sandbox version of the database with a database name like adempiere\_sandbox. |
> | :--- | :--- |

#### Import ADempiere Data

> | [![Image:Caution.gif](http://wiki.adempiere.net/images/3/3f/Caution.gif)](http://wiki.adempiere.net/File:Caution.gif) | **Caution!**The following script will **DROP** any existing adempiere database. Do not run this command if you already have data loaded. |
> | :--- | :--- |

In a shell, navigate to $ADEMPIERE\_HOME\utils and execute '**RUN\_ImportAdempiere.\[sh\|bat\]'**.

See [CreateDatabase](http://wiki.adempiere.net/CreateDatabase) for more information.

#### Apply Migration Scripts

The database installed above will be at the state of the release version and will have all migration scripts applied. You may need to apply migration scripts which were downloaded with the patches.

If you are not installing patches, skip this step.

**SQL - Prior to Release 3.8.0**

The migration scripts can be found in the \*\_migra\_\*.\[zip\|tar\] file downloaded above. Unzip the contents to a convenient directory. The scripts can be applied in a number of ways, using database tools or the command line. Refer to the documentation for your database.

**XML - Since Release 3.8.0**

The XML migration scripts to apply should be saved in the $ADEMPIERE\_HOME\migrations directory. These scripts will be included in \*\_migra\_\*.zip file. Unzip the contents to $ADEMPIERE\_HOME\migrations. To apply the scripts, execute the command $ADEMPIERE\_HOME\utils\RUN\_MigrateXML.\[sh\|bat\] from a shell.

### Run ADempiere

#### Start the Application Server

In a shell, navigate to $ADEMPIERE\_HOME\utils. Execute '**RUN\_Server2.\[sh\|bat\]'** and wait for the server to fully start - it will end this phase with "INFO \[Server\] JBoss .... Started in xx:xx:xx ms", which will take around 30 seconds to 3 minutes depending on your computer.

#### Starting the Application Server Automatically

In Windows, if you would like to run the server as a service, in a shell, navigate to $ADEMPIERE\_HOME\utils\windows and run Adempiere\_Service\_Install.bat. Select the batch file for the type of Windows - 32 or 64 bit.  You will need to open the Services Window \(**Control Panel&gt;Administrative Tools&gt;Services**\) to set the properties so the service starts automatically or manually. 

In linux, you can use **nohup** or an equivalent tool.

### Launching the ADempiere Application

'**Congratulations!'**

At this point, your installation is complete and you can move on to [Launching the ADempiere Application.](../introduction/getting-started/launching-the-application.md)

### Uninstall or Revert to Previous Version

To uninstall the software, simple delete the $ADEMPIERE\_HOME directory. To delete the database, use the database administrator to drop the adempiere database and user.

To revert to the previous version, delete the $ADEMPIERE\_HOME directory and copy the previous version to $ADEMPIERE\_HOME. Restore the backed-up copy of the database using $ADEMPIER\_HOME\utils\RUN\_DBRestore.\[sh\|bat\].

## System Specific Installations

The following links provide detailed instructions for manual installations on various operating systems.

#### Windows

* [Adempiere Install for Windows & PostgreSQL](http://wiki.adempiere.net/Adempiere_Install_for_Windows_%26_PostgreSQL) Updated for version 3.8.0. \(Original page contributed by Bepivin\)
* [How To Install on Oracle 10gXE / WinXP or Win2003 Server](http://www.infotechaccountants.com/topicsar/16200001.htm) \(From [Information Technology Accountants](http://www.infotechaccountants.com/) WebSite\) \(Arabic\)
* [How To Install on Oracle 10gXE / WinXP](http://tyarli.googlepages.com/adempiere2) \(From Tyarli's Home Page\)

#### Linux-General

* [ADempiere via .deb/RPM/apt-get/yum](http://wiki.adempiere.net/ADempiere_via_.deb/RPM/apt-get/yum)
* Using IzPack Installer \( Outdated \) [PostgreSQL & Linux](http://wiki.adempiere.net/ADempiere_Install_Linux%26PostgreSQL)
* Install ADempiere 3.5.3a on Linux \(Chinese\):[ADempiere安装指南-3.5.3a \(Linux\)](http://hi.erp100.com/space-53704-do-blog-id-6766689.html)

#### Linux-Debian/Ubuntu

* [Installing ADempiere 3.7.0 on Ubuntu 11.04](http://wiki.adempiere.net/Installing_ADempiere_3.7.0_on_Ubuntu_11.04)
* [Debian and PostgreSQL Install](http://wiki.adempiere.net/Debian_and_PostgreSQL_Install)
* [Install on Ubuntu 10.04 LTS](http://wiki.adempiere.net/Install_on_Ubuntu_10.04_LTS)
* [Install on Ubuntu 8.04](http://wiki.adempiere.net/Install_on_Ubuntu_8.04) by [Gabriel](http://wiki.adempiere.net/User:Gabriel)
* [Install on Ubuntu 8.10](http://wiki.adempiere.net/Install_on_Ubuntu_8.10) by [Tamás Magyar](http://wiki.adempiere.net/User:Magyusz)
* [ADempiere with Postgresql on Ubuntu 9.04 Jaunty](http://wiki.adempiere.net/ADempiere_with_Postgresql_on_Ubuntu_9.04_Jaunty)
* [ADempiere Dedicated Server](http://wiki.adempiere.net/ADempiere_Dedicated_Server) or utilizing Ubuntu Linux Server Edition just for ADempiere
* Install on Debian \(Chinese\): [在Debian及Postgres上安装Adempiere](http://wiki.adempiere.net/Install_on_Debian_Chinese)
* Install on Ubuntu 7.10 \(Chinese\): [在Ubuntu 7.10上安装Adempiere](http://wiki.adempiere.net/Install_Adempiere_on_Ubuntu_7.10)

#### Linux-RedHat/Fedora

* [Install ADempiere 3.6.0 on Fedora 13 with PostgreSQL](http://wiki.adempiere.net/Installation_Guide_for_AD360,_Postgres_and_Fedora) \([Snantachai](http://wiki.adempiere.net/User:Snantachai)\)
* [Install on Fedora 10 with PostgreSQL](http://wiki.adempiere.net/Install_on_Fedora_10_with_PostgreSQL) \([Wariola](http://wiki.adempiere.net/User:Wariola)\)
* [Install Adempiere 3.5.4 on Centos 5.4 / PostgreSQL 8.4.2 ](http://wiki.adempiere.net/Install_Adempiere_3.5.4_on_Centos_5.4_/_PostgreSQL_8.4.2)by [Michael Judd](http://wiki.adempiere.net/User:Juddm)
* [Adempiere 3.3.0 and PostgreSQL 8.1.9 Installation on CentOS 4.5 \(Thai\)](http://wiki.adempiere.net/Adempiere_3.3.0_and_PostgreSQL_8.1.9_Installation_on_CentOS_4.5_%28Thai%29) by [Sureeraya L.](http://wiki.adempiere.net/User:Sureeraya)
* [How to install Adempiere on CentOS 5.1 \(Xen\) with Postgres](http://wiki.adempiere.net/How_to_install_Adempiere_on_CentOS_5.1_%28Xen%29_with_Postgres) by [Michael Judd](http://wiki.adempiere.net/User:Juddm)

#### Linux-Other

* [Install on Mandriva 2009 \(Spanish\)](http://wiki.adempiere.net/Install_on_Mandriva_2009_%28Spanish%29) by Ana María Orozco and Javier Andrés Cárdenas
* [SLES10 \(64 bit\) and PostgreSQL](http://wiki.adempiere.net/SLES10_64_PostgreSQL) \(by Terence Ng\)
* [How to Install ADempiere on P-Series with IBM JAVA & SLES 64bit](http://wiki.adempiere.net/How_to_Install_ADempiere_on_P-Series_with_IBM_JAVA_%26_SLES_64bit) by [Leroy P.](http://wiki.adempiere.net/index.php?title=User:Python&action=edit&redlink=1)

#### Open Source OS

* [How to Install and Run ADempiere on OpenSolaris and Glassfish](http://wiki.adempiere.net/How_to_Run_ADempiere_on_OpenSoalris) by [Bahman M.](http://wiki.adempiere.net/User:Bmovaqar) and [Praneet Tiwari](http://wiki.adempiere.net/User:Praneet)
* [How To Run ADempiere on FreeBSD](http://wiki.adempiere.net/How_To_Run_ADempiere_on_FreeBSD) by [Bahman M.](http://wiki.adempiere.net/User:Bmovaqar)

#### IBM

* [Installation Guide for ADempiere using WebSphere Application Server](http://wiki.adempiere.net/Installation_Guide_for_ADempiere_using_WebSphere_Application_Server) by [Grant Q](http://wiki.adempiere.net/User:Grantq)
* [Installation Guide for ADempiere on IBM i](http://wiki.adempiere.net/Installation_Guide_for_ADempiere_on_IBM_i) by [Grant Q](http://wiki.adempiere.net/User:Grantq)

#### Other

* [How to install Adempiere with Postgres on MacOSX 10.5](http://wiki.adempiere.net/How_to_install_Adempiere_with_Postgres_on_MacOSX_10.5)

### Installation From Trunk \(SVN\)

* [Manual Installation From Trunk](http://wiki.adempiere.net/Manual_Installation_From_Trunk)
* [AdempiereERP and its pre-requisites complete installation from Trunk \(SVN\)](http://wiki.adempiere.net/ADempiere_Installation) [\(in ppt format\)](http://vulms.vu.edu.pk/Courses/cs619/Downloads/VOSS_ADempiere_Installation_Guide_Windows.zip) VOSS Com AdempiereERP installation guide is a complete, comprehensive and sequential installation guide of AdempiereERP and its pre-requisites for Windows platform. The unique and prominent feature of this installation guide is that it has information to install all components or prerequisites of AdempiereERP in a single file. Contributed by [VOSSCom](http://wiki.adempiere.net/User:Vosscom) \([Virtual University](http://www.vu.edu.pk/) \(of Pakistan\) Open Source Software Community\)

### OS and DB Setup

* [Manual postgres setup in linux](http://wiki.adempiere.net/Manual_postgres_setup_in_linux)

### Step By Step Series

contributed by [Alejandro Falcone](http://wiki.adempiere.net/User:Afalcone)

* [InstallServer](http://wiki.adempiere.net/InstallServer) for setup at server after Database is done
* [Launching the ADempiere Application](http://wiki.adempiere.net/Launching_the_ADempiere_Application) for client side where remote PC users can login
* [InitialClientSetup](http://wiki.adempiere.net/ManPageX_InitialClientSetup) starting the Business Client Setup

### Application Server Setup

* Alternate setup using [Glassfish](http://blogs.sun.com/praneet/entry/running_adempiere_in_glassfish) by Praneet Tiwari.
* ADempiere on [OpenSolaris and Glassfish](http://www.adempiere.com/index.php/How_to_Run_ADempiere_on_OpenSolaris#Running_ADempiere_3.53_on_OpenSolaris_2008.05_with_Glassfish_Application_Server) by [Praneet Tiwari](http://wiki.adempiere.net/User:Praneet).

