# Data Query Language
**DQL statements are used for performing queries on the data within schema objects**. The purpose of the DQL Command is to get some schema relation based on the query passed to it. We can define DQL as follows it is a component of SQL statement that allows getting data from the database and imposing order upon it. **It includes the SELECT statement**. This command allows getting the data out of the database to perform operations with it. When a SELECT is fired against a table or tables the result is compiled into a further temporary table, which is displayed or perhaps received by the program i.e. a front-end.

## SELECT
Select is the most commonly used statement in SQL. The SELECT Statement in SQL is used to retrieve or fetch data from a database. We can fetch either the entire table or according to some specified rules. The data returned is stored in a result table. This result table is also called result-set.

With the SELECT clause of a SELECT command statement, we specify the columns that we want to be displayed in the query result and, optionally, which column headings we prefer to see above the result table.

The select clause is the first clause and is one of the last clauses of the select statement that the database server evaluates. The reason for this is that before we can determine what to include in the final result set, we need to know all of the possible columns that could be included in the final result set.

``` sql
-- This query will return all the rows in the table with fields column1 , column2:
SELECT column1, column2 
FROM table_name 

-- column1 , column2: names of the fields of the table
-- table_name: from where we want to fetch

-- To fetch the entire table or all the fields in the table:
SELECT * FROM Student;

-- Query to fetch the fields ROLL_NO, NAME, AGE from the table Student:
SELECT ROLL_NO, NAME, AGE FROM Student;
```

## How does select work?
Let's say we have these tables:

![image](https://user-images.githubusercontent.com/53339016/150652099-bdd9ba60-2d6b-4281-b348-c268c25e4b89.png)

And this query:
```sql
SELECT R.Name
FROM Researchers R, AuthorContribution A
WHERE R.RID = A.RID AND A.PID = 307
```

The first step is to calculate the cross product of tables Researchers and AuthorContribution:

![image](https://user-images.githubusercontent.com/53339016/150652132-0377c808-a0c4-46e9-a947-588eb169afca.png)

RID appears in both Researchers and AuthorContribution => it must be qualified (e.g., in the WHERE clause). So, we remove the rows in the cross product that don't satisfy the condition:
* **R.RID = A.RID** (red means it satisfies the condition)
![image](https://user-images.githubusercontent.com/53339016/150652199-a9b17298-e5fa-4660-b3cc-102dbcb5c7fd.png)
* A.PID = 307 (purple means it satisfies the condition)
![image](https://user-images.githubusercontent.com/53339016/150652218-60a3f77e-6818-4000-bf1c-177a870f480e.png)
* We end up with this table :
![image](https://user-images.githubusercontent.com/53339016/150652235-00c04242-dae8-4fdc-b5c6-353206a4fef3.png)
* Then we remove the column that don't appear in the SELECT (so we only select R.Name)
![image](https://user-images.githubusercontent.com/53339016/150652257-adc2412c-24ae-4f6e-9f78-492c656c281c.png)
