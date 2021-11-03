# SQL Server Fundamentals

SQL Server is an implementation of a relational database, highly scalable, and accessible by several users at once. Has a wide range of features, and collections of services, applications of libraries.

## Applications

These are things such as SSMS (SQL SERVER MANAGEMENT STUDIO), which provides a GUI to work on SQL databases. Databases can also be worked on via a command line interface, such as sqlcmd or powershell. Other useful apps are SQL server profiler (makes a trace of all commands being sent to SQL Server), and Database Engine Tuning Advisor (which optimises the performance of SQL server).

#### SSMS

This is one of the more common tools for working with SQL server. WEnt through this in previous SQL Basics course as well. Can use Object Explorer to look through everythign that SSMS is managing. First have to connect to an instance of SQL server. Once connected, the object explorer models the connected objects in a tree-like structure similar to a normal file system. can delete databases with a simple right click -> delete procedure. to add a database, simply right click -> new database. These can also be done via the command line. Initially, a simple recovery module is a good diea, until the database is entering the production environment.

## T-SQl

This is short for Transact SQL, and is the language used for programming SQL. Metadata that defines what is in the database has to be defined in the database itself. This is stored in INFORMATION_SCHEMA. There are richer, proprietary schemas for storing the database metadata. Documentation can be gotten via "BOL" (Books OnLine), and contains indepth documentation for all SQL Server products.

### Metadata

This defines what is in SQL Server. Every database contains views of all the metadata that make it up. This include,s for example, the logins to the database. For details on where to find metadata, it is best ot use the books online.
