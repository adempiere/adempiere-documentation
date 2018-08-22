---
description: >-
  The third main step in installing the application, this page describes the
  initialization of the database.
---

# Initialize the Database

After having installed the database and setup the ADempiere Application Server, the database needs to be initialized prior to launching the Application Server and any client software.

> | [![Image:Note.gif](http://wiki.adempiere.net/images/6/62/Note.gif)](http://wiki.adempiere.net/File:Note.gif) | **Note:** The utility scripts provided with the Application software need to have access to the database functions in order to run. In a network installation, you may have to copy the database executable files to the Application Server machine, install a local copy of the database on the application server or manually install the seed database on the database server. Detailed instructions are provided below. |
> | :--- | :--- |

Before starting with the database creation, you should have the following installed:

* a suitable database \(i.e. Oracle XXg, Oracle XXgXE, PostgreSQL, MySQL\) and that the database server is running. See [Database Server Installation & Setup](database-server-installation-and-setup.md).
* the application server installation is complete. See [Application Server Installation & Setup](application-server-installation-and-setup.md).

## Database Creation

The database created when you installed Oracle/Postgres/MySQL has no ADempiere data. Before the ADempiere application can run, a suitable database must be created. This can be done by installing the **Seed Database** provided with the software or by restoring a previously created database.

### Database Creation from the Seed

The initial ADempiere Seed database is imported from the Adempiere.dmp file for Oracle or Adempiere\_pg.dmp for PostgreSQL, located in the ADEMPIERE\_HOME/data directory.

Open shell and change directories to the ADEMPIERE\_HOME/utils directory.

> | [![Image:Caution.gif](http://wiki.adempiere.net/images/3/3f/Caution.gif)](http://wiki.adempiere.net/File:Caution.gif) | **Caution!** The following script will **DROP** any existing adempiere database. Do not run this command if you already have data loaded. |
> | :--- | :--- |

Run the script **RUN\_ImportAdempiere** \(.bat or .sh\).

You will see information about .dmp file \(such as date creation, size, etc.\) and the message: **== The import will show warnings. This is Ok ==**

 [![](http://wiki.adempiere.net/images/0/0c/CD_Run_ImportAdempiere.PNG)](http://wiki.adempiere.net/File:CD_Run_ImportAdempiere.PNG)

Press any key to start the process.

Don't worry if you see warnings \(such as "Warning: object created with compilation warnings"\). This is normal and can be ignored. After the import has finished, an SQL procedure makes sure that everything has been imported correctly and will list any invalid objects.

 [![](http://wiki.adempiere.net/images/f/f4/CD_Run_ImportAdempiere2.PNG)](http://wiki.adempiere.net/File:CD_Run_ImportAdempiere2.PNG)

At the process end, you should see a message similar to the one displayed below, with the text "no rows selected".

 [![](http://wiki.adempiere.net/images/2/28/CD_Run_ImportAdempiere3.PNG)](http://wiki.adempiere.net/File:CD_Run_ImportAdempiere3.PNG)

A common cause of problems when running this script is not having the environment variables set properly. The script will not run if ADEMPIERE\_HOME, JAVA\_HOME are set incorrectly or if the database executables are not on the path. It may also be necessary to add the Postgres/Oracle bin directory to the PATH environment variable in some environments.

### Next Step

The next step is [Complete ADempiere Server Install](http://wiki.adempiere.net/InstallComplete).

### Notes

* For Oracle Users:
  * Please make sure that the tablespaces for the database user Adempiere exist. The Default database tablespace names are:
    * default tablespace= **USER** \(150 MB, 10 MB Autoextend\),
    * index tablespace= **INDX** \(100 MB, 10 MB Autoextend\),
    * temporary tablespace= **TEMP** \(100 MB, 10 MB Autoextend\).
  * The setup script have been changed to use the EZCONNECT naming method instead of TNSNAMES. Open your Oracle Net Manager, under profile -&gt; Naming, make sure EZCONNECT is one of the selected methods. Alternatively, verify that the SQLNET.ORA file has the following entries: NAMES.DIRECTORY\_PATH = \(EZCONNECT,TNSNAMES\)

### Installation Details

The script RUN\_ImportAdempiere simply calls the script ImportAdempiere in the $ADEMPIERE\_HOME/utils/&lt;database&gt; directory. The version of ImportAdempiere called deals with the specific setup needs of the various databases.

Since 3.8.0, the RUN\_ImportAdempiere script will also import and apply any migrations found in the $ADEMPIERE\_HOME/migrations directory.

Following the database import, the database is **signed** - to indicate the version of the database.

The ImportAdempiere script is called with the following parameters:

* system/%ADEMPIERE\_DB\_SYSTEM% \(not used in PostgreSQL installation\)
*  %ADEMPIERE\_DB\_USER% \(typically Adempiere\)
*  %ADEMPIERE\_DB\_PASSWORD% \(typically Adempiere\)
*  %ADEMPIERE\_DB\_SYSTEM% \(typically postgres - not used in the oracle installation\)

In addition, the following environment variables are required and should have been set by the Application Setup process:

* ADEMPIERE\_HOME e.g. D:\ADEMPIERE2
* ADEMPIERE\_DB\_NAME e.g. adempiere or xe
* ADEMPIERE\_DB\_SERVER e.g. dbserver.adempiere.org
* ADEMPIERE\_DB\_PORT e.g. 5432 or 1521

The descriptions below are not correct code and are intended for information purposes only. See the actual scripts for the details.

#### Postgres

The ADEMPIERE\_HOME/utils/postgresql/ImportAdempiere script will run the following commands:

```text
-- Drop the ADempiere database if it exists
dropdb -h %ADEMPIERE_DB_SERVER% -p %ADEMPIERE_DB_PORT% -U postgres %ADEMPIERE_DB_NAME%

-- Drop the ADempiere user if it exists
dropuser -h %ADEMPIERE_DB_SERVER% -p %ADEMPIERE_DB_PORT% -U postgres %ADEMPIERE_DB_PASSWORD%

-- Recreate the ADempiere user
set ADEMPIERE_CREATE_ROLE_SQL=CREATE ROLE %ADEMPIERE_DB_USER% SUPERUSER LOGIN PASSWORD '%ADEMPIERE_DB_PASSWORD%'
psql -h %ADEMPIERE_DB_SERVER% -p %ADEMPIERE_DB_PORT% -U postgres -c "%ADEMPIERE_CREATE_ROLE_SQL%"

-- Create the ADempiere database (empty)
set PGPASSWORD=%ADEMPIERE_DB_PASSWORD%
createdb -h %ADEMPIERE_DB_SERVER% -p %ADEMPIERE_DB_PORT% -E UNICODE -O %ADEMPIERE_DB_USER% -U %ADEMPIERE_DB_USER% %ADEMPIERE_DB_NAME%

-- Import the seed data
@psql -h %ADEMPIERE_DB_SERVER% -p %ADEMPIERE_DB_PORT% -d %ADEMPIERE_DB_NAME% -U %ADEMPIERE_DB_USER% -f %ADEMPIERE_HOME%/data/Adempiere_pg.dmp
```

#### Oracle and OracleXE

The ADEMPIERE\_HOME/utils/oracle\(XE\)/ImportAdempiere script will run the following commands:

```text
-- Re-Create DB user
sqlplus system/%ADEMPIERE_DB_SYSTEM%@%ADEMPIERE_DB_SERVER%:%ADEMPIERE_DB_PORT%/%ADEMPIERE_DB_NAME% _
   @%ADEMPIERE_HOME%\Utils\%ADEMPIERE_DB_PATH%\CreateUser.sql %ADEMPIERE_DB_USER% %ADEMPIERE_DB_SYSTEM%

-- Import Adempiere.dmp
imp system/%ADEMPIERE_DB_SYSTEM%@%ADEMPIERE_DB_SERVER%:%ADEMPIERE_DB_PORT%/%ADEMPIERE_DB_NAME% _
   FILE=%ADEMPIERE_HOME%\data\Adempiere.dmp FROMUSER=(reference) TOUSER=%ADEMPIERE_DB_USER% STATISTICS=RECALCULATE

-- Create SQLJ 
call %ADEMPIERE_HOME%\Utils\%ADEMPIERE_DB_PATH%\create %ADEMPIERE_DB_USER%/%ADEMPIERE_DB_PASSWORD%

-- System Check - The Import phase showed warnings. 
-- This is OK as long as the following does not show errors
sqlplus %ADEMPIERE_DB_USER%/%ADEMPIERE_DB_PASSWORD%@%ADEMPIERE_DB_SERVER%:%ADEMPIERE_DB_PORT%/%ADEMPIERE_DB_NAME% _
   @%ADEMPIERE_HOME%\Utils\%ADEMPIERE_DB_PATH%\AfterImport.sql
```

### See Also

* [Complete ADempiere Server Install](http://wiki.adempiere.net/InstallComplete) is the next thing after Create ADempiere Database.
* [Initial Client Setup](http://wiki.adempiere.net/ManPageX_InitialClientSetup) is the starting business setup within ADempiere.
* [Getting Started](http://wiki.adempiere.net/Getting_Started) Tutorial on how to setup and configure ADempiere.
* [Tutorials](http://wiki.adempiere.net/Tutorials) on many things from basic to advanced.
* If you have any further problems installing the Oracle database or you would like to remove it, additional information can be found in here: [\[1\]](http://download-east.oracle.com/docs/cd/B25329_01/doc/install.102/b25143/toc.htm#CIHDDHJD)

