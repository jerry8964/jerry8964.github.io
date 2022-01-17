```
layout: post
title: "SQL-ServerのSp_help***"
date:   2022-01-17
tags: [sql-server, database]
comments: true
author: Jerry8964
```



# SQL-SERVER Database Engine



## Sp_help***



[**official document**](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-help-transact-sql?view=sql-server-ver15)

### sp_help

Reports information about a database object (any object listed in the **sys.sysobjects** compatibility view), a user-defined data type, or a data type.



### sp_helpdb

Reports information about a specified database or all databases.



### sp_helpdevice

Reports information about Microsoft® SQL Server™ backup devices.



### sp_helpextendedproc

Reports the currently defined extended stored procedures and the name of the dynamic-link library (DLL) to which the procedure (function) belongs.



### sp_helpfile

Returns the physical names and attributes of files associated with the current database. Use this stored procedure to determine the names of files to attach to or detach from the server.



### sp_helpfilegroup

Returns the names and attributes of filegroups associated with the current database.



### sp_helpindex

Reports information about the indexes on a table or view.



### sp_helplanguage

Reports information about a particular alternative language or about all languages in SQL Server 2019 (15.x).



### sp_helpserver

Reports information about a particular remote or replication server, or about all servers of both types. Provides the server name, the network name of the server, the replication status of the server, the identification number of the server, and the collation name. Also provides time-out values for connecting to, or queries against, linked servers.



### sp_helpsort

Displays the sort order and character set for the instance of SQL Server.



### sp_helpstats

Returns statistics information about columns and indexes on the specified table.



### sp_helptext

Displays the definition of a user-defined rule, default, unencrypted Transact-SQL stored procedure, user-defined Transact-SQL function, trigger, computed column, CHECK constraint, view, or system object such as a system stored procedure.



### sp_helptrigger

Returns the type or types of DML triggers defined on the specified table for the current database. sp_helptrigger cannot be used with DDL triggers. Query the [system stored procedures](https://docs.microsoft.com/en-us/sql/relational-databases/system-catalog-views/sys-triggers-transact-sql?view=sql-server-ver15) catalog view instead.



### sp_helpconstraint

Returns a list of all constraint types, their user-defined or system-supplied name, the columns on which they have been defined, and the expression that defines the constraint (for DEFAULT and CHECK constraints only).



### others database engine procedure

[**official documents**](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql?view=sql-server-ver15)

[sp_executesql](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-add-data-file-recover-suspect-db-transact-sql?view=sql-server-ver15) 　[日本語](https://docs.microsoft.com/ja-jp/sql/relational-databases/system-stored-procedures/sp-executesql-transact-sql?view=sql-server-ver15)   

[sp_lock](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql?view=sql-server-ver15)    [日本語](https://docs.microsoft.com/ja-jp/sql/relational-databases/system-stored-procedures/sp-lock-transact-sql?view=sql-server-ver15)

[sp_recompile](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-recompile-transact-sql?view=sql-server-ver15)    [日本語](https://docs.microsoft.com/ja-jp/sql/relational-databases/system-stored-procedures/sp-recompile-transact-sql?view=sql-server-ver15)

[sp_refreshview](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-refreshview-transact-sql?view=sql-server-ver15)    [日本語](https://docs.microsoft.com/ja-jp/sql/relational-databases/system-stored-procedures/sp-refreshview-transact-sql?view=sql-server-ver15)

[sp_rename](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql?view=sql-server-ver15)    [日本語](https://docs.microsoft.com/ja-jp/sql/relational-databases/system-stored-procedures/sp-rename-transact-sql?view=sql-server-ver15)

[sp_set_session_context](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-set-session-context-transact-sql?view=sql-server-ver15)   [日本語](https://docs.microsoft.com/ja-jp/sql/relational-databases/system-stored-procedures/sp-set-session-context-transact-sql?view=sql-server-ver15)

[sp_spaceused](https://docs.microsoft.com/en-us/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=sql-server-ver15)     [日本語](https://docs.microsoft.com/ja-jp/sql/relational-databases/system-stored-procedures/sp-spaceused-transact-sql?view=sql-server-ver15)





---end----



