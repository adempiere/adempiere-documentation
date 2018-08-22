---
description: This page provides advice on installation of the ADempiere application server.
---

# Application Server Installation and Setup

This page is directed at System Administrators who need to install the **ADempiere Application Server** in a network environment where the database server could be running on a separate network server and the clients run on remote computers. 

### Prerequisites

Before continuing, ensure you have installed a suitable database \(i.e. Oracle 10g, Oracle 10gXE, PostgreSQL, MySQL\) and that the database server is running. See [Database Server Installation & Setup](database-server-installation-and-setup.md).

### Required Downloads

Download each of the following packages:

* **Java SE Development Kit** - Get the latest from [http://www.oracle.com/](http://www.oracle.com/technetwork/java/javase/downloads/index.html). You only need the JDK without JavaFX, EE or NetBeans bundles.
* **ADempiere Latest Release** - Download the latest ADempiere from [here](https://github.com/adempiere/adempiere/releases).
* **ADempiere Patches** - Any patches or customization jars to apply.

### Install Java

Install the JAVA JDK with the default installation settings. Say OK to install the follow-on JRE as well. Carefully note the full path for the JDK directory \(e.g: C:\Program Files\java\jdk1.5.0\_19\) and the JRE directory that you have just installed.

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**There may well be a number of JDK and JRE directories, so choose the right one! The JDK should include the JRE. |
> | :--- | :--- |

The ADempiere scripts rely on the existence of a system environment variable JAVA\_HOME. When the scripts call java, they use the full path as JAVA\_HOME/bin/java so it is important that this variable exist.

Following the instructions for your system, add a new System Variable JAVA\_HOME for your new JDK directory. Set JAVA\_HOME to C:\Program Files\Java\jdk1.7.0\_25 \(or whatever your JDK directory is called\).

According to your OS, append the following JDK path to the system path: 

`%JAVA_HOME%\bin` or 

`$JAVA_HOME/bin`

### Install the ADempiere Software

There is no install script. Just extract the ADempiere archive to a suitable location: \(e.g. c:\ or /u01/\). For reference, call this directory ADEMPIERE\_ROOT. You should end up with the files in a folder like ADEMPIERE\_ROOT\Adempiere. For reference, call this folder ADEMPIERE\_HOME.

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note: Avoid spaces in the directory path**. The batch scripts do not like directory names with spaces. If using a ADEMPIERE\_ROOT with multiple directories, avoid directory names with spaces. |
> | :--- | :--- |

#### Apply the Patches

Patches are a combination of \*.jar files, which replace \*.jar files in the ADEMPIERE\_HOME\lib directory, and migration scripts which update the database. In the Patches directory on Source Forge, there may be more than one type of \*.jar that needs patching. If you downloaded one or more patch files, replace the existing file with the downloaded one, changing its name to match. For example, copy the \*\_patches\_\*.jar file to ADEMPIERE\_HOME\lib\patches.jar, overwriting the existing file. See the detailed instructions in [Patches Installation](http://wiki.adempiere.net/Patches_Installation).

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**It is a good idea to rename the existing \*.jar file to something like patches.jar.old before you replace it with the the new file |
> | :--- | :--- |

#### Apply Customizations, Packages and other Files

If you have a customization.jar with customized code or a packages.jar file with supporting \*.jar files, add them to the ADEMPIERE\_HOME\lib directory, overwriting the existing files.

For migration scripts which end in .xml, store these in the ADEMPIERE\_HOME/migration directory.

### Setting Up The ADempiere Server

The Application Server is configured by a utility RUN\_Setup.\(sh/bat\) found in the ADEMPIERE\_HOME directory. This utility launches a tool where the configuration settings can be set and tested. Once everything passes the tests, the configuration is saved and the software repackages itself with the new settings. You can then launch the Application Server.

You can rerun this utility as many times as you like until everything is correct.

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:** In case you are changing settings on an existing Application Server, make sure that the Application Server is shut down before you start. Otherwise you will get port errors during the testing. You can shut down the Application server by running the script RUN\_Server2Stop.\(sh/bat\) from ADEMPIERE\_HOME/utils or by stopping the "service". |
> | :--- | :--- |

In a command shell with administrative privileges, run the script **RUN\_Setup**, located in the ADEMPIERE\_HOME directory. The ADempiere Server Setup window should appear as shown below:

![ADempiere Server Setup window](../../../.gitbook/assets/image.png)

The Setup window opens and loads its values from the file AdempiereEnv.properties. It looks for this file in the ADEMPIERE\_HOME directory. If the environment variable ADEMPIERE\_HOME is not set or is null, it will look in the directory defined in the system property "user.dir".

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**The setup process creates a file named Adempiere.properties. This is the main configuration file for your Client. You can copy this file and pass it as a variable when you start ADempiere using the command line interface parameter-DPropertyFile=AdempiereProduction.properties.  If you create several files you can use them to easily switch between development, test and production environments, for example. |
> | :--- | :--- |

#### Setup Fields

Fill in the setup window fields as follows:

* Java
  * **Java Home**: select the SDK Java Home location \(e.g. C:\jdk1.5.0\_05\). This should be the same as the JAVA\_HOME environment variable.
  * **Java VM**: the Java Virtual Engine Vendor \(Default= Sun\).
* Adempiere
  * **ADempiere Home**: is the base directory where the distribution files are located \(e.g. C:\Adempiere\). This should be the same a the ADEMPIERE\_HOME environment variable.
  * **KeyStore Password**: ADempiere requires a SSL certificate. It automatically creates a certificate in the key store $ADEMPIERE\_HOME/keystore/myKeystore with the keystore password entered. The self certified certificate created has the alias adempiere and uses the same password as the keystore. You can replace the certificate used with the Java "keytool" \(see Java tool documentation\).
* Application Server
  * **Application Server**: is the name, URL or IP of your server PC \(Don't use localhost\). The Application Server defaults to the server currently running the program. Avoid using IP addresses - use the DNS name of the server.
  * **Web Port**: The web port that the Application Server will listen on. Access to the application server will be through a URL similar to http://myApplicationServer:webport \(http://appserver:8088\). Please keep in mind that, under Linux/Unix, ports under 1000 need root privileges. If you use Apache as a front end, you may need to use ports like 8080 or 8088 - basically, find a free port. The default ports is 80
  * **SSL**: The secure socket layer port. The default is 443. If that is not available try another value such as 4443 or 8443.
  * **JNP Port**: The Java Name Provider and Remote Method Invocation\(RMI\) port. The Default ports are 1099 \(1098\).
* Database Server
  * **Database Server**: The Database Server defaults to the server currently running the program. Avoid using IP addresses - use the DNS name of the server. Localhost can be used only if the database server is running on the same machine as the Application Server and client software. For Oracle, the Service names are discovered. You can overwrite the entries if they are not correct.
  * **Database Name**:
    * PosgreSQL: PostgreSQL database name
    * Oracle: SID/Service name. Oracle 10g/11g default: orcl, OracleXE default: xe
  * **Database Type**: select the database you have installed \(i.e. Oracle 10g, Oracle 10gXE, PostgreSQL\).
  * **Database Port**: select the port for connect to database.\(i.e. Oracle use 1521 as standard port, PostgreSQL 5432, etc.\)
  * **System Password:**
    * Oracle: Password for the system user.
    * PostgreSQL: Password for the postgres user.
  * **Database User**: The application database user name, default is adempiere.
  * **Database Password**: The application database password, default is adempiere.
* Mail Server \(See notes below\)
  * **Server**: ****the mail server  \(e.g. smtp.gmail.com\)
  * **Port**: the mail server port for sending mail
  * **Protocol**: the protocol to use, SMTP or IMAP
  * **Admin E-Mail**: The email to use as the From address
  * **Encryption Type**: The type of encryption to use
  * **Auth. Mechanism**: how the account is authorized.  Login is the default.
  * **Mail User**: the mail user login name
  * **Mail Password**: the mail user password

Mail setup is optional but a server does have to be identified.  The Setup Tool will finish successfully whether the mail tests work or not. You can maintain the mail server connection in the Application on a Client basis from the [**Client Window**](http://wiki.adempiere.net/ManPageW_Client). If you don't want to setup mail or don't have an SMTP server, just enter a valid server - the field defaults to the local computer name. As long as the server exists, the setup will finish successfully. 

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**The software only needs a method to send email. There is no ability to read email in the application. |
> | :--- | :--- |

#### Testing the Setup

After you fill the Setup fields, press the Test button to verify them. As the test progresses, you will see the boxes checked \(√\). Only if all the parameters are verified will you will not be able to save them. If an entry cannot be verified, a pop-up window stating the error will be displayed Fix it and test again.

If, for example, the Application Server name is wrong, then you will see a message such as:

 [![](http://wiki.adempiere.net/images/c/c1/IS_ServerSetupError.PNG)](http://wiki.adempiere.net/File:IS_ServerSetupError.PNG)

When all the tests pass \(you can see the boxes checked: √ \):

![ADempiere Server Setup with the test results shown](../../../.gitbook/assets/image%20%281%29.png)

* press the Save button. This will save the settings to the AdempiereEnv.properties file in the ADEMPIERE\_HOME directory.
* After you accept the license, you will see the dialog:

 [![](http://wiki.adempiere.net/images/5/55/IS_EnvironmentSaved.PNG)](http://wiki.adempiere.net/File:IS_EnvironmentSaved.PNG)

* Press the OK button to continue and take a look into the log. Make sure that you see the **BUILD SUCCESSFUL** and **Done**, such as:

```text
     [echo] AppsDeployment= C:\Adempiere\jboss\server\adempiere\deploy
     [copy] Copying 1 file to C:\Adempiere\jboss\server\adempiere\deploy
     [copy] Copying 1 file to C:\Adempiere\jboss\server\adempiere\deploy
     [copy] Copying 1 file to C:\Adempiere\jboss\server\adempiere\deploy
     [copy] Copying 1 file to C:\Adempiere\jboss\server\adempiere\deploy

 setupTomcat:

 setupDeploy:
     [echo] AppsDeployment= C:\Adempiere\jboss\server\adempiere\deploy

 setup:
 
BUILD SUCCESSFUL
Total time: 2 minutes 22 seconds

*** 2006-12-28 14:15:35.53 Adempiere Log (CLogConsole) ***
ErrorLevel = 0
===================================
Setup Client Environment
===================================
SET ADEMPIERE_HOME=C:\Adempiere
SET JAVA_HOME=c:\Archivos de programa\Java\jdk1.5.0_05
Path is OK = c:\Archivos de programa\Java\jdk1.5.0_05\bin;C:\Archivos de programa\Java\jdk1.5.0_05\
bin;C:\oraclexe\app\oracle\product\10.2.0\server\bin;%SystemRoot%\system32;%SystemRoot%;
%SystemRoot%\System32\Wbem
Created Shortcut Adempiere.lnk
Created Shortcut Adempiere Web Site.url
Done
.
For problems, check log file in base directory
```

If something is wrong, you can fix it and rerun the script until everything is correct.

Once the setup is complete, you can move on to [Initialize the ADempiere Database](http://wiki.adempiere.net/Initialize_the_ADempiere_Database).

### Common Issues

* **Application Server** \* **Database Server** is the name, URL or IP of your server PC.
* **JNP Port = 1099** error means that a previous service is running. Kill it. Also, since this is the first port that is tested, it could also mean that you have a mismatch between your host name \(in the hosts file\) and your actual IP address. Fix it in "/etc/hosts" \(linux\)
* **Database Port = 1521** error can be solved by restarting DB machine.
* **System** & **Database Passwords** are those defined when you setup your Database.
* **Mail Server** is optional. RUN\_Setup can still finish without it.

#### Java Home Error

If you receive the following message:

 [![](http://wiki.adempiere.net/images/5/54/IS_JAVA_HOME_ERROR.PNG)](http://wiki.adempiere.net/File:IS_JAVA_HOME_ERROR.PNG)

You should check your java environment variables. Check that the JAVA\_HOME system environment variable points to the correct directory.

#### Web Port Error

If you receive the following message from the installer:

 [![](http://wiki.adempiere.net/images/e/e8/Adempiereerror1.png)](http://wiki.adempiere.net/File:Adempiereerror1.png)

it is likely that you have some other web server running or, if your are using Linux, you need the appropriate privileges.

The default ports are: 80 for http connections and 443 for SSL connections. This message means that the user is not allowed to use the port, likely because it is already used by another application. Change the port to something else. WebPort 8088 and SSL 4443 are recommended. If you are using Linux, remember that ports under 1000 need root privileges. If you are using Oracle database, port 8080 might be used.

#### JNP Port 1099 Error

Another possible error is Server Setup Error Error JNP Port \(Not correct: JNP Port = 1099\) OK

The JNP Port = 1099 error can be caused by another process which is already attached to that TCP port. Take a look what process is using this port and so you can take steps to stop it. It can also be caused by a mismatch between your IP address and the entry in your hosts file. See /etc/hosts\(linux\) or %SystemRoot%/system32/drivers/etc/hosts\(windows\).

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:**To find the IP address of your server try the following in a command script:Linux /sbin/ifconfigWindows IPCONFIG |
> | :--- | :--- |

#### JNP Name Not Found Exception

This error is usually related to a DNS problem. It is possible to complete the setup using IP addresses when installing with PostgreSQL. Make sure you have a working DNS environment or add an entry in /etc/hosts\(linux\) or %SystemRoot%/system32/drivers/etc/hosts\(windows\).

### See Also

* [Initialize the ADempiere Database](http://wiki.adempiere.net/Initialize_the_ADempiere_Database) is the next thing after Install Server.
* [Launching the ADempiere Application](http://wiki.adempiere.net/Launching_the_ADempiere_Application) to perform the Client-Server client install which is the next thing to do after completing the Database setup.
* [Initial Client Setup](http://wiki.adempiere.net/ManPageX_InitialClientSetup) is the starting business setup within ADempiere.
* [Getting Started](http://wiki.adempiere.net/Getting_Started) Tutorial on how to setup and configure ADempiere for single computer operation \(database, application and client all on the same machine\).
* [Tutorials](http://wiki.adempiere.net/Tutorials) on many things from basic to advanced.

