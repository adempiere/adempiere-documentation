---
description: >-
  This section provide hints and tips on configuring the database to work with
  ADempiere.
---

# Database Server Installation & Setup

## Things to Think About

The ADempiere scripts will need to find the database command line utilities, so set your path to point to the "bin" directory of the database install. You can do this in the same way JAVA\_HOME was used above. Create an environment variable such as DATABASE\_HOME set to the database install directory, and add DATABASE\_HOME/bin to your path according to the methods for your system

{% hint style="info" %}
The ADempiere application utility scripts need access to the database binary commands from the application server machine. You may need to install an empty version of database on the ADempiere application server or, at least, a copy of the necessary binary executable files.
{% endhint %}

{% hint style="warning" %}
If for some twisted reason you also have Oracle running on the same machine as PostgreSQL, be aware that the two databases include some executables with the same name. If you have both POSTGRES\_HOME and the equivalent ORACLE\_HOME on the path, you might have errors when running some of the ADempiere scripts. Try to keep the path pointing to one or the other database at a time and switch between the two as required.
{% endhint %}

## PostgreSQL Installation & Setup

It is recommended that you read the [PostgreSQL Manuals](http://www.postgresql.org/docs/manuals) carefully. There are many useful tips and tricks in the documentation and user comments.

If you use the Postgres Windows Installer, many of the following steps will be done for you by the installer but you will have to pay attention to the security settings.

The following is from the PostgreSQL installation guide after the software has been built and installed from source.

Create a unpriviledged user on the database server computer that is unique to the PostgreSQL installation and has sole access to/ownership of the data the database creates but little else. Don't use this user to install the software but ensure the PostgreSQL server daemon runs under this account. The user "postgres" is a common choice.

Log in as the "postgres" user and [create the database cluster](http://www.postgresql.org/docs/8.4/interactive/creating-cluster.html) - a group of databases. This is done by defining the location where the databases will be stored. This can be anywhere on the file system. The cluster is created with the command initdb which comes with PostgreSQL. The format is

```text
$ initdb -D /usr/local/pgsql/data
```

where /usr/local/pgsql/data is the location of the database cluster. As an alternative to the -D option, the environment variable PGDATA can be defined.

{% hint style="info" %}
If the postgres user is unpriviledged, the initdb command may not be able to create the data directory if it doesn't already exists. In that case, log in as root/administrator and create the data directory before you run the command as the postgres user. The initdb command will remove all access permissions to the data directory for everyone but the postgres user. See the PostgreSQL manuals for additional security settings.
{% endhint %}

It is important to properly set up the [pg\_hba.conf](http://www.postgresql.org/docs/8.4/interactive/auth-pg-hba-conf.html) file to ensure the ADempiere application server can talk with the database. Remote TCP/IP connections will not be possible until this file is modified since the default behavior is to listen for TCP/IP connections only on the local loopback address "localhost". When the application server and the database server are separate machines, the pg\_hba.conf file must be set to allow connections from the application server. For security, use as restrictive a connection as possible.

Follow the instructions to start the database server.

Move on to [Application Server Installation & Setup](application-server-installation-and-setup.md).

## Oracle Installation & Setup

{% hint style="info" %}
The Oracle XE version \(Express Edition\) is available for free but there are limitations on its use in terms of maximum database size, number of running instances allowed, amount of RAM used, number of CPUs used to process queries \(only 1 used\) and a lack of https support. While these limitations are acceptable for demonstrations and development, use in production and multi-user environments is not recommended. Please review the Oracle Database Express Edition documentation on Licensing Restrictions prior to making your choice. If you require Oracle, consider purchasing licenses for the Standard Editions.
{% endhint %}

Oracle installation is straight forward. Follow the instructions in the Oracle documentation.

Move on to [Application Server Installation & Setup](application-server-installation-and-setup.md).

## MySQL Installation & Setup

{% hint style="info" %}
ADempiere integration with MySQL requires developer support. Please verify in the repository and forums if MySQL is supported by the version of ADempiere you wish to use.
{% endhint %}

This section from [Naquib13](http://wiki.adempiere.net/User:Naquib13). He is documenting from Trifon's [SF thread](http://sourceforge.net/projects/adempiere/forums/forum/610546/topic/3854274).

* SUN JDK
* [MySQL 5.x](http://www.mysql.com/downloads/mysql/) I recommend using [Workbench](http://www.mysql.com/downloads/workbench/)
* Do the following after installing the above:
* Change my.cnf file.
* Set tables names to be lower case.
* Enable recursive stored procedures.
* Enable MySQL ANSI mode. $ sudo vim /etc/mysql/my.cnf lower\_case\_table\_names=1 max\_sp\_recursion\_depth=128 sql\_mode='ANSI'
* Restart MySQL server $ sudo /etc/init.d/mysql restart
* Create "adempiere" database $ mysql -u root -p mysql&gt;create database adempiere DEFAULT CHARACTER SET = utf8 DEFAULT COLLATE = utf8\_bin;
* Create "adempiere" MySQL DB user $ mysql -u root -p mysql&gt; GRANT ALL ON adempiere.\* TO 'adempiere'@'localhost' IDENTIFIED BY 'adempiere';
* Import Initial MySQL DB Seed\(ADempiere version 3.6.0LTS\) $ mysql -u adempiere -p -h localhost adempiere &lt; &lt;ADEMPIERE\_HOME&gt;/data/Adempiere\_mysql.dmp
* Follow standard ADempiere installation process $ &lt;ADEMPIERE\_HOME&gt;/RUN\_setup.sh
* Start ADempiere Server $ &lt;ADEMPIERE\_HOME&gt;/utils/RUN\_Server2.sh
* Start ADempeire Swing client $ &lt;ADEMPIERE\_HOME&gt;/RUN\_Adempiere.sh

Move on to [Application Server Installation & Setup](application-server-installation-and-setup.md).

### Links

* [ADempiere on MySQL](http://sourceforge.net/projects/adempiere/forums/forum/610546/topic/3854274)- SF.net thread by Trifon on 2010 & 2011.
* [Running ADempiere on MySQL](http://blogs.sun.com/praneet/entry/mysqling_adempiere) by Praneet on Jul 03, 2009.
* [MySQL Download](http://www.mysql.com/downloads/mysql/)

