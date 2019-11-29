---
description: >-
  Instructions for upgrading the application and migrating the data to the new
  version.
---

# Upgrading and Migration

One of the great features of ADempiere is that upgrades and migration to new releases are always free! The process of migration is relatively simple with the migration tools that have been added in release 3.8.0.

There are two main activities:

1. Upgrade your software; and
2. Migrate your database to ensure all the necessary fields and data are compatible with  the software.

{% hint style="warning" %}
 **Caution!**  Back up your database \(utils/RUN\_DBExport\) and make a copy of the contents of the application directory \($ADEMPIERE\_HOME\) before attempting to upgrade your system. The installation of the latest version of software may overwrite needed files so its best to have them all backed up. In production environments, stage the upgrade in a test environment first.
{% endhint %}

## Software Upgrades

The software that drives the application is always being upgraded with fixes and new features. Keeping an implementation up-to-date helps the users benefit from the work of the community.

When upgrading the software, it is important that any customized code incorporated with the implementation works with the upgrade. If you are not sure, please contact the developers of your customization or ask for assistance. Developers should be able to provide you with all the elements of the upgrade, ensuring the main code, patches and customizations will all work together.

### Upgrade to a New Release

Advise users that the software will be off-line during the upgrade. Shut down the application server.

Download from GitHub or generate from your development environment, the version of software you want to upgrade to. This will be in the form of a zip or tar file like "Release\_380lts.zip".

Copy your ADEMPIERE\_HOME directory or rename it. For example, from c:\adempiere to c:\adempiere\_old.

If you are installing over top of the existing installation, you should, as a minimum, delete the contents of the following.

* ADEMPIERE\_HOME\migration \(since 3.8.0\)
* ADEMPIERE\_HOME\lib
* ADEMPIERE\_HOME\jboss

Extract the new ADempiere archive to the ADEMPIERE\_ROOT directory \(i.e. if ADEMPIERE\_HOME is c:\adempiere, extract to c:\\).

### **Apply Patches**

Patches are a combination of \*.jar files, which replace \*.jar files in the ADEMPIERE\_HOME\lib directory. In the Patches directory on GitHub, there may be more than one type of \*.jar that needs patching. If you downloaded one or more patch files, replace the existing file with the downloaded one, changing its name to match. For example, copy the \*\_patches\_\*.jar file to ADEMPIERE\_HOME\lib\patches.jar, overwriting the existing file. See the detailed instructions in [Patches Installation](http://wiki.adempiere.net/Patches_Installation).

{% hint style="info" %}
 If you are updating a patch file, it is a good idea to rename the existing \*.jar file to something like patches.jar.old.
{% endhint %}

### **Apply Customizations, Packages and other Files**

{% hint style="info" %}
 Ensure that any customizations applied are compatible with the target software version.
{% endhint %}

If you have a customization.jar with customized code or a packages.jar file with supporting \*.jar files, add them to the $ADEMPIERE\_HOME\lib directory, overwriting the existing files.

Also, if you have other customized files, such as \*.bat files, a CustomReport.war file, images, etc..., don't forget to add them to the new installation.

When all the files have been added, RUN\_Setup \(or RUN\_SilentSetup if you kept the .properties files in $ADEMPIERE\_HOME\) to build the application.

## Database Migration

The next step is to update the database. Prior to 3.8.0, this was done by applying sql files in sequence which required access to database tools. With release 3.8.0 a new [ADempiere Migration Tool](http://wiki.adempiere.net/Migrate) has been added that makes the process much simpler. In summary, rather than apply scripts to one database to change it into another, the Migration tool compares the production database with the reference \(or seed\) database and ensures that all the necessary dictionary elements are in place. The tool is very versatile and allows for migrations across multiple releases of the software and transfers of databases from one vendor to another. For more details, please refer to the [Migration Tool](http://wiki.adempiere.net/Migrate) manual.

To use the tool, you will first need to import the seed database as the reference. You do this with the script RUN\_ImportReference.\[sh\|bat\]. When the import is complete, execute the script RUN\_Migrate.\[sh\|bat\] to launch the [Migration Tool](http://wiki.adempiere.net/Migrate). If the tool has identified the database settings correctly, you can simply click **Start Migration** and let the tool complete the task. Most production databases will require some intervention so refer to the Migration Tool manual for more detailed instructions.

### Migration with XML or SQL Scripts

It may be necessary to further migrate the database by applying scripts that are included in patches or customizations and that haven't been applied to the seed or reference database. XML migrations can be applied by executing RUN\_MigrateXML.\[sh\|bat\] following the installation and build of the software. The xml scripts to apply should be found/saved in the ADEMPIERE\_HOME/migration directory. SQL scripts can be applied with any one of a number of tools. The process is similar to generating a new seed database. See [Creating a New Seed Database](http://wiki.adempiere.net/Creating_a_New_Seed_Database) for more details.

Once all the scripts are applied, you can start the application server and test the upgrade.

