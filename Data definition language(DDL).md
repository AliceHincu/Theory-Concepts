# DDL
DDL or Data Definition Language actually **consists of the SQL commands that can be used to define the database schema**. It simply deals with descriptions of the database schema and is used to create and modify the structure of database objects in the database. **DDL is a set of SQL commands used to create, modify, and delete database structures but not data.**

List of DDL commands: 
* **CREATE**: This command is used to create the database or its objects (like table, index, function, views, store procedure, and triggers).
* **DROP**: This command is used to delete objects from the database.
* **ALTER**: This is used to alter the structure of the database.
* **TRUNCATE**: This is used to remove all records from a table, including all spaces allocated for the records are removed.
* **COMMENT**: This is used to add comments to the data dictionary.
* **RENAME**: This is used to rename an object existing in the database.

## CREATE
There are two CREATE statements available in SQL:
1. CREATE DATABASE
2. CREATE TABLE

### CREATE DATABASE
```sql
CREATE DATABASE database_name;
```

* **database_name**: name of the database.

### CREATE TABLE
``` sql
CREATE TABLE table_name (
  column1 data_type(size),
  column2 data_type(size),
  column3 data_type(size),
  ....
);
```

* **table_name**:  name of the table.
* **column1**: name of the first column.
* **data_type**: Type of data we want to store in the particular column. 
* **size**: Size of the data we can store in a particular column. For example if for a column we specify the data_type as int and size as 10 then this column can store an integer number of maximum 10 digits.

**EXAMPLE**:
```sql
CREATE TABLE Students (
  ROLL_NO int(3),
  NAME varchar(20),
  SUBJECT varchar(20),
);
```

## DROP
```sql
DROP object object_name
```

* **object**: can be a table, database, view etc.
* **object_name**: name of object duh.

Examples:
```sql
DROP TABLE table_name;
-- table_name: Name of the table to be deleted.

DROP DATABASE database_name;
-- database_name: Name of the database to be deleted.
```

## ALTER
You can add, change or remove a column.
You can add and remove a constraint.

### ALTER TABLE – ADD
ADD is used to add columns into the existing table, or adding a constraint.

Example for **adding a column**:
```sql
ALTER TABLE table_name
ADD (Columnname_1  datatype,
     Columnname_2  datatype,
              …
     Columnname_n  datatype);
```

Example for **adding a constraint**:
```sql
ALTER TABLE table_name ADD [CONSTRAINT constraint_name] PRIMARY KEY(column_list);
ALTER TABLE table_name ADD [CONSTRAINT constraint_name] UNIQUE(column_list);

ALTER TABLE table_name 
ADD [CONSTRAINT constraint_name] FOREIGN KEY (column_list) REFERENCES table_name[(column_list)] [ON UPDATE action] [ON DELETE action]
```

Practical example:
```sql
-- for column
ALTER TABLE Students ADD FavSymphony VARCHAR(50)

-- for constraint
ALTER TABLE [dbo].[States] WITH CHECK 
ADD CONSTRAINT [FK_States_Countries] FOREIGN KEY([CountryID])
REFERENCES [dbo].[Countries] ([CountryID])
ON UPDATE CASCADE
ON DELETE CASCADE
GO
```
[Delete and update cascade](https://www.sqlshack.com/delete-cascade-and-update-cascade-in-sql-server-foreign-key/)

### ALTER TABLE - DROP
DROP is used to remove a column or a constraint.

Example for dropping a column:
```sql
ALTER TABLE table_name
DROP COLUMN column_name;
```

Example for dropping a constraint:
```sql
DROP [CONSTRAINT] constraint_name
```

### ALTER TABLE - ALTER COLUMN
It is used to modify the existing columns in a table. Multiple columns can also be modified at once.
```sql
ALTER TABLE table_name
ALTER COLUMN column_name column_type;
```
For example, we can change maximum size of the Course Column from X to 20.
```sql
ALTER TABLE Student 
ALTER COLUMN COURSE varchar(20);
```

### ALTER TABLE - RENAME
```sql
-- rename table
ALTER TABLE table_name
RENAME TO new_table_name;

-- rename column
ALTER TABLE table_name
RENAME COLUMN old_name TO new_name;
```
