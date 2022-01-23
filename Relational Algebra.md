## SELECT
**Notation**: 𝜎_{𝐶}(𝑅) 

Resulting relation:
* schema: 𝑅's schema
* tuples: records in 𝑅 that satisfy condition C
* equivalent SELECT statement: ```SELECT * FROM R WHERE C```

### Example
We have this table:

| PID | Name | Ruthlessness | Ship |
| -- | -- | -- | -- |
| p1 | Jack Sparrow | 1 | BP |
| p2 | Elizabeth Swann | 2 | BP |
| p3 | Hector Barbossa | 3 | BP |
| p4 | Will Turner | 1 | FD |
| p5 | Davy Jones | 5 | FD |
| p6 | Blackbeard | 5 | QAR |

If we want to have this query:
```sql
SELECT * FROM Pirates WHERE Ruthlessness < 4
```

We will write using sigma:  ![](https://latex.codecogs.com/svg.image?\sigma_{Ruthlessness&space;<&space;4})(Pirates) and it will produce the first 4 rows.


## PROJECTION
Notation: 𝜋_{𝛼}(𝑅)

Resulting relation:
* schema: attributes in 𝛼
* tuples: every record in 𝑅 is projected on 𝛼
* equivalent SELECT statement
```sql
SELECT DISTINCT 𝛼 FROM R --algebra on sets
SELECT 𝛼 FROM R --algebra on bags
```

If we want to have this query:
```sql
SELECT PID, Name FROM Pirates
```

We will write using pi: ![](https://latex.codecogs.com/svg.image?\pi_{PID,&space;Name}(Pirates)) and it will produce the first 2 columns.

If we want to have this query:
```sql
SELECT PID, Name FROM Pirates
WHERE Ruthlessness < 3
```

We will write like this: ![](https://latex.codecogs.com/svg.image?\pi_{PID,&space;Name}(\sigma_{Ruthlessness<3}(Pirates)) ) 

## Cross-product
Notation: 𝑅1 × 𝑅2

Resulting relation:
* schema: the attributes of 𝑅1 followed by the attributes of 𝑅2
* tuples: every tuple 𝑟1 in 𝑅1 is concatenated with every tuple 𝑟2 in 𝑅2
* equivalent SELECT statement:
```sql
SELECT *
FROM R1 CROSS JOIN R2
```

## Union, Set-difference, Intersection
Notation: 𝑅1 ∪ 𝑅2, 𝑅1 − 𝑅2, 𝑅1 ∩ 𝑅2

𝑅1 and 𝑅2 must be union-compatible:
* **same number of columns**
* corresponding columns, taken in order from left to right, **have the same domains**

Resulting relation:
* schema: defined to be identical to the schema of R1
* tuples: 
   * 𝑅1 ∪ 𝑅2: occur in R1 or in R2(or both)
   * 𝑅1 − 𝑅2: occur in R1 but not in R2
   * 𝑅1 ∩ 𝑅2: occur in R1 and in R2
* equivalent SELECT statements
```sql
-- 𝑅1 ∪ 𝑅2
SELECT * FROM R1
UNION
SELECT * FROM R2

-- 𝑅1 − 𝑅2
SELECT * FROM R1
EXCEPT
SELECT * FROM R2

-- 𝑅1 ∩ 𝑅2
SELECT * FROM R1
INTERSECT
SELECT * FROM R2
-- algebra on bags: SELECT statements that don't eliminate duplicates (e.g., UNION ALL)
```

## Condition join(theta join)
Notation: 𝑅1 ⨂_{Θ} 𝑅2

Resulting relation:
* schema: the attributes of R1 followed by the attributes of R2
* tuples: the records in the cross-product of 𝑅1 and 𝑅2 that satisfy a certain condition Θ
* definition ⇒ 𝑅1 ⨂_{Θ} 𝑅2 = 𝜎_{𝛩}(𝑅1 × 𝑅2)
* equivalent SELECT statement
```sql
SELECT *
FROM R1 INNER JOIN R2 ON Θ
```

### Example
If we have this 2 tables:

|Pirates|Shares|
|--|--|
|<table> <tr><th>PID</th><th>Name</th><th>Ruthlessness</th><th>Ship</th></tr><tr><td>p1</td><td>Jack Sparrow</td><td>1</td><td>BP</td></tr><tr><td>p2</td><td>Elizabeth Swann</td><td>2</td><td>BP</td></tr><tr><td>p3</td><td>Hector Barbossa</td><td>3</td><td>BP</td></tr><tr><td>p4</td><td>Will Turner</td><td>1</td><td>FD</td></tr> </table>| <table> <tr><th>PID</th><th>TID</th><th>Value</th></tr><tr><td>p1</td><td>t1</td><td>100</td></tr><tr><td>p2</td><td>t9</td><td>5000</td></tr><tr><td>p3</td><td>t1</td><td>200</td></tr> </table>|

After condition join (with condition Ruthlessness <= 2 ) we will get the table:
| PID | Name | Ruthlessness | Ship | PID | TID | Value |
| -- | -- | -- | -- | -- | -- | -- |
| p1 | Jack Sparrow | 1 | BP | p1 | t1 | 100 |
| p2 | Elixabeth Swann | 2 | BP | p2 | t9 | 5000 |

## Natural join
Notation: 𝑅1 ∗ 𝑅2

Resulting relation:
* schema: the union of the attributes of the two relations (attributes with the same name in 𝑅1 and 𝑅2 appear once in the result)
* tuples: obtained from tuples <𝑟1, 𝑟2>, where 𝑟1 in 𝑅1, 𝑟2 in 𝑅2, and 𝑟1 and 𝑟2 agree on the common attributes of 𝑅1 and 𝑅2
* let 𝑅1[𝛼], 𝑅2[𝛽], 𝛼 ∩ 𝛽 = 𝐴1, 𝐴2,... , 𝐴𝑚 ; then:
   * 𝑅1 ∗ 𝑅2 = 𝜋_{𝛼⋃𝛽(𝑅1 ⨂_{𝑅1.𝐴1=𝑅2.𝐴1 𝐴𝑁𝐷 … 𝐴𝑁𝐷 𝑅1.𝐴𝑚=𝑅2.𝐴𝑚} 𝑅2)}
   * by 𝛼⋃𝛽 we eliminate duplicates.
* equivalent SELECT statement
```sql
SELECT *
FROM R1 NATURAL JOIN R2
```

### Example
If we have this 2 tables:

|Pirates|Shares|
|--|--|
|<table> <tr><th>PID</th><th>Name</th><th>Ruthlessness</th><th>Ship</th></tr><tr><td>p1</td><td>Jack Sparrow</td><td>1</td><td>BP</td></tr><tr><td>p2</td><td>Elizabeth Swann</td><td>2</td><td>BP</td></tr><tr><td>p3</td><td>Hector Barbossa</td><td>3</td><td>BP</td></tr><tr><td>p4</td><td>Will Turner</td><td>1</td><td>FD</td></tr> </table>| <table> <tr><th>PID</th><th>TID</th><th>Value</th></tr><tr><td>p1</td><td>t1</td><td>100</td></tr><tr><td>p2</td><td>t9</td><td>5000</td></tr><tr><td>p3</td><td>t1</td><td>200</td></tr> </table>|

After natural join we will get the table:
| PID | Name | Ruthlessness | Ship | TID | Value |
| -- | -- | -- | -- | -- | -- |
| p1 | Jack Sparrow | 1 | BP | t1 | 100 |
| p2 | Elixabeth Swann | 2 | BP | t9 | 5000 |
| p3 | Hector Barbossa | 3 | BP | t1 | 200 |

## IDK
![image](https://user-images.githubusercontent.com/53339016/150700250-6b034a93-61d0-4ec1-8e98-736e992f492a.png)

take the ids of cruel pirates that have no shares in tresures from serbia :
![image](https://user-images.githubusercontent.com/53339016/150700356-d643e401-7962-4fc2-88ec-a4c0577598da.png)

## Left outer join
Notation (in these notes): 𝑅1 ⋉_{C} 𝑅2

Resulting relation:
* schema: the attributes of 𝑅1 followed by the attributes of 𝑅2
* tuples: 
   * tuples from the condition join 𝑅1 ⨂_{c} 𝑅2 + 
   * the tuples in 𝑅1 that were not used in 𝑅1 ⨂_{c} 𝑅2 combined with the null value for the attributes of 𝑅2
* equivalent SELECT statement
```sql
SELECT *
FROM R1 LEFT OUTER JOIN R2 ON C
```

## Right outer join
Notation: 𝑅1 ⋊_{C} 𝑅2

Resulting relation:
* schema: the attributes of 𝑅1 followed by the attributes of 𝑅2
* tuples: 
   * tuples from the condition join 𝑅1 ⨂_{c} 𝑅2 + 
   * the tuples in 𝑅2 that were not used in 𝑅1 ⨂_{c} 𝑅2 combined with the null value for the attributes of 𝑅1
* equivalent SELECT statement
```sql
SELECT *
FROM R1 RIGHT OUTER JOIN R2 ON C
```

## Full outer join
Notation: 𝑅1 ⋈_{C} 𝑅2

Resulting relation:
* schema: the attributes of 𝑅1 followed by the attributes of 𝑅2
* tuples:
   * tuples from the condition join 𝑅1 ⨂_{c} 𝑅2 +
   * the tuples in 𝑅1 that were not used in 𝑅1 ⨂_{c} 𝑅2 combined with the null value for the attributes of 𝑅2 +
   * the tuples in 𝑅2 that were not used in 𝑅1 ⨂_{c} 𝑅2 combined with the null value for the attributes of 𝑅1
* equivalent SELECT statement
```sql
SELECT *
FROM R1 FULL OUTER JOIN R2 ON C
```

## Left semi join
Notation: 𝑅1 ⊳ 𝑅2

Resulting relation:
* schema: 𝑅1's schema
* tuples: the tuples in 𝑅1 that are used in the natural join 𝑅1 ∗ 𝑅2

### Example
If we have this 2 tables:

|Pirates|Shares|
|--|--|
|<table> <tr><th>PID</th><th>Name</th><th>Ruthlessness</th><th>Ship</th></tr><tr><td>p1</td><td>Jack Sparrow</td><td>1</td><td>BP</td></tr><tr><td>p2</td><td>Elizabeth Swann</td><td>2</td><td>BP</td></tr><tr><td>p3</td><td>Hector Barbossa</td><td>3</td><td>BP</td></tr><tr><td>p4</td><td>Will Turner</td><td>1</td><td>FD</td></tr> </table>| <table> <tr><th>PID</th><th>TID</th><th>Value</th></tr><tr><td>p1</td><td>t1</td><td>100</td></tr><tr><td>p2</td><td>t9</td><td>5000</td></tr><tr><td>p3</td><td>t1</td><td>200</td></tr> </table>|

After left semi join we will get the table:
| PID | Name | Ruthlessness | Ship |
| -- | -- | -- | -- |
| p1 | Jack Sparrow | 1 | BP |
| p2 | Elixabeth Swann | 2 | BP |

## Right semi join
Notation: 𝑅1 ⊲ 𝑅2

Resulting relation:
* schema: 𝑅2's schema
* tuples: the tuples in 𝑅2 that are used in the natural join 𝑅1 ∗ 𝑅2

## Division
Notation: 𝑅1 ÷ 𝑅2 𝑅1[𝛼], 𝑅2[𝛽], 𝛽 ⊂ 𝛼

Resulting relation:
* schema: 𝛼 − 𝛽
* tuples: a record 𝑟 ∈ 𝑅1÷𝑅2 if ∀ 𝑟2 ∈ 𝑅2, ∃𝑟1 ∈ 𝑅1 such that:
   * 𝜋𝛼−𝛽 𝑟1 = 𝑟
   * 𝜋𝛽 𝑟1 = 𝑟2
   * i.e., a record 𝑟 belongs to the result if in 𝑅1 𝑟 is concatenated with every record in 𝑅2

Basically:

If we have a table like this:
| PID | TID |
| -- | -- |
| p1 | t1 |
| p1 | t2 |
| p1 | t3 |
| p2 | t1 |
| p2 | t2 |
| p3 | t1 |

And 3 tables like this:
|T1|T2|T3|
|--|--|--|
|<table> <tr><th>TID</th></tr><tr><td>t1</td></tr> </table>| <table> <tr><th>TID</th></tr><tr><td>t1</td></tr><tr><td>t2</td></tr> </table>| <table> <tr><th>TID</th></tr><tr><td>t1</td></tr><tr><td>t2</td></tr><tr><td>t3</td></tr> </table> | 

We'll have: 
![image](https://user-images.githubusercontent.com/53339016/150702170-b0ebfda0-fb3d-4b20-8ec6-9be4b8843a6a.png)

## Independent subset of operators
For the previously described query language, with operators: {𝜎, 𝜋, ×, ∪, −, ∩, ⨂, ∗, ⋉, ⋊, ⋈, ⊳, ⊲, ÷} **an independent set of operators is {𝜎, 𝜋, ×, ∪, −}**
