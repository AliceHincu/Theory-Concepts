# Data Manipulation Language
The SQL commands that deals with the manipulation of data present in the database belong to DML or Data Manipulation Language and this includes most of the SQL statements.

Basically: subset of SQL used to pose queries, to add / update / remove data

## INSERT
The INSERT INTO statement of SQL is used to insert a new row in a table. 

There are two ways of using INSERT INTO statement for inserting rows:
* **Only values**: First method is to specify only the value of data to be inserted without the column names.
```sql
INSERT INTO table_name VALUES (value1, value2, value3,…);
-- table_name: name of the table.
-- value1, value2,.. : value of first column, second column,… for the new record
```
* **Column names and values both**: In the second method we will specify both the columns which we want to fill and their corresponding values as shown below:
```sql
INSERT INTO table_name (column1, column2, column3,..) 
VALUES ( value1, value2, value3,..);
-- table_name: name of the table.
-- column1: name of first column, second column …
-- value1, value2, value3 : value of first column, second column,… for the new record
```

**We can use the SELECT statement with INSERT INTO** statement to copy rows from one table and insert them into another table.The use of this statement is similar to that of INSERT INTO statement. The difference is that the SELECT statement is used here to select data from a different table. The different ways of using INSERT INTO SELECT statement are shown below:

```sql
INSERT INTO first_table SELECT * FROM second_table;
-- first_table: name of first table.
-- second_table: name of second table.

INSERT INTO first_table(names_of_columns1) SELECT names_of_columns2 FROM second_table;
-- first_table: name of first table.
-- second_table: name of second table.
-- names of columns1: name of columns separated by comma(,) for table 1.
-- names of columns2: name of columns separated by comma(,) for table 2.
```

## UPDATE
The UPDATE statement in SQL is used to update the data of an existing table in database. We can update single columns as well as multiple columns using UPDATE statement as per our requirement.

```sql
UPDATE table_name SET column1 = value1, column2 = value2,... 
WHERE condition;
```

The command changes the records in the table that satisfy the condition in the WHERE clause; if the WHERE clause is omitted, all the records in the table are changed; the values of the columns specified in SET are changed to the associated expressions' values

## DELETE
The DELETE Statement in SQL is used to delete existing records from a table. We can delete a single record or multiple records depending on the condition we specify in the WHERE clause.

```sql
DELETE FROM table_name WHERE some_condition;
-- table_name: name of the table
-- some_condition: condition to choose particular record.
```

We can delete single as well as multiple records depending on the condition we provide in WHERE clause. If we omit the WHERE clause then all of the records will be deleted and the table will be empty.

