---
description: >-
  How to run the ADempiere Application Server as a standalone process or a
  service.
---

# Launch the Application Server

## Prerequisites

Before launching the Application Server, you should already have completed:

* [Database Server Installation & Setup](database-server-installation-and-setup.md)
* [Application Server Installation & Setup](application-server-installation-and-setup.md)
* [Initialize the ADempiere Database](initialize-the-database.md)

If the above are completed, you can start the JBoss-based ADempiere Application Server. For demonstrations, its fine to launch the server from a console. For production systems, its best to use a method that will keep the server running after the user has logged off.

## Run the Server as a Stand-Alone Process

To run the ADempiere Server from a console, open up a console window and go to the ADEMPIERE\_HOME/utils directory. Run the script RUN\_Server2\[.bat\|.sh\] . Then you will see the RUN\_Server2 output, such as:

[![](http://wiki.adempiere.net/images/7/75/IS_RUN_Server2.PNG)](http://wiki.adempiere.net/File:IS_RUN_Server2.PNG)

If the server started with no errors, you can move on to [Launching the ADempiere Application](../../../introduction/getting-started/launching-the-application.md).

## As a Service on Windows Operating Systems

For windows operating systems, the ADempiere Application Server can be installed as a service and scripts are provided for this purpose. Open a DOS shell with Administrative Privileges, navigate to %ADEMPIERE\_HOME%\utils\windows and run:

* Adempiere\_Service\_Install.bat for 32-bit systems; or
* Adempiere\_Service\_Install\_64.bat for 64-bit systems \(since 380LTS hotfix 2\).

The install sets the start-up options as manual. You will need to open the Services Window \(Control Panel→Administrative Tools→Services\) to set the properties so the service starts automatically or manually as required for your implmentation.

\(Since 380LTS hotfix 2\) On 64-bit systems, the service will log the full console output to ADEMPIERE\_HOME\jboss\bin\run.log. As a result, run.log may get large over time. To prevent this, comment out the CONSOLE appender-ref in the ADEMPIERE\_HOME\jboss\server\adempiere\conf\jboss-log4j.xml file:

```text
<root>
     <appender-ref ref="CONSOLE"/>
     <appender-ref ref="FILE"/>
</root>
```

Once the Service is running, you can move on to [Launching the ADempiere Application](launch-the-application-server.md).

## Using nohup on Linux Systems

For other operating systems, check ADEMPIERE\_HOME/utils/unix or use the Linux nohup command \(no hangup\) as follows:

```text
nohup ./RUN_Server2.sh &
```

To see the output of the server, use

```text
cat nohup.out | more
```

or

```text
tail nohup.out
```

If the server started with no errors, you can move on to [Launching the ADempiere Application](../../../introduction/getting-started/launching-the-application.md).

## Trouble Shooting

Check the logs for errors. They are located at ADEMPIERE\_HOME/jboss/server/adempiere/logs or ADEMPIERE\_HOME/jboss/bin.

The most common problems are with ports already in use. Typical conflicting ports are:

* HTTP: 80, 443, 8080, 8443
* RMI : 1098, 1099

For Linux users, sometimes it helps to restart the workstation/server and execute RUN\_Server2 as root.

**Any port conflict when starting the Application Server must be resolved!**

If you have errors related to the database, check that the database has been installed, ADempiere data imported and that the database server is running.

