# SQL Basics Recap


SQL Server is Microsoft's relational database management system. Primarily used to store and retrieve dat aused by other applications. lots of versions available. Generally have Developer, Express, Web, Standard and Enterprise editions. 2017 edition added a big change in enabling SQL Server to run on Linux

## 1 - Database Fundamentals

Three main types of database: Hierarchical (directory structure), Flat-File (CSV, Excel, Delimited), Relational. SQL is a relational database management system so that is what will be dealt with here. Relational is based on relational model; similar data is presented in tables that have a relationship with other tables.

Tables are akin to a singular excel sheet. The table contains columns, representing a particular type of data (e.g. a name), and rows (representing all the pieces of data for an item,, such as a customer's name, address and date of birth).

## Data Manipulation Language (DML)

The computer language used to interact with data. The actions are typically in the name. SQL has ```SELECT```, ```INSERT```, ```UPDATE```,```DELETE```,```MERGE```, and ```BULK INSERT```. Select retrieves rows and enables selection of one or many rows or columns. INSERT adds one or more rows to a table or view. Update changes existing data in a table. Delete removes one or more rows. Merge Performs insert, update or deletes on a target table based on the results of a join with a source table. Bulk insert imports a data file into a database table or view. There are others, such as WRITETEXT, READTEXT,UPDATETEXT, CREATE, ALTER, DROP, ENABLE TRIGGER, DISABLE TRIGGER, RENAME, UPDATE STATISTICS. Triggers are interesting as they can be used to respond to a different DML command. UPDATE STATISTICS updates the query optimisation statistics. Also nifty is the USE statement whihc changes the database context, and the TRUNCATE command, which removes all rows from a table without logging, making is very efficient for quickly clearing a table.

## Data Types

"An attribute that specifies the type of data na object can hold"

In SQL, these are specified at the time of creation and help SQL engine determine data type of results, and collation precendence. Types include:

 - Exact Numerics
 - Approximate Numerics
 - Unicode Character Strings
 - Binary Strings

Exact Numerics include tinyint, smallint, int, bigint, smallmoney, money. Always use the smallest data type for purpose. These are used in context where (surprise) accuracy is absolutely crucial , such as financial data. Foir example, money and smallmoney are accurate to a tenthousandth of the smallest denomination (e.g. cents)

Approximate Numerics represent real numbers, but do not represent them as exact numbers in the DB. Examples include float and real.

Unicode is used for an extended character set. Includes nchar, nvarchar, ntext.

Binary is used to store binary representations of data. the binary is simply a series of bytes, whith lenght of 1 to 8k. size is n bytes. image type is used for storing binary block data, originating in compressed images. 0 to 2^31 bytes size. varbinary is length of data +2 bytes.

Other data types include Data and time (datetime), character Strings, and others.

Date and time can be stored as date, datetime(date with a time attached), datetime2 (more precise datetime), datetimeoffset (datetime with timezone awareness), smalldatetime (datetime without seconds or fractional seconds), and finally time (time of day, no time zone awareness).

Character Strings have char (fixed length string data), varchar (variable-length string data), text (variable length, non-unicode data).

Others include cursor (variables or stored procude output parameters, containing a reference to a cursor. used when data needs ot be updated row by row). rowversion (exposes automaticall generated unique binary numbers within a DB that are used for version stamping table rows). hierarchyid represents position in a tree hierarchy. uniqueidentifyer is a 6-byte GUID (globally unique identifier). sql_variant stores values of various sql-supported data types. xml allows xml data to be stores. There are also spacial geometry and geography types. table type can be used for temporary store of a set of rows returned as the result set of a table-valued function.

During the demos, notice the use of ```GO``` ,which is used by some editors in a similar way to ```;``` as a way of sending the statements to be run.

### Tables

Contains data in a database in a row and column format. Can have up to 1024 columns (30k using SPARSE).

### View

This is a virtual table that is defined by a query. Can also be viewed as a filter on a table, although they can reference several tables at once.

### Stored Procedures

"A group of one or more statements or a reference to a .NET framework CLR method"

These can accept input parameters and return multiple values as output paramenter. This allows programmers to store operations within the database. This helps to reduce network traffic, allows the combination of multiple calls, is mroe secure (as it limits the ability to run unauthorised commands remotely0, and is reusable. They often offer improved performance as they allow modular programming.

### Functions

Similar to functions in other programming languages. Routines that accept parameters, perform an action and return the result. Again, allows a modular approach, generally allows faster execution and reduces network traffic. There are some system functiosn built in that can be used to improve performance.

## Manipulating Data

In order to manipulate data for select statements or to update data in a table, need to add commands. When selecting, the SELECT command retrieves rows, FROM specifies table, view, derived tables used in statements. GROUP BY divides the query result into a group of rows, usually when aggregating. HAVING is normally used as a search condition for a gorup or an aggregate. ORDER BY allows the ordering of results. UNION combines the results of two or mroe queries into a single set. EXCEPT returns distinct rows from one input query. INTERSECT returns common output results from two queries. JOIN defines the way two tables are related in a query.

UPDATE changes existing data in a table or view. They always acquires a lock on the modified row or rows. It is very important to specifiy exactly which records to update to avoid accidentally rewriting data

The DELETE statement removes existing records form a table. TRUNCATE removes all rows from a table or specified partitions of a table. INSERT allows insertion of new records into a table.

## Data Storage

### Normalisation

A database design technique which origanises tables in a manner ot make a database mroe efficient. Resolves issues of data redundancy and improves storage efficiency. 

#### Forms of normalisa1iton

First Normal Form. All entries in a column should be of the same data types and there should be no duplicate columns or multi-valued attributes. Second Normal Form already in 1NF, all partial dependencies remove to other tables. An example of this would be to take a course name out of a list of courses and put it (alongside it's associated ID) into a separate table. third normal form (3nf): already in 2nf, then eliminate non-dependent columns and transient dependencies. 3NF is most common form. An example of this would be to remove instructor details (such as their name and phone number) from the main table, replacing them with an instructorID attribute that links to a table containg the instructors' details. 4NF is £NF with no independent multiple relationships. 5NF goes further by also isolating "semantically related relationships".

 
### Primary Keys

Unique identifier for each record in a table. CANNOT BE NULL AND MUST BE UNIQUE. can only have one primary key per table. can be made up of one or several fields as long as it is unique. 

### Foreign Keys

Can be used to reference columns of a unique constraint in another table, for example, an instructor id might be linked to a table of courses offered, as well as a table of instructor details.

### Composite Keys

A key containing multiple columns. Can be designated as primary key if the combination of the columns uniquely identifies a row.


## Administering a Database

### Users & Authentication

2 supported methods via SQL server. Windows authentication (aka Integrated Security) where Windows user groups are given permission to log in. The other option is "mixed mode" where windows AND a separate SQL server authentication. Windows authentication is more convenient as it allows a single log on and groups can be easily controlled in an organisation. SQL logins allow mixed-OS access and separate the login details from the ones required to access windows

### Roles
Sysadmin - superuser, SA account is mapped to this. Unlimited access. SA account is a known default and often the target of attacks, meaning many organisations now disable this account after setup. Other than that there are 3 types of logins/users

- Windows logins, or trusted domain accounts. SQL server relies on windows to authenticate user accounts. Commonly used for one-off low level access.
- SQL logins, where sql server is storing login data internally to verify login attempts. Used for instances that are not part of a domain or where windows logins cannot be used
- WIndows group logins. This grants access to a particular group of users, where an organisation is using windows access domain. Simple to administer and easy to add users as needed by an administratior

#### Special Users

- DBO or database owner. Sysadmin is mapped to this. Permissions to perform all actions in database. not to be confused with DB_owner roles
- Guest, for logins without a mapping. By default, users cannot access the database with guest accounts. Advisable to keep disabled.

### Database permissions
SQL server securables have associated permissions that can be granted. GRANT is a positive privilege, whereas DENY overwrites GRANT and blocks access. REVOKE negates a grant or deny. Permissions include ones such as ALTER, CONNECT, BACKUP, CONTROL (gives ownership-like capabilities), CREATE, DELETE, DROP, EXECUTE, INSERT, TAKE OWNERSHIP, SLECT, UPDATE, VIEW DEFINITION. There are hundreds of permissions available, and it is a good idea to only grant the minimum needed to a particular user group to avoid security issues.

#### Objects and Permissions

Instance level locks down Endpoints; these are the point of entry into SQL server. Can listen natively to requests. 
Database level locks down Assemblies and Services - object that references a managed application model. Cotnains class metadata and managed code. Uploading an assembly to an instance is first step in creation of various objects.
Schema level locks down Tables, Views, Procedures, Queues- More granular
Column-level; to specify this, list the columns that access is granted to for a particular app or user.

#### Database Roles

- db_owner: Perform all configuration and maintenance, including ability to drop database. Give out only when needed
- db_securityadmin: Modify role membership and manage permissions
- db_accessadmin: Add or remove access to the database for Windows logins or groups, and SQl server logins
- db_backupoperator: Can back up any database
- db_ddladmin: can run any DDL command on the database
- db_datawriter: Can add, delete, or change dat ain all user tables
- db_datareader: Can read all data from all user tables
- db_denydatawriter: Add so that user cannot add, modify or delete any data
- db_ denydatareader: as above but for reading

There's also the public role, which is equivalent to the "everyone" group in Windows. It is also possible to create custom roles if needed.


## Maintenance

A SQL server instance has several means of support

- Statistics: SQL Server optimiser that analyses a number of candidate execution plans, estiamtes cost and selkects lowest cost option. This optimises execution of queries. Statistics should be updated regularly to keep optimiser having most recent information. If using out-of-date statistics, the query optimiser's plan choice may be suboptimal, resulting in higher CPU usage and slower times. Can auto-update statistcs, which typically updates after a certain amount of rows is changed.
- Indexes: On-disk structure that speeds retrieval from a table or view. Stored in keytree, and allows faster findign of keys. Needs regular maintenance as well. fragmentation occurs as data is inerted, updated, and deleted. This can negatively impact performance. Can counter this by reoganising, disable-and-organise. Can set up Database maintenance plans or custom scripts in an SQL agent job. Alternativel,y third party tools are available.
- Consistency Checks: These check for changes due to, for example, disk corruption and ensure any edits are due to user action and not accidental. Corruption can happen, usually due to an i/o subsystem issue (in the disk storage layer). Running DBCC CHECKDB will find corruption but may take some time. Alternatives are DBBC CHECKALLOC, DBCC CHECKCATALOG, DBCC CHECFILEGROUP, and DBCC CHECKTABLE. should implement a scheduled job to run dbcc checkdb to prevent data loss and recover from a backup if necessary.



## Backup and Disaster Recovery

Several types
- Full backup: Backs up the hwol databse, icnluding part of the transaction log.
- Differential Backup: Stores the changes from a previous full backlog. full backup this is based on is known as base of the differential
- Log backup: Backs up the transaction log. Helps protect data and prevents log from filling up, as it truncates the log
- Filegroup backup: specify filegroups. used for larger database
- file backup: individual file backup, used mostly when several files are created for database
- COPY_ONLY: SQL Server backup that is independent of other backups. Does nto affect SQL server state such as logs, or differential bitmaps.

### Tail-log backup

Captures any log record that have nto yet been backed up to prevent data loss and keep log chain intact.

### Recovering Transactions

Usually starts with tail-log backup. Restore last known-good full backup with NORECOVERY. Restore most recent differential, then transaction logs, both with NORECOVERY. If able to takea tail-log backup, restore this. Finally RESTORE dbname WITHRECOVERY.

Need to plan ahead, and know how to recover. Testing that backups are good regularly both ensures they are available and practices the recovery process. Having a disaster recovery plan may be prudent, for example if a data center is lost. Knwoing how long a restore takes is also important, as it allows the informing of customers or stakeholders how long they will have to wait.