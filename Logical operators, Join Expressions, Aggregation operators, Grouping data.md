# Contents
* [Logical operators](#logical-operators) - ALL, AND, ANY, BETWEEN, EXISTS, IN, LIKE, NOT, OR
* [Union, Intersect, and Except Operators](#union,-intersect,-and-except-operators) - UNION, INTERSECT, EXCEPT
* [Join Expressions](#join-expressions) - INNER JOIN, LEFT JOIN, RIGHT JOIN, FULL OUTER JOIN
# Logical operators
| Operator | Description | 
| -- | -- |
| ALL | TRUE if all of the subquery values meet the condition	|
| AND	| TRUE if all the conditions separated by AND is TRUE |	
| ANY	| TRUE if any of the subquery values meet the condition	|
| BETWEEN	| TRUE if the operand is within the range of comparisons |
| EXISTS | TRUE if the subquery returns one or more records	|
| IN | TRUE if the operand is equal to one of a list of expressions |	
| LIKE | TRUE if the operand matches a pattern |
| NOT	| Displays a record if the condition(s) is NOT TRUE |	
| OR | TRUE if any of the conditions separated by OR is TRUE |	

## ALL
Condition	Meaning
* **c > ALL(…)** : The values in column c must greater than the biggest value in the set to evaluate to true.
* **c >= ALL(…)**: The values in column c must greater than or equal to the biggest value in the set to evaluate to true.
* **c < ALL(…)** : The values in column c must be less than the lowest value in the set to evaluate to true.
* **c >= ALL(…)**: The values in column c must be less than or equal to the lowest value in the set to evaluate to true.
* **c <> ALL(…)**: The values in column c must not be equal to any value in the set to evaluate to true.
* **c = ALL(…)** : The values in column c must be equal to any value in the set to evaluate to true.

For example, the following statement finds all employees whose salaries are greater than the highest salary of employees in the Marketing department whose id is 2:
```sql

SELECT first_name, last_name, salary
FROM Employees
WHERE salary > ALL 
      (SELECT salary
       FROM employees
       WHERE department_id = 2)
ORDER BY salary;
```

## AND
The AND operator allows you to construct multiple conditions in the WHERE clause of an SQL statement such as SELECT, UPDATE, and DELETE:

The following example finds all employees whose salaries are greater than 5,000 and less than 7,000:
```sql
SELECT first_name, last_name, salary
FROM Employees
WHERE salary > 5000 AND salary < 7000
ORDER BY salary;
```

## ANY
Condition	Meaning
* **x = ANY (…)**	: The values in column c must match one or more values in the set to evaluate to true.
* **x != ANY (…)**: The values in column c must not match one or more values in the set to evaluate to true.
* **x > ANY (…)** : The values in column c must be greater than the smallest value in the set to evaluate to true.
* **x < ANY (…)**	: The values in column c must be smaller than the biggest value in the set to evaluate to true.
* **x >= ANY (…)**: The values in column c must be greater than or equal to the smallest value in the set to evaluate to true.
* **x <= ANY (…)**: The values in column c must be smaller than or equal to the biggest value in the set to evaluate to true.

For example, the following statement finds all employees whose salaries are greater than the lowest salary of employees in the Marketing department whose id is 2:
```sql
SELECT first_name, last_name, salary
FROM Employees
WHERE salary > ANY 
      (SELECT salary
       FROM employees
       WHERE department_id = 2)
ORDER BY salary;
```

## BETWEEN 
The BETWEEN operator is one of the logical operators in SQL. The BETWEEN operator checks if a value is within a range of values.

The following statement uses the BETWEEN operator to find all employees whose salaries are between 2,500 and 2,900:
```sql
SELECT employee_id, first_name, last_name, salary
FROM Employees
WHERE salary BETWEEN 2500 AND 2900
ORDER BY salary DESC;
```

## EXISTS
Find the names of students who are not graded in Alg1.
```sql
SELECT S.sname
FROM Students S
WHERE NOT EXISTS
    (SELECT *
     FROM Exams E
     WHERE E.sid = S.sid AND E.cid = 'Alg1')
```

## IN
The IN operator - it tests whether a value belongs to a set of elements

```sql
SELECT R.Name
FROM Researchers R
WHERE R.RID IN
    (SELECT A.RID 
     FROM AuthorContribution A
     WHERE A.PID = 300)
```

## Like
The LIKE operator returns true if a value matches a pattern or false otherwise.

The SQL standard provides you with two wildcard characters to make a pattern:
* % **percent** wildcard matches zero, one, or more characters
* _ **underscore** wildcard matches a single character.

The following example uses the LIKE operator to find all employees whose first names start with Da :
```sql
SELECT employee_id, first_name, last_name
FROM Employees
WHERE first_name LIKE 'Da%';
```

To match a string that contains a wildcard for example 10%, you need to instruct the LIKE operator to treat the % in 10% as a regular character.

To do that, you need to explicitly specify an escape character after the ESCAPE clause:
```sql
value LIKE '%10!%%' ESCAPE '!'
```
In this example, the ! is an escape character. It instructs the LIKE operator to treat the % in the 10% as a regular character.

## NOT
To negate the result of any Boolean expression, you use the NOT operator

Example to get the employees who work in the department id 5 and with a salary not greater than 5000.
```sql
SELECT employee_id, first_name, last_name, salary
FROM Employees
WHERE department_id = 5
AND NOT salary > 5000
ORDER BY salary;
```

## OR
The SQL OR is a logical operator that combines two boolean expressions. The SQL OR operator returns either true or false depending on the results of expressions.

```sql
SELECT first_name, last_name, hire_date, department_id
FROM Employees
WHERE YEAR(hire_date) = 1997 OR YEAR(hire_date) = 1998
```

# Union, Intersect, and Except Operators
![image](https://user-images.githubusercontent.com/53339016/150655587-51891366-86d2-42b3-9c9d-a9f868066072.png)
### Union
Find the ids of students who are older than 20 or have a grade in the Alg1 course:
```sql
SELECT S.sid FROM Students S WHERE S.age > 20
UNION
SELECT E.sid FROM Exams E WHERE E.cid = 'Alg1'
--UNION ALL doesn't eliminate duplicates
```

### Intersect 
Find the ids of students who received a grade in both a 4 credits course and a 5 credits course:
```sql
SELECT E.sid FROM Exams E, Courses C WHERE E.cid = C.cid AND C.credits = 4
INTERSECT
SELECT E2.sid FROM Exams E2, Courses C2 WHERE E2.cid = C2.cid AND C2.credits = 5
```

### Except
Find the ids of students who received a grade in a 4 credits course, but have no grades in 5 credits courses.
```sql
SELECT E.sid FROM Exams E, Courses C WHERE E.cid = C.cid AND C.credits = 4
EXCEPT
SELECT E2.sid FROM Exams E2, Courses C2 WHERE E2.cid = C2.cid AND C2.credits = 5
```

# Join Expressions
Let's say we have these tables: 
![image](https://user-images.githubusercontent.com/53339016/150656396-dd9b6128-f2a8-416a-96ad-96999485c7d7.png)

## Inner join
![image](https://user-images.githubusercontent.com/53339016/150655721-c04ba225-423e-4af9-a7e3-c4c791a722ae.png)
For each row in table A, the inner join clause finds the matching rows in table B. If a row is matched, it is included in the final result set.

```sql
source1 [alias] [INNER] JOIN source2 [alias] ON condition
```

**Example**: find all the students' grades; include the students' names in the answer set
```sql
SELECT *
FROM Students S INNER JOIN Exams E ON S.SID = E.StdId
```
Result:

![image](https://user-images.githubusercontent.com/53339016/150655802-78320ac1-f67d-46c3-91e9-fdb28be3dccd.png)

## Left join
![image](https://user-images.githubusercontent.com/53339016/150655911-9f5867ff-26fb-4d22-87de-d0cc638b31c1.png)

```sql
source1 [alias] LEFT [OUTER] JOIN source2 [alias] ON condition
```

**Example**: find all the students' grades; include students with no exams; the students' names must appear in the answer set
```sql
SELECT *
FROM Students S LEFT JOIN Exams E ON S.SID = E.StdId
```
Result:
![image](https://user-images.githubusercontent.com/53339016/150656426-1f10f00e-a344-4c7a-83b7-af1432842aca.png)

## Right join
```sql
source1 [alias] RIGHT [OUTER] JOIN source2 [alias] ON condition
```

**Example**: find all the exams (including the names of the courses); include courses with no exams
```sql
SELECT *
FROM Exams E RIGHT JOIN Courses C ON E.CrsId = C.CID
```
Result:
![image](https://user-images.githubusercontent.com/53339016/150656355-cddec43a-9e81-4dad-84d6-4e5e4dc2dfbd.png)


## Full outer join
![image](https://user-images.githubusercontent.com/53339016/150656372-291cabfe-21a3-4454-8de6-3bad5d855148.png)

```sql
source1 [alias] FULL [OUTER] JOIN source2 [alias] ON condition
```

**Example**: find all the exams; include students with no exams and grades given by mistake to nonexistent students; the result should also contain students' names
```sql
SELECT *
FROM Students S FULL JOIN Exams E ON S.SID = E.StdId
```
Result:
![image](https://user-images.githubusercontent.com/53339016/150656350-26f35118-3ba3-4b51-b20d-516c68ca3692.png)


# Aggregation operators
* **AVG** – calculate the average value of a set.
* **COUNT** – return the number of items in a set.
* **SUM** – return the sum of all or distinct items of a set.
* **MAX** – find the maximum value in a set.
* **MIN** – find the minimum value in a set.

```sql
-- Find the number of students.
SELECT COUNT(*)
FROM Students S

-- Find the average and minimum age for group 924.
SELECT AVG(S.age), MIN(S.age)
FROM Students S
WHERE S.sgroup = 924

-- Find the number of groups that have at least one student called Mihai.
SELECT COUNT(DISTINCT S.sgroup)
FROM Students S
WHERE S.sname = 'Mihai'

-- Find the name and age of the oldest student.
SELECT S.sname, S.age
FROM Students S
WHERE S.age = ANY
      (SELECT MAX(S2.age)
       FROM Students S2)
```
# Grouping Data
## Group by
The GROUP BY clause is an optional clause of the SELECT statement that combines rows into groups based on matching values in specified columns. One row is returned for each group.

You often use the GROUP BY in conjunction with an aggregate function such as MIN, MAX, AVG, SUM, or COUNT to calculate a measure that provides the information for each group.

It is important to emphasize that the **WHERE clause is applied before rows are grouped whereas the HAVING clause is applied after rows are grouped**. In other words, the WHERE clause is applied to rows whereas the HAVING clause is applied to groups.

To sort the groups, you add the ORDER BY clause after the GROUP BY clause.

**Example**: To find the headcount of each department, you group the employees by the department_id column, and apply the COUNT function to each group as the following query:
```sql
SELECT department_id, COUNT(employee_id) headcount
FROM employees
GROUP BY department_id;
```

![image](https://user-images.githubusercontent.com/53339016/150656755-2794842a-9b47-40e5-a93f-c43c02f131e1.png)

## Having
To specify a condition for groups, you use the HAVING clause.

### HAVING vs. WHERE
The WHERE clause applies the condition to individual rows before the rows are summarized into groups by the GROUP BY clause. However, the HAVING clause applies the condition to the groups after the rows are grouped into groups.

Therefore, it is important to note that the HAVING clause is applied after whereas the WHERE clause is applied before the GROUP BY clause.

**Example1**: To find the managers who have at least five direct reports, you add a HAVING clause to the query above as the following:
```sql
SELECT manager_id, first_name, last_name, COUNT(employee_id) direct_reports
FROM employees
WHERE manager_id IS NOT NULL
GROUP BY manager_id
HAVING direct_reports >= 5;
```

**Example2**: SQL HAVING with SUM function example
The following statement calculates the sum of salary that the company pays for each department and selects only the departments with the sum of salary between 20000 and 30000.
```sql
SELECT  department_id, SUM(salary)
FROM employees
GROUP BY department_id
HAVING SUM(salary) BETWEEN 20000 AND 30000
ORDER BY SUM(salary);
```

**READ THIS!!!!(The answer)**
[Why can't you mix Aggregate values and Non-Aggregate values in a single SELECT?](https://stackoverflow.com/questions/5920070/why-cant-you-mix-aggregate-values-and-non-aggregate-values-in-a-single-select)

Aggregates doesn't work on a complete result, they only work on a group in a result.

Consider a table containing:
```
Person   Pet
-------- --------
Amy      Cat
Amy      Dog
Amy      Canary
Dave     Dog
Susan    Snake
Susan    Spider
```
If you use a query that groups on Person, it will divide the data into these groups:
```
Amy:
  Amy    Cat
  Amy    Dog
  Amy    Canary
Dave:
  Dave   Dog
Susan:
  Susan  Snake
  Susan  Spider
```
If you use an aggreage, for exmple the count aggregate, it will produce one result for each group:
```
Amy:
  Amy    Cat
  Amy    Dog
  Amy    Canary    count(*) = 3
Dave:
  Dave   Dog       count(*) = 1
Susan:
  Susan  Snake
  Susan  Spider    count(*) = 2
```
So, the query ```select Person, count(*) from People group by Person``` gives you one record for each group:
```
Amy    3
Dave   1
Susan  2
```
If you try to get the Pet field in the result also, that doesn't work because there may be multiple values for that field in each group.

(Some databases, like MySQL, does allow that anyway, and just returns any random value from within the group, and it's your responsibility to know if the result is sensible or not.)

If you use an aggregate, but doesn't specify any grouping, the query will still be grouped, and the entire result is a single group. So the query ```select count(*) from Person``` will create a single group containing all records, and the aggregate can count the records in that group. The result contains one row from each group, and as there is only one group, there will be one row in the result.
