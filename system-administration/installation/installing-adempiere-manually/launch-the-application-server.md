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

## As a Service on Linux

ADempiere can be setup a service on Ubuntu using systemd. 

 Create a file called "adempiere.service" under the /lib/systemd/system/ directory

```text
[Unit] Description=Task that runs the ADempiere ERP Service After=network.target After=systemd-user-sessions.service After=network-online.target
[Service] Environment=ADEMPIERE_HOME=/opt/Adempiere Type=forking ExecStart=/opt/Adempiere/utils/RUN_Server2.sh ExecStop=/opt/Adempiere/utils/RUN_Server2Stop.sh TimeoutSec=30 Restart=on-failure RestartSec=30 StartLimitInterval=350 StartLimitBurst=10
[Install] WantedBy=multi-user.target
```

With the service defined, you can run the following commands to control it. You will need to run these as root or using `sudo`

| Command | Purpose |
| :--- | :--- |
| `systemctl daemon-reload`  | Loads the new service |
| `systemctl start adempiere` | Starts the ADempiere service. |
| `service adempiere status` | Show the status of the ADempiere service |
| `systemctl enable adempiere` | Enable the ADempiere service to it will restart on the next reboot/restart event. |
| `systemctl stop adempiere` | Stop the ADempiere service |
| `systemctl disable adempiere` | Turns the ADempiere service off at the next reboot/restart event. Prevents the ADempiere service from restarting. |
| `systemctl is-enabled adempiere` | Use this to check if the service is currently configured to start or not on the next reboot. |

{% hint style="info" %}
The systemd script may fail if the memory runs out.  When the heap is full for some reason, the stop script will fail.   In that case,  try kill -9 using the service PID, wait for a few seconds then start the service again. System Administrators should add a health check to handle this condition.
{% endhint %}

If the server started with no errors, you can move on to [Launching the ADempiere Application](../../../introduction/getting-started/launching-the-application.md).

\(Thanks to [@pmdw](https://github.com/pmdw) and [Horacio Miranda @piracio](https://github.com/piracio) for their contribution.\)

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

Check the logs for errors. 

For JBoss, the logs are located at ADEMPIERE\_HOME/jboss/server/adempiere/logs or ADEMPIERE\_HOME/jboss/bin.

For Tomcat, you will find them in ADEMPIERE\_HOME/tomcat/log/Catalina.out.

The most common problems are with ports that are already in use. Typical conflicting ports are:

* HTTP: 80, 443, 8080, 8443
* RMI : 1098, 1099

For Linux users, sometimes it helps to restart the workstation/server and execute RUN\_Server2 as root.

**Any port conflict when starting the Application Server must be resolved!**

If you have errors related to the database, check that the database has been installed, ADempiere data imported and that the database server is running.

