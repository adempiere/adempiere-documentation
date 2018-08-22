---
description: >-
  This page provides advice on securing the ADempiere application and database
  servers.  The advice here should be applied in production environments.
---

# Securing Your ADempiere Installation

## Securing Access to the Application Server and Database

Servers used in production environments should be setup using industry standard security measures. Here are some suggestions. It is recommended that you seek the advice of your IT department and security experts to provide the highest level of security.

### General Security Measures

* **Restrict user access to the servers**
  * Disable all the default vendor/special user accounts and groups that come with your server and that you do not intend to use. For example:
    * Users: adm, lp, shutdown, halt, news, mail, uucp, operator, games, gopher, ftp etc...
    * User groups: adm, lp, news, mail, uucp, games, dip etc...
  * Disable root logins via ssh
  * Disable password authentication for ssh, force private key based access only
  * Use sudo to control system access
  * On the ADempiere application server, create a user **adempiere** with restricted access and install adempiere with ADEMPIERE\_HOME = /home/adempiere/ so that only that user has access to the application.
    * Set the permissions on the .properties files \(i.e. adempiere.properties, AdempiereEnv.properties etc...\) to be readable only by adempiere user as the file contains the database and keystore passwords.
  * For a PostgreSQL database server, the install of the database will create a user **postgres** with limited access. Disable terminal login for the user **postgres**. To disable user postgres edit the file /etc/passwd to find the line `postgres:x:118:125:PostgreSQL administrator,,,:/var/lib/postgresql:/bin/bash`and replace with`postgres:x:118:125:PostgreSQL administrator,,,:/var/lib/postgresql:/usr/sbin/nologin`
* * Configure postgres security \(pg\_hba.conf\) using MD5 password hash and IP filtering. If using ZK Web User Interface only, restrict access to the application server only
* **Limit the function of the servers to the intended purpose**
  * Limit, disable or uninstall all other applications and services which could provide means of attack \(ftp, inetd, sendmail, etc...\)
  * Disable or Secure JMX or web consoles unless these are actually needed. If required, enable authentication and limit access to specific known IP addresses
  * Secure tomcat/jboss by removing all default applications \(i.e. sample apps and manager console app\). Run tomcat and jboss with a restricted user such as the adempiere user.
* **Protect the servers**
  * Ensure the servers are behind firewalls and are not accessible to the Internet directly
  * Enable firewall rules to restrict access to specific ports and IP addresses \(if possible\). Only open the ports required. Use secure ports that require https:// rather than the standard 443.
  * Limit web service connections to known IP addresses, such as a specific server running an Internet site or web store.
  * Provide a secure means of communication with the server such as VPN or remote desktop \(NX, Citrix, etc...\)
  * Configure postgres security \(pg\_hba.conf\) using MD5 password hash and IP filtering \(for zk only restrict to local interface\)
  * Install and configure security software such as Fail2Ban which will attempt to detect and repel intrusions and brute-force attacks.
  * Install anti-virus software
* **Watch and Maintain**
  * Keep all software applications up to date with the latest security patches
  * Reguarily review security and access logs

#### Securing the ADempiere Application

* Setup the ADempiere application using the **adempiere** user.
* Use a port other than the standard 80 \(for example 8081\).
* Consider using a local IP address. For example, edit the AdempiereENV.properties file and change the IP address for the application server to 127.0.0.1. \(You can't do this through RUN\_Setup\).
* Do not expose the ADempiere application to the web or internet directly. Always access the application through a firewall using a suitable means of access.
* Expose ADempiere webstore and services only through a separate Apache proxy server or by limiting access and routing with jboss/tomcat. To set up the proxy in Apache:
  * In httpd.conf \(/etc/httpd/conf/httpd.conf in Fedora\)
    * Enable modules for proxy \(normally enabled by default\):

```text
LoadModule proxy_module modules/mod_proxy.so
LoadModule proxy_connect_module modules/mod_proxy_connect.so
LoadModule proxy_http_module modules/mod_proxy_http.so
```

Then add the following lines to your httpd.conf:

```text
SetEnv force-proxy-request-1.0 1

ProxyPass /wstore http://127.0.0.1:8081/wstore
ProxyPassReverse /wstore http://127.0.0.1:8081/wstore
```

If you want to expose the Web Store to an address other than wstore \(e.g. root web site /\), you also need to change the cookie path in order for the login to work:

```text
ProxyPassReverseCookiePath /wstore /
```

You can also expose the admin interface

```text
ProxyPass /admin http://127.0.0.1:8081/admin
ProxyPassReverse /admin http://127.0.0.1:8081/admin
```

Or simply expose the whole installation

```text
ProxyPass / http://127.0.0.1:8081/
ProxyPassReverse / http://127.0.0.1:8081/
```

> \| [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) \| **Note:**The port and the IP address can/must be changed if you used different IP/port for RUN\_setup.sh \| \| :--- \| :--- \|

* Be wary of "free" parameters in web services. Use these wisely as they can be a vector for an attack. For example through unrestricted filters or allowing accesses to any table. It is recommended to be specific with web service requests.
* Secure access to the server
  * Use SSH public/private keys for access to the server
  * Use the server's operating system permission mechanisms to limit execution of the application and database to particular users with limited access
  * Limited access to specific IP addresses - especially on the database, the only access allowed should be the application server
  * Keep ADempiere behind a firewall and limit access using standard corporate security means such as VPN, remote connections or other RSA
  * Use LDAP \(which can be enabled and managed through ADempiere\) to provide more secure password access
* For the database, follow the security advice of the database being used. Some of the key concepts are
  * Ensure the database server only responds to the application server
  * Limit the access of the database data to a single user with limited permissions. Run the database under this user.
* Monitor your installations and logs regularly

### Securing the Software

It is important that the ADempiere code be built using a secure private key and that all jars are signed. ADempiere provides a means to do so through the java keystore when RUN\_Setup is executed. During every build/rebuild of ADempiere its binaries are unpacked, signed and repacked again \(to the according JARs, WARs, EARs\). Java security prevents any code modifications and won't allow unsigned jars to run. This prevents bytecode insertion attacks which can be an issue where hot-swappable code is allowed, such as in OSGI implementations.

When you first execute RUN\_Setup, a dialog will appear allowing you to create a keystore. Alternatively, you can edit the AdempiereENV.properties file and define an existing keystore. If one doesn't exist it will be created automatically. This creation is done by the JDK's native keytool.exe which is being called automatically within the installation process. System Admins are obligated to do nothing more than to fill all the provided variables for the Keystore setting and Certificate details sections of the AdempiereEnv.properties file. For more information search for the documentation on the java keytool.

### Securing User Passwords

All security measures depend on adequate passwords. Ensure all system admin passwords are strong and secure. Draconian password policies for end-users can backfire if end-users are writing down the passwords or sharing accounts to get around the policies - find a suitable level of security for your corporation and enforce it.

ADempiere, by default, does not encrypt data. **System admins should enable encryption on all fields/columns that contain sensitive data** including user passwords. In the demo sites and on initial install, these fields are not encrypted so it is important to take action.

As part of Release 380, a password salt and hash feature was added that will encrypt all passwords in an unrecoverable form. The password hash can be applied on migration from earlier releases and will encrypt all passwords in the database.

**Change all standard user passwords in the system** - SuperUser, System, GardenAdmin, GardenUser. After all are changed then log in as System in role System Adminsitrator. Find and run the process "convert all passwords to hashes". Open the User window, open the record for System, look at the password field and confirm it is hashed \(full of asterisks\). Check the other passwords as well.

