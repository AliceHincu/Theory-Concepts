* [Lecture 12 exercises](#from-l12)
* [Written 1 exercises](#w1)
* [Written 2 exercises](#w2)


# From L12
### 1
In a SELECT query: <br>
**! a !**. the SELECT clause can contain arithmetic expressions <br>
b. according to the conceptual evaluation strategy, ORDER BY is evaluated before GROUP BY <br>
c. HAVING can contain row-level qualification conditions <br>
**! d !**. DISTINCT eliminates duplicates from the answer set <br>
e. none of the above is correct. <br>

### 1-EXPLANATION
b. We have: FROM, WHERE, GROUP BY, HAVING, SELECT, ORDER BY <br>
c. it specifies group-level qualification conditions, it doesn't do row. For row-level it's WHERE. <br>

### 2
The natural join operator R1 * R2 in the relational algebra: <br>
a. returns a relation whose schema contains only the attributes in R1 that don't appear in R2 <br>
**! b !**. returns a relation whose schema contains all the attributes in R1 and R2, with common attributes appearing only once <br>
c. returns 2 relation instances <br>
d. is not associative <br>
e. none of the above is correct. <br>

### 2-EXPLANATION
c. It returns a single relation instance

### 3
In the ANSI-SPARC architecture (for a database system), a database can have: <br>
a. exactly one symbolic structure <br>
b. several conceptual structures <br>
**! c 1**. several external structures <br>
d. several physical structures <br>
e. none of the above is correct. <br>

### 3-EXPLANATION
a. There is no symbolic structure in ANSI-SPARC <br>
b. Conceptual structure describes the structures, the data structures and the restrictions in your databases(like the schema), so you have a single **collection of data**(=instance of the schema) in a database, so no several structures. <br>
c. We can have multiple views for example


### 4
4. Consider relation S[A, B, C, D, E, F, G, H] with:
* primary key {A, B, C}, no other candidate keys;
* functional dependencies that are known to hold over S: {F} → {H}, {C} → {E, G};
* no repeating attributes.
a. S is not 1NF <br>
b. S is 2NF <br>
**! c !**. S is not BCNF <br>
d. S is 3NF <br>
e. none of the above answers is correct.

### 4-EXPLANATION 
a. it is in 1NF because it doesn't have any repeating attributes. <br>
b. It is not 2NF because it has a dependency: {C} -> {E, G}

### 5
5. In a B-tree of order 8:
**! a !**. a non-terminal node has at most 8 subtrees <br>
**! b !**. a non-terminal node with 7 values has 8 subtrees <br>
c. terminal nodes can be on different levels
d. a non-terminal node with 7 values has 6 subtrees <br>
e. none of the above answers is correct.

### 5-EXPLANATION 
Every non-terminal node has at most m subtrees and m/2 subtrees and m-1 values.

### 6
6. Let 𝛼, 𝛽 and 𝛾 be subsets of attributes in a relational schema. If 𝛼 → 𝛽 and 𝛽 → 𝛾, then by transitivity:
**! a !**. 𝛼 → 𝛾 <br>
b. 𝛾 → 𝛼 <br>
c. 𝛽 → 𝛼 <br>
d. 𝛾 → 𝛽 <br>
e. none of the above answers is correct.

### 7
Let RepairLog[RID, MechanicID, RollerCoasterID, RepairTime] be a table in a SQL Server database. RepairLog has 100.000 records and 2 indexes: a unique clustered index on RID and a non-clustered index on MechanicID without nonkey columns.

Consider the following query:
```sql
SELECT RID, MechanicID, RepairTime
FROM RepairLog
WHERE MechanicID = 7
```
If the execution plan contains an Index Seek (NonClustered), it also contains a: <br>
a. Clustered Index Scan <br>
b. Index Scan (NonClustered) <br>
**! c !**. Key Lookup (Clustered) <br>
d. Index Trick (NonClustered) <br>
e. none of the above answers is correct. <br>

### 7-EXPLANATION
The Index Seek (NonClustered) is used because we make a search on MechanicID, and the SELECT clause contains also RepairTime which is not includeed in the NonClustered Index, so for this the SQL server performs a key look up in order to retrieve the value of RepairTime maching MechanicID = 7.

RID is used as a row locator in the NonClustered Index, and this RID value is taken and  basically a Clustered Index operation is carried out which is called a key lookup.

Btw: you need to make MechanicID unique to work. And if you add RepairTime to the as a nonkey column, then you don't do a key look up anymore

### 8-10
Consider the relational schema S[FK1, FK2, A, B, C, D, E], with primary key {FK1, FK2}. Answer questions 8-10 using the legal instance below:

![image](https://user-images.githubusercontent.com/53339016/150860554-db54f13d-e11a-4d8e-9c75-7edf71277483.png)

### 8
Consider queries Q1 and Q2:
```sql
-- Q1:
SELECT *
FROM S s1 LEFT JOIN S s2 ON s1.FK1 = s2.E
-- Q2:
SELECT DISTINCT *
FROM S s1 INNER JOIN S s2 ON s1.FK1 = s2.E
```

8. The cardinality of the answer set of Qi is denoted by |Qi|. |Q1| - |Q2| is:
a. 0 <br>
b. 3 <br>
c. 10 <br>
d. 2 <br>
e. none of the above answers is correct.

### 8-EXPLANATION
For Q1: you have the concatenation of s1.FK1=2(2 rows) and s2.E=2(3 rows), which meand we will have 6 rows that respect the condition. For s1.FK1=1(3rows), we don't have any match, so we put them with null. It means 9 rows, so cardinality 9

For Q2: same thing about the concatenation, so 6 rows.

Q2-Q1=3.

### 9
9. Regarding the functional dependencies of S:
**! a !**. at least one of the following dependencies is not satisfied by the instance: {A} → {B}, {FK1, FK2} → {A, B}, {FK1} → {A} <br>
b. by examining the instance, we can conclude that at least one of the following dependencies is specified on the schema S: {A} → {B}, {FK1} → {A, B}, {FK1} → {A} <br>
c. at least two of the following dependencies are not satisfied by the instance: {FK2} → {A, B}, {A} → {E}, {A, B} → {E}, {FK1, FK2} → {E} <br>
d. by examining the instance, we can conclude that at least two of the following dependencies are specified on the schema S: {FK2} → {A, B}, {A} → {E}, {A, B} → {E}, {B} → {C, E} <br>
e. none of the above answers is correct.

### 9-EXPLANATION
a. {A} -> {B} is satisfied because we have 2 rows where a3 -> b3, and {FK1, FK2} → {A, B} hold because it is a primary key, but the last one doesn't hold. <br>
b. Just by looking at the instance, you can never draw conclusions about the specification of certain integrity constraints(dependencies included) on the relational schema. <br>
c. Everything except {FK2} → {A, B} is satisfied  <br>
d. same as b

### 10
Consider queries Q1 and Q2:
```sql
-- Q1:
SELECT FK2, FK1, COUNT(DISTINCT B)
FROM S
GROUP BY FK2, FK1
HAVING FK1 = 0

-- Q2:
SELECT FK2, FK1, COUNT(C)
FROM S
GROUP BY FK2, FK1
HAVING MAX(E) < 0
```

The cardinality of the answer set of Qi is denoted by |Qi|.
10. |Q1| - |Q2| is:
**! a !**. 0 <br>
b. 2 <br>
c. 1 <br>
d. -1 <br>
e. none of the above answers is correct

### 10-EXPLANATION
|Q1| = |Q2| = 0

### 11
11. A secondary index:
**! a !**. can contain duplicates <br>
b. cannot contain duplicates <br>
**! c !**. can be non-clustered <br>
d. cannot be non-clustered <br>
e. none of the above answers is correct <br>

### 11-EXPLANATION
**A secondary index** = it's the one whose search key does not include the primary key. 

**Duplicates** = data entries with the same value for the search key.

### 12
![image](https://user-images.githubusercontent.com/53339016/150865742-b59b1245-463b-46ac-afdf-d6759449be74.png)

12. For the relation R[A, B, C] below, consider the 3 possible projections on 2 attributes: AB[A, B], BC[B, C], AC[A, C]. How many extra records does AB * BC * AC contain (i.e., records that don’t appear in R)?
a. 0 <br>
**! b !**. 1 <br>
c. 2 <br>
d. 3 <br>
e. none of the above answers is correct.

### 12-EXPLANATION
|AB|BC| AB * BC |AC| (AB * BC) * AC |
|--|--|--|--|--|
|<table> <tr><th>A</th><th>B</th></tr><tr><td>a1</td><td>b2</td></tr><tr><td>a1</td><td>b1</td></tr><tr><td>a2</td><td>b1</td></tr> </table>| <table> <tr><th>B</th><th>C</th></tr><tr><td>b2</td><td>c1</td></tr><tr><td>b1</td><td>c2</td></tr><tr><td>b1</td><td>c1</td></tr> </table>| <table> <tr><th>A</th><th>B</th><th>C</th></tr><tr><td>a1</td><td>b2</td><td>c1</td></tr> <tr><td>a1</td><td>b1</td><td>c2</td></tr> <tr><td>a1</td><td>b1</td><td>c1</td></tr> <tr><td>a2</td><td>b1</td><td>c2</td></tr> <tr><td>a2</td><td>b1</td><td>c1</td></tr></table>|  <table> <tr><th>A</th><th>C</th></tr><tr><td>a1</td><td>c1</td></tr><tr><td>a1</td><td>c2</td></tr><tr><td>a2</td><td>c1</td></tr> </table>| <table> <tr><th>A</th><th>B</th><th>C</th></tr><tr><td>a1</td><td>b2</td><td>c1</td></tr> <tr><td>a1</td><td>b1</td><td>c2</td></tr> <tr><td>a1</td><td>b1</td><td>c1</td></tr> <tr><td>a2</td><td>b1</td><td>c1</td></tr> </table>|

One extra row => b

### 13
13. The cross-product operator R1 × R2 in the relational algebra:
**! a !**. returns a relation whose schema contains all the attributes in R1 followed by all the attributes in R2 <br>
b. returns a relation whose schema contains only the attributes in R1 <br>
c. returns 3 relation instances <br>
**! d !**. is associative <br>
e. none of the above answers is correct.

### 14
1. Rewrite the CREATE TABLE statements below such that the following restriction is enforced: one T1 entity can be associated with any number of T2 entities, and one T2 entity can be associated with at most one T1 entity. Don't add other SQL statements.
```sql
CREATE TABLE T1
   ( IDT1 INT PRIMARY KEY,
     C1 VARCHAR(100)
   )
CREATE TABLE T2
   ( IDT2 INT PRIMARY KEY,
     C2 DATE
   )
```

### 14-SOLUTION
```sql
CREATE TABLE T1
   ( IDT1 INT PRIMARY KEY,
     C1 VARCHAR(100)
   )
CREATE TABLE T2
   ( IDT2 INT PRIMARY KEY,
     C2 DATE,
     IDT1 INT REFERENCES T1(IDT1)
   )
```
If it said one T2 entity can be associated with EXACTLY one T1 entity, you just add NOT NULL

### 15
2. Write the relational algebra expression below as a SQL query:
𝜋_{𝐴,𝐵,𝐶}((𝜋_{𝐴,𝐵,𝐼𝐷}(𝜎𝑀=70(𝑅))) ⊗_{𝐼𝐷=𝐼𝐷𝑇1} (𝜋_{𝐶,𝐼𝐷𝑇1}(𝜎_{𝑁>5}(𝑆))))

### 15-SOLUTION
```sql
SELECT A, B, C -- if we operated on sets we needed to add DISTINCT
FROM (
    (SELECT A,B,ID
     FROM R
     WHERE M=70) t1
    INNER JOIN
    (SELECT C,IDT1
     FROM S
     WHERE N>5) t2
    ON t1.ID = t2.IDT1
   )
```

### 16-19
Consider the relational schema R[RID, A, B, C, D, E, F], with primary key {RID}. Answer questions 3-6 using the legal instance below:

![image](https://user-images.githubusercontent.com/53339016/150873071-409c9e81-55b0-42da-851f-09df04850302.png)

### 16
3. What's the result set returned by the following query? Write the tuples' values and the names of the columns.
```sql
SELECT r1.RID, r1.A + r2.A C2, r1.A * r2.A C3
FROM R r1 LEFT JOIN R r2 ON r1.RID = r2.RID
WHERE r1.A > ANY (SELECT B WHERE C < 10)
FROM R
```

### 16-SOLUTION
Left join result: the table concatenated with itself.
```
(SELECT B WHERE C < 10)
```
The query will select the rows 1,3,4,5 and B=(100,200). r1.A > ANY(100,200) meanr r1.A>100. So, for the final table we have:

| RID | C2 | C3 |
| -- | -- | -- |
| 2 | 202 | 10201 |
| 4 | 400 | 40000 |
| 5 | 400 | 40000 |
| 6 | 600 | 90000 |

### 17
4. Evaluate the expressions below. 𝜋 doesn't eliminate duplicates. What's the cardinality of 𝑇?

𝑆 ≔ 𝜎_{𝐹<13}(𝑅) <br>
𝑇 ≔ 𝜋_{𝑆.𝑅𝐼𝐷,𝑆.𝐴}(𝑆 ⊗_{𝑆.𝐷=𝑅.𝐷} 𝑅)

### 17-SOLUTION 
This is S(i only took the rid and D just to simplify):

| RID | D |
| -- | -- |
| 1 | 200 |
| 2 | 200 |
| 5 | 200 |
| 6 | 200 |


After we do the condition join, because every value of D is the same everywhere, we will have 4rows(from S) * 6rows(from T) = 24rows. " 𝜋 doesn't eliminate duplicates", so the answer is 24. If pi eliminated duplicates, we would only have 4.

### 18
5. What's the result set returned by the following query? Write the tuples' values and the names of the columns.
```sql
SELECT R.*
FROM
  (SELECT r1.RID, r2.A, r3.B
   FROM R r1 INNER JOIN R r2 ON r1.A = r2.B
             INNER JOIN R r3 ON r2.B > r3.D
    WHERE r1.F > 10) t
RIGHT JOIN R ON t.RID = R.RID
```

### 18 - SOLUTION
When we reach INNER JOIN R r3 ON r2.B > r3.D, there is no B > 200, so we have 0 rows.

t is empty. We right join it with R. => **it's the original table R.**

### 19
6. Write all functional dependencies F such that:
* F is satisfied by the current instance of R;
* the dependent of F is {D};
* the determinant of F has a single column.

### 19 - SOLUTION
Because D has the same values everywhere, {every column} -> {D}

### 20
7. Rewrite the expression below using only operators in the set {𝜎, 𝜋, ×, ∪, −}.

(𝑅 ⊗_{𝑅.𝐼𝐷=𝑆.𝑅𝐼𝐷} 𝑆) ∩ (𝑇 ⊗_{𝑇.𝐼𝐷=𝑈.𝑇𝐼𝐷} 𝑈)

### 20 - SOLUTION
![image](https://user-images.githubusercontent.com/53339016/150881202-4d63627c-e559-44ed-8d83-8c9bf7c0ac35.png)

### 21
8. Let P, Q, R be 3 relations with schemas P[PID, P1, P2, P3], Q[QID, Q1, Q2, Q3,Q4, Q5], R[RID, R1, R2, R3], and E an expression in the relational algebra: 
 
E = π_{P2, Q2, Q4, R3}(𝜎_{PID = Q1 AND QID = R2 AND P3='Bilbo' AND Q5 = 100 AND R1=7} (P×Q×R))

Optimize E and draw the evaluation tree for the optimized version of the expression.

### 21 - SOLUTION

To be continued...

# W1
### Part I. 
1. Define the 3rd normal form.

A relation is in 3NF if it's in 2NF and there are no non-prime attributes that functionally tranzitive dependent on any key.

2. Briefly describe a ternary relationship set in the Entity-Relationship model using an example.

A ternary relationship is a relationship type that **involves many to many relationships between three tables.** The University might need to record which teachers taught which subjects in which courses.

### Part III
1-5. Consider the relational schema S[ID, A, B, C, D, E, F] with the key {ID}. Answer questions 1-5 using the legal instance below:

| ID | A | B | C | D | E | F |
| -- | -- | -- | -- | -- | -- | -- |
| t1 | a1 | b2 | Şi abia plecă bătrânul... Ce mai freamăt, ce mai zbucium! | 0 | 1 | 0 |
| t2 | a1 | b2 | Codrul clocoti de zgomot şi de arme şi de bucium, | 1 | 2 | 1 |
| t3 | a1 | b3 | Iar la poala lui cea verde mii de capete pletoase, | 0 | 3 | 0 | 
| t4 | a1 | b3 | Mii de coifuri lucitoare ies din umbra-ntunecoasă; | 2 | 123 | -1 |
| t5 | a1 | b3 |Călăreţii umplu câmpul şi roiesc după un semn | -1 | 4 | -1 |

1. When executed on the above instance S:
a. query ```SELECT DISTINCT A, B FROM S``` returns 2 tuples. <br>
b. query ```SELECT * FROM S WHERE B = 'b2' AND B = 'b3'``` returns 0 tuples. <br>
c. query ```SELECT * FROM S WHERE B = 'b3' UNION SELECT * FROM S WHERE B = 'b3'``` returns 1 tuple. <br>
d. query ```SELECT * FROM S WHERE D >= 0 EXCEPT SELECT * FROM S WHERE E <> 4``` returns 0 tuples. <br>
e. none of the above answers is correct.

**ANSWER**: a,b,d

**EXPLANATION**: a) returns <a1,b2> and <a1,b3> ... b) retur 0 because you can't habe B equal to both b2 and b3 ... c) Union eliminates duplicates, but you will still have 3 rows(t3 t4 t5) ... d) is true because that "except select" will include all rows.

2. Consider projections S1[ID, A, B, C, F] and S2[D, E, F]. The result of the natural join S1 * S2 contains (column order is not important):
a. only the 5 tuples in S <br>
b. 7 tuples, out of which 5 are the original tuples in S <br>
c. no tuples <br>
d. 9 tuples, out of which 5 are the original tuples in S <br>
e. none of the above answers is correct. <br>

**ANSWER**: d

**EXPLANATION**: <t1, t1>, <t1, t3>, <t2, t2>, <t3, t1>, <t3, t3>, <t4, t4>, <t4, t5>, <t5, t4>, <t5, t5>. There are 5 tuples like <tx,tx> and 9 in total.

3. How many records does the query below return?
```sql
SELECT B, C, COUNT(*)
FROM S
GROUP BY B, C
HAVING D <= 1
```
a. 5  <br>
b. 4  <br>
c. 3  <br>
d. 2  <br>
e. none of the above answers is correct.

**ANSWER**: e

**EXPLANATION**: "Column 'T1.D' is invalid in the HAVING clause because it is not contained in either an aggregate function or the GROUP BY clause."

4. How many records does the query below return?
```sql
SELECT *
FROM S
WHERE C LIKE 'de%'
```

a. 3 <br>
b. 0 <br>
c. 5 <br>
d. 1 <br>
e. none of the above answers is correct.

**ANSWER**: b

**EXPLANATION**: There isn't any column that starts with "de"

5. Regarding the functional dependencies of S:
a. at least one of the following dependencies is not satisfied by the instance: {ID, A} → {D, E}, {B} → {A}, {A, B} → {D} <br>
b. by examining the instance, we can conclude that at least one of the following dependencies is specified on the schema S: {A} → {D, E}, {B} → {A}, {A, B} → {D} <br>
c. at least two of the following dependencies are not satisfied by the instance: {C} → {A}, {A} → {C}, {E} → {B}, {F} → {A} <br>
d. by examining the instance, we can conclude that at least two of the following dependencies are specified on the schema S: {C} → {A}, {A} → {C}, {E} → {B}, {F} → {A} <br>
e. none of the above answers is correct.

**ANSWER**: a

**EXPLANATION**: a) {A, B} → {D} is not satisfied (<a1, b3>) ... b) and d) are never true, because with an instance  we can't conclude the schema. c) only {a}->{c) is false.

6. A data description model can be used to describe:
a. the structure of the data <br>
b. IF statements <br>
c. the relationships with other data <br>
d. the consistency constraints <br>
e. none of the above answers is correct. <br>

**ANSWER**: a, c, d.

**EXPLANATION**: data description model: set of concepts and rules used to model data; such concepts describe: the structure of the data, consistency constraints, relationships with other data

7. In a DBMS, the buffer manager:
a. manages disk space <br>
b. brings pages from the disk into main memory <br>
c. monitors lock requests <br>
d. produces an efficient execution plan for query evaluation <br>
e. none of the above answers is correct. 

**ANSWER**: b

**EXPLANATION**: disk space manager is at a). lock manager ar c) .. d) optimizer.

8. A SELECT statement:
a. can contain a HAVING clause only if it contains a WHERE clause <br>
b. can contain a WHERE clause only if it contains a HAVING clause <br>
c. can contain a HAVING clause only if it contains an ORDER BY clause <br>
d. can contain a GROUP BY clause only if it contains a HAVING clause <br>
e. none of the above answers is correct.

**ANSWER**: e

**EXPLANATION**: Be aware!! You can have "having" without "group by" (ex: ```SELECT SUM(D) FROM T1 HAVING SUM(D) <= 3```), because it operates on the table as a group

9. Let R[ID1, ID2, ID3, A, B, C, D, E, F, G] be a relational schema with no repeating attributes. The keys of R are {ID1, ID2, ID3} and {A, B}. The following dependencies hold: {ID1, ID2} → {C} and {A} → {G}. R is:
a. 1NF <br>
b. 2NF <br>
c. 3NF <br>
d. BCNF <br>
e. none of the above answers is correct.

**ANSWER**: a

**EXPLANATION**: "no repeating attributes" means 1NF.   {ID1, ID2, ID3} is a key , but  {ID1, ID2} → {C} and {ID1, ID2} it's a subset. So no 2NF.

10. On a magnetic disk, disk access time includes:
a. lunch time <br>
b. seek time <br>
c. rotational delay <br>
d. transfer time <br>
e. none of the above answers is correct.

**ANSWER**: b, c, d

**EXPLANATION**: "no repeating attributes" means 1NF.   {ID1, ID2, ID3} is a key , but  {ID1, ID2} → {C} and {ID1, ID2} it's a subset. So no 2NF.

12. The projection operator π in the relational algebra:
a. is a binary operator
b. is a unary operator
c. is a ternary operator
d. is distributive with respect to set-difference
e. none of the above answers is correct.

**ANSWER**: b

**EXPLANATION**: it is applied on a single relation => unary

### Part IV. 
Let A, B, C, D be 4 relations with schemas A[ID, A1, A2, A3], B[B1, B2], C[C1, C2], D[ID, D1], and E an expression in the relational algebra:

E = (σID = B1 AND A2='exam' AND B2='DB'(A×B)) * (σC1=3 (C×D)) 

![image](https://user-images.githubusercontent.com/53339016/150988252-bc7bce59-aa02-496a-9e74-5bb3ee6c177b.png)

Optimize E and draw the evaluation tree for the optimized version of the expression.

**EXPLANATION**: First, we apply selections on a single table. Then, we apply projections to reduce the nr of columns on all the condition cols (but here it's not the case)

# W2
1. Rows in a relation in the relational model:
a. are not ordered <br> 
b. are not distinct <br> 
c. are ordered <br>
d. are distinct <br>
e. none of the above answers is correct.

**ANSWER**: a, d. 

**EXPLANATION**: See lecture 12.

2-6. Consider the relational schema R[RID, M, N, P, Q, O] with the primary key {RID}, and NOT NULL constraints on columns M and N. R has no other restrictions. Answer questions 2-6 using the legal instance below:

| RID | M | N | P | Q | O |
| -- | -- | -- | -- | -- | -- |
| 10 | Allons | Le jour | 20 | 1 | 10 |
| 1 | enfants | de | 21 | 1 | 5 |
| 2 | de gloire | 22 | 1 | null |
| 11 | la est | 23 | 1 | null |
| 3 | Patrie, | arrivé! | 24 | 1 | 2 |

2. How many records does the query below return when executed on a legal instance of R?
```sql
SELECT *
FROM R
WHERE M IS NULL
```
a. 1 <br>
b. 2 <br>
c. 0 <br>
d. 3 <br>
e. none of the above answers is correct.

**ANSWER**: c

**EXPLANATION**: M is null nowhere

3. After executing the statement:
```sql 
DROP TABLE R
```
a. both the schema information and the tuples of the table are still stored in the database <br>
b. only the tuples are removed from the table, the schema information is still stored in the database <br>
c. both the schema information and the tuples of the table are removed from the database <br>
d. only the schema information is removed, the tuples are still stored in the table <br>
e. none of the above answers is correct.

**ANSWER**: c

4. How many records does the query below return?
```sql
SELECT M, COUNT(DISTINCT P)
FROM R
```
a. 1 <br>
b. 5 <br>
c. 4 <br>
d. 2 <br>
e. none of the above answers is correct.

**ANSWER**: e

**EXPLANATION**: "Column 'R.M' is invalid in the select list because it is not contained in either an aggregate function or the GROUP BY clause."

5. How many records does the query below return?
```sql
SELECT *
FROM R
WHERE P > ALL (SELECT P FROM R)
```

a. 0 <br>
b. 5 <br>
c. 1 <br>
d. 4 <br>
e. none of the above answers is correct.

**ANSWER**: a

**EXPLANATION**: If you do >ALL(SELECT...) you take the max value from the select. In this case, max value of P. In the Where clause, you search for a P > P_max, which will always return false.

6. How many records does the query below return?
```sql
SELECT AVG(P)
FROM R
GROUP BY Q
HAVING AVG(P) < 10
```

a. 0 <br>
b. 5 <br>
c. 2 <br>
d. 1 <br>
e. none of the above answers is correct.


**ANSWER**: a

**EXPLANATION**: Group by Q, where Q=1 everywhere mean we take the whole table as a group. The AVG(P) is 22 which is not <10, so we get 0 rows.

7. For the relation S[A, B, C] below, consider the 3 possible projections on 2 attributes: AB[A, B], BC[B, C], and AC[A, C]. How many extra records does AB * BC * AC contain (i.e., records that don’t appear in S)?

| A | B | C |
| -- | -- | -- |
| A1 | B1 | C1 |
| A1 | B1 | C2 |
| A2 | B2 | C1 |

a. 0 <br>
b. 1 <br>
c. 3 <br>
d. 2 <br>
e. none of the above answers is correct.


**ANSWER**: a

**EXPLANATION**: 

|AB|BC| AB * BC |AC| (AB * BC) * AC |
|--|--|--|--|--|
|<table> <tr><th>A</th><th>B</th></tr><tr> <td>A1</td><td>B1</td></tr> <tr><td>A2</td><td>B2</td></tr> </table>| <table> <tr><th>B</th><th>C</th></tr> <tr><td>B1</td><td>C1</td></tr> <tr><td>B1</td><td>C2</td></tr> <tr><td>B2</td><td>C1</td></tr> </table>| <table> <tr><th>A</th><th>B</th><th>C</th></tr> <tr><td>A1</td><td>B1</td><td>C1</td></tr> <tr><td>A1</td><td>B1</td><td>C2</td></tr> <tr><td>A2</td><td>B2</td><td>C1</td></tr> </table>|  <table> <tr><th>A</th><th>C</th></tr> <tr><td>A1</td><td>C1</td></tr> <tr><td>A1</td><td>C2</td></tr> <tr><td>A2</td><td>C1</td></tr> </table>| <table> <tr><th>A</th><th>B</th><th>C</th></tr> <tr><td>A1</td><td>B1</td><td>C1</td></tr> <tr><td>A1</td><td>B1</td><td>C2</td></tr> <tr><td>A2</td><td>B2</td><td>C1</td></tr> </table>|

9. Of the algorithms below, which one is the best to evaluate a search of the form C = C0, where C is a key?
a. table scan <br>
b. index scan <br>
c. index seek <br>
d. cross join <br>
e. hash join

**ANSWER**: c

**EXPLANATION**: 
Index Seek:
* searching for a key value K0
* condition of the form: K = K0

10. When mapping an m:n association to tables, if an association class exists, its attributes:
a. are added to the table that lies on the m side of the association
b. are added to the table that lies on the n side of the association
c. are added to the link table
d. are not added to any table
e. none of the above answers is correct.

**ANSWER**: c

**EXPLANATION**: Link table = the relation between them = the "verb"

11. Consider the relation R[A, B, C, D, E] with:
- the keys {A, E}, {A, B, C}, {A, B, D};
- the functional dependency {A, C} → {D};
- no repeating attributes.

a. R is 1NF
b. R is 2NF
c. R is 3NF
d. R is BCNF
e. none of the above answers is correct.


**ANSWER**: a,b,c

**EXPLANATION**: no repeating attributes => 1NF. We have the key {A,B,C}, and we can see that {A,C} is a subset of the key and {A, C} → {D}, but D is also a prime attribute => 2NF. The are no non-prime attributes that are tranzitively dependent on the keys, so it's also 3NF. BCNF: Every determinant is a key, but {A, C} is not a key, it's a subset, so it's not BCNF.

12. In a DBMS, the buffer manager:
a. automatically drops clustered indexes
b. manages available disk space
c. when necessary, chooses a page in the buffer pool for replacement, based on a replacement policy
d. maintains the number of current users for every page in the buffer pool
e. none of the above answers is correct.


**ANSWER**: c, d

### PART IV
IV. Let A, B, and C be 3 relations with schemas A[AID, A1, A2, A3], B[BID, B1, B2, B3], C[CID, C1, C2, C3], and E an expression in the relational algebra:

E = σA.AID = B.B1 AND B.BID=C.C2 AND C.C3=5 (Π{A.AID, A.A1, A.A2, B.BID, B.B1, C.C2, C.C3}(A×B×C))

Optimize E and draw the evaluation tree for the optimized version of the expression.

**ANSWER**:
![image](https://user-images.githubusercontent.com/53339016/151014504-72d97417-0c5a-4287-87bb-4fc05dc07a68.png)

How to solve:

you go backwords. you start with the 3 rectangles, A,B,C. You do the selection first and then the projection because:
* sigma reduces the nr of rows
* pi reduces the number of columns, and you need to retain attriibutes that will be required later.

Then just do the joins.
