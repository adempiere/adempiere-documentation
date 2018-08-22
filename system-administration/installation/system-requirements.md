---
description: A list of system requirements for the ADempiere application.
---

# System Requirements

ADempiere system requirements vary considerably with the complexity of the enterprise being supported. This page provides a minimum set of system requirements.

It is possible to install ADempiere on a single computer with the database, server and client all running on the same machine. This is quite adequate for evaluation or very small applications. In a production environment such a simple installation may not be sufficient, especially when there are more than a handful of concurrent users. Performance demands will require more attention to the architecture of the installation. In a production environment, it is highly recommended to separate the servers, with the [Application Server](http://en.wikipedia.org/wiki/Application_server) and [Database Server](http://en.wikipedia.org/wiki/Database_server) on different machines.

> \| [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) \| **Note:** Proper database server architecture and database tuning is essential to efficient operation. For installations with more than 10 users, ensure you do your homework. See specifics about your database or consult with a database specialist for correct hardware architecture, database tuning and query tuning.For PostgreSQL, see [Postgres Performance](http://wiki.postgresql.org/wiki/Category:Performance) [Hardware Design](http://www.postgresql.org/files/documentation/books/aw_pgsql/hw_performance/) [Tuning Your PostgreSQL Server](http://wiki.postgresql.org/wiki/Tuning_Your_PostgreSQL_Server) [Using EXPLAIN \(Query Tuning\)](http://wiki.postgresql.org/wiki/Using_EXPLAIN) \| \| :--- \| :--- \|

The following sections describe the main requirements and options.

## ADempiere Application Server Requirements

### Software

* Operating Systems - any one of the following
  * Microsoft Vista, Windows 7 or later \(Support for will be limited by the supporting stack of Java and database.\)
  * Linux
    * Suse \*
    * Red Hat \*
    * CentOS
    * Debian / Ubuntu
    * FreeBSD
  * Unix
    * OpenSolaris
  * MAC OSX

### Hardware

* Architecture of hardware
  * [Intel](http://en.wikipedia.org/wiki/XEON)
  * [AMD Opteron](http://en.wikipedia.org/wiki/Opteron)
  * [Sparc](http://en.wikipedia.org/wiki/SPARC)\]
  * [Power](http://en.wikipedia.org/wiki/Power_Architecture)
  * [Itanium](http://en.wikipedia.org/wiki/Itanium)

### Databases

* Oracle 10g release 2 \(Express, Standard and Enterprise editions\)

> \| [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) \| **Note:** The export utility \(used by RUN\_DBExport\) on 11g doesn't export empty tables by default. Some configuration of the database is needed or you need to use a different tool. For that reason, 11g is not "officially" supported. \| \| :--- \| :--- \|

* PostgreSQL 8.2 or better
* MySQL

### Stack Required

* \(Versions 3.7.0 and below\) Java 2 Platform Standard Edition 5.0 or higher
* \(Version 3.8.0 and above\) Java 2 Platform Standard Edition 7.0 or higher
* JBoss
* Apache-ant 1.6 or higher.

### Technologies Used

* Java
* JavaServer pages \(JSP\)
* Servlets
* EJB
* SQL/SQLJ
* XML
* HTML/CSS
* PDF

### Client Side

For web start or web application:

* Browsers
  * Firefox 2.0 or better
  * Google Chrome
  * Safari 2 or better
  * Internet Explorer 7.0 or better
  * Java 2 Platform Standard Edition 5.0 or higher

For client application

* Java 2 Platform Standard Edition 5.0 or higher
* Operating Systems - any one of the following
  * Microsoft Windows 2000, XP\*, Vista or newer
  * Linux
    * Suse \*
    * Red Hat \*
    * CentOS
    * Debian / Ubuntu
    * FreeBSD
  * Unix
    * OpenSolaris
  * MAC OSX

