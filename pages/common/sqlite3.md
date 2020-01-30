# sqlite3

> The command-line interface to SQLite 3, which is a self-contained file-based embedded SQL engine.
> More information: <https://sqlite.org>.

- Start an interactive shell with a new database:

`sqlite3`

- Open an interactive shell against an existing database:

`sqlite3 {{path/to/database.sqlite3}}`

- Execute an SQL statement against a database and then exit:

`sqlite3 {{path/to/database.sqlite3}} '{{SELECT * FROM some_table;}}'`

- Execute file and log output to file

`sqlite3 -column -header {{path/to/database.sqlite3}} < {{path/to/script.sql}} > {{path/to/file.log}}`

- Script to import CSV

````
-- https://www.sqlite.org/pragma.html
-- https://www.tutorialspoint.com/sqlite/sqlite_pragma.htm
-- https://stackoverflow.com/questions/2182774/can-sqlite-load-10m-data-into-the-memory
-- https://www.whoishostingthis.com/compare/sqlite/optimize/

--  BEGIN TRANSACTION; Decrease performance

-- Prints PRAGMAS
PRAGMA journal_mode; 
PRAGMA page_size;
PRAGMA synchronous;

PRAGMA journal_mode=OFF;
PRAGMA page_size=32768;
PRAGMA synchronous=0; -- Does nothing for performance in this case

-- Prints PRAGMAS again
PRAGMA journal_mode;
PRAGMA page_size;
PRAGMA synchronous;

CREATE TABLE IF NOT EXISTS TEMP_TABLE (
	DATABASE TEXT,
	CPR TEXT,
  	STARTTID TEXT,
  	SLUTTID TEXT,
  	FORLOEB_ID TEXT,
	UDTRAEK_ID TEXT,
  	AFSENDERSYSTEM TEXT,
  	FOEDESYSTEM TEXT,
  	SKSKODE TEXT,
  	TS_SUPSYS TEXT
);

.mode csv
.import csv1.del TEMP_TABLE
.import csv2.del TEMP_TABLE
.import csv3.del TEMP_TABLE
.import csv4.del TEMP_TABLE
.mode list

-- COMMIT; Decrease performance

-- With this setting
/*
+-------------+---------+------------+
|    Rows     | seconds |  rows/sec  |
+-------------+---------+------------+
|   4.151.966 |      39 | 106.460,67 |
| 143.893.264 |     878 | 163.887,54 |
+-------------+---------+------------+
*/
````