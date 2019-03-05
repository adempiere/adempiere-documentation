---
description: Hints and tips to maintain the database.
---

# Database Maintenance

## Database Tuning

Databases need regular maintenance to function well. If you do not have a database administrator who can look at this for you, consider contracting one at regular intervals.

Read the documentation for your database on tuning the database for performance. For example, see [https://community.oracle.com/message/12295510](https://community.oracle.com/message/12295510). There are many tactics you can try such as separating separating index, data and blob table spaces.

### Hardware Considerations

Hardware tuning can get quite technical to ensure the fastest access to data. Seek specific expert advice. Here are a few ideas to look into.

Check the database server for RAM and make sure you have enough RAM to hold the entire database. The system can have lots of page swapping if you don't have enough RAM to hold it all.

Consider using solid state drives as these will also help speedup the database access. Specifically, two solid state drives in RAID 0 config will be much faster than a single drive. However, there is no redundancy and the system will be vulnerable to data corruption. This may be preferable if regular backups to a more secure storage can be performed.

### Trim Unused Data

There are a few things you can look at quickly. In your database, find the commands to list the top twenty tables by size. Some of these may be temporary or logs of process parameters. You can delete the info you no longer need. When you have the data trimmed down, use the database tools to analyse and vacuum the tables. This will also save space.

In ADempiere, the following tables, log tables in particular, can be trimmed or emptied of data:

* Temporary tables that start with "T\_"
* Import tables that start with "I\_"
* Any table called Test
* Tables that start with "AD\_PInstance"
* AD\_Find
* AD\_Error
* AD\_Issue
* AD\_ChangeLog  \(old records\)
* AD\_Session \(old records\)
* AD\_Note \(old notes\)
* Tables that end in Log

These tables can easily take up half of the database space. If you need this data, consider a backup to another database. As routine maintenance, consider setting up housekeeping tasks to scrub old data from these tables.

In the Application, you can limit the amount of data returned by a query if a user opens a window with all records.

Tables with lots of records can be flagged as "High Volume" so users are presented with a search when the window first opens rather than opening all the records.

You can also limit the number of records returned by queries in the Role window to prevent returning too many.

### Add Indexes

ADempiere does not apply indexes on database tables by default. Indexes have a cost in the write operation that offsets the speed gained in some read operations. A index strategy is required to ensure the indexes are effective and don't just add to the overhead. Consider the advice of Craig Mullens in the article [Top 10 Steps to Building Useful Database Indexes](http://www.dbta.com/Columns/DBA-Corner/Top-10-Steps-to-Building-Useful-Database-Indexes-100498.aspx)

> Indexes should be built to optimize the access of your SQL queries. To properly create an optimal set of indexes requires a list of the SQL to be used, an estimate of the frequency that each SQL statement will be executed, and the importance of each query. Only then can the delicate balancing act of creating the right indexes to optimize the right queries most of the time be made.

Here are a few examples:

* Big non-transaction tables

```text
create index with (AD_Org_ID, AD_Client_ID, IsActive)
create index with (UPPER(Value))
create index with (UPPER(Name))
```

* Big transaction tables

```text
create index with (AD_Org_ID, AD_Client_ID, DocStatus, Processed, Posted)
```

* Big AD\_ChangeLog

```text
create index for ad_changelog with (ad_table_id, record_id)
```

