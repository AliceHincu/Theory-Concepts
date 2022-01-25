# Content
* [1NF](#1nf)
* [2NF](#2nf)
* [3NF](#3nf)
* [BCNF](#bcnf)
* [4NF](#4nf)
* [5NF](#5nf)

# What is normalization?
**Normalization** is a database design technique that **reduces data redundancy** and **eliminates undesirable characteristics like Insertion, Update and Deletion Anomalies**. 

What do Insertion, Update and Deletion Anomalies look like? Let's suppose we have this table:
| PID | Name | Reputation | Ship | Salary |
| -- | -- | -- | -- | -- |
| p1 | Jack Sparrow | 5 | BP | 10k |
| p2 | Elizabeth Swan | 6 | BP | 15k |
| p3 | Captain Barbossa | 5 | BP | 10k |
| p4 | Will Turner | 6 | FD | 15k |
| p5 | Davy Jones | 4 | FD | 9k |

### Update Anomaly
Suppose you want to change the salary for a particular reputation. If you only change it in a tuple and not the other ones, we will have an inconsistancy in the database. We have to make sure all the tuples are modified accordigly. (For repuration 5, you need to change both the first and third row)

### Insertion Anomaly
Can we add a salary for a particular reputation value if currently, in the database, there is no pirate with that reputation ? (Let's say for reputation 7 we want 20k salary). There is no pirate, but can we add a row like  "NULL, NULL, 7, NULL, 20K" ? No, because the PK is null. So we cannot do it. To add a new rep, we also need to add a pirate with that rep. It's too restrictive

### Deletion Anomaly
What if we fire Sparrow and Barbossa (both with reputation 5 and salary 10k)? Then we lose the salary for reputation 5. We lose the association between them. 

### How to solve this?
Normalization rules **divides larger tables into smaller tables and links them** using relationships. The purpose of Normalization in SQL is to eliminate redundant (repetitive) data and ensure data is stored logically.

We can eliminate those 3 anomalies by creating 2 tables: One that stores pirates and one that stores the association between reputation and salary:

|Table 1|Table 2|
|--|--|
|<table> <tr><th>PID</th><th>Name</th><th>Reputation</th><th>Ship</th></tr><tr><td>p1</td><td>Jack Sparrow</td><td>5</td><td>BP</td></tr><tr><td>p2</td><td>Elizabeth Swan</td><td>6</td><td>BP</td></tr><tr><td>p3</td><td>Captain Barbossa</td><td>5</td><td>BP</td></tr><tr><td>p4</td><td>Will Turner</td><td>6</td><td>FD</td></tr><tr><td>p5</td><td>Davy Jones</td><td>4</td><td>FD</td></tr> </table>| <table> <tr><th>Reputation</th><th>Salary</th></tr><tr><td>5</td><td>10k</td></tr><tr><td>6</td><td>15k</td></tr><tr><td>4</td><td>9k</td></tr> </table>|

### Decomposition
A relation R is decomposed into relations R1, R2 .. Rm. A **good decomposition** means that we can recover the original relation (in our case R) from the smaller relations. If the decomposition is irreversible, then it's bad. 

![image](https://user-images.githubusercontent.com/53339016/150659712-1bc5decf-b08c-4c04-a9f5-c03faff08048.png)

See more at Lecture 7 (or the readMe for relational algebra if it exists)

Also read about functional dependecy before continuing [here](https://github.com/AliceHincu/Theory-Concepts/blob/main/Functional%20dependency.md)
  
# Database Normal Forms
Here is a **list of Normal Forms** in SQL:
* 1NF (First Normal Form)
* 2NF (Second Normal Form)
* 3NF (Third Normal Form)
* BCNF (Boyce-Codd Normal Form)
* 4NF (Fourth Normal Form)
* 5NF (Fifth Normal Form)
* 6NF (Sixth Normal Form)

## 1NF 
Definition from lecture: **A relation is in the first normal form if it doesn't have any repeating attributes.(which is in accordance with the definition of a relation in the relational model)**

If a relation contains a composite or multi-valued attribute, it violates the first normal form, or **the relation is in first normal form if it does not contain any composite or multi-valued attribute**. A relation is in first normal form if every attribute in that relation is singled valued attribute. 

Rules: 
* **Each table cell should contain a single value.**
* **Each record needs to be unique**.

### Example
Let's say we have this table:

Student(name, birthyear, group, course, grade) with the key "name".

![image](https://user-images.githubusercontent.com/53339016/150660084-f97c8b93-9859-4e08-825c-031377bd2cec.png)

We have a **composite repeating attribute**: the pair {COURSE, GRADE}

### Example2
BOOK(Bid, AuthorsNames, Title, Publisher, PublishingYear, Keyphrases) with the key Bid.

![image](https://user-images.githubusercontent.com/53339016/150660139-65b522f2-6496-4ee6-9dfd-cf64b9d0ff32.png)

We have a **simple repeating attribute**: AuthorsNames, KeyPhrases.

### How to solve this problem
If you have a relation with repeating attribute, the idea would be to decompose it such that the collection the relations contains all the data in the original relation, and the decomposition is good.

**You replace the relation with the repeating attribute by a collection of other relations, via a good decomposition and the repeating attribute is now not repeating anymore.**

### Solution for Example2 
We have 2 separate simple repeating attributes, so we are gonna decompose the book relation into 3 tables: 
* BOOKS[Bid, Title, Publisher, PublishingYear] - so with the attributes that weren't repeating in the original relation
* AUTHORS[Bid, AuthorName] - we took out the first repeating attribute
* KEYPHRASES[Bid, Keyphrase] - we took out the second repeating attribute

![image](https://user-images.githubusercontent.com/53339016/150660330-3768ee5b-3e2a-4033-969a-abbd7f42aefb.png)
![image](https://user-images.githubusercontent.com/53339016/150660334-f39909e0-2901-4a2b-acdf-63ced34f3493.png)

### Solution for Example1
We have a composite repeating attributes, so we are gonna decompose the relation into 2 tables:
* GENERAL_DATA[Name, Birthyear, Group] - with the attributes that were not repeated.
* RESULTS[Name, Course, Grade] - we add the key and the composite repeating attribute.

![image](https://user-images.githubusercontent.com/53339016/150660475-6d894935-df15-43ff-a6f4-a4e06ea61b3b.png)
![image](https://user-images.githubusercontent.com/53339016/150660484-c0e1d934-1a0e-4493-9194-73a77a0eaebe.png)

## 2NF
Before talking about 2NF, take a look at "functional dependency".

Definition from lecture: **A relation is in the second normal form if it's in the first normal form and every non-prime attribute is fully functionally dependent on the key**


**An attribute is prime** if there is a key K in our relation and the attribute is a proper subset of the key. Ex: if our key consists of K1, K2 then K1 is a prime attribute.

Let's say we have a relation R[A1,A2,...,An], where alpha and beta are nonempty sets of attributes in R. Beta is **fully functionally dependent** on alpha if:
* alpha -> beta
* if gamma is any subset of alpha, then gamma -> beta does not hold.
   * Example: we have alpha = [A,B,C] and beta = [D]. Then ABC->D is true, but A->D,B->D,AC->D and so on is not true. 
* **Basically:  Beta is fully functionally dependent on alpha if it's functionally dependent on alpha but it's not functionally dependent on any proper subset of attributes in alpha.**

Let's take an example. We have this table: EXAMS[StudentName, Course, Grade, FacultyMember]

| StudentName | Course | Grade | Faculty Member |
| -- | -- | -- | -- |
| Pop Ioana | Computer Networks | 10 | Matei Ana |
| Vlad Ana | Probabilities and Statistics | 10 | Simion Bogdan |
| Vlad Ana | Computer Networks | 9.98 | Matei Ana |
| Dan Andrei | Probabilities and Statistics | 10 | Simion Bogdan |
| Popescu Alex | Operating Systems | 9.99 | Matei Ana |

The key is {StudentName, Couse}, and as we can oberse, we have this dependency: {Course}->{Faculty Member}. We need to check if it's in the 2NF:
* First rule: to be in 1NF. It doesn't have any repeating attributes, so it's okay.
* Second rule: every non-prime attribute is fully functionally dependent on every key.
   * The prime attributes are StudentName(S), Course(C), and the non-prime attributes are Grade(G), FacultyMember(F).
   * We check for the Grade attribute: is it fully functionally dependent on the key? Fully functionally dependent on the key means:
     * Is grade functionally dependent on StudentName and Course? Yes. SC -> G
     * Is grade not functionally dependent on any subsets of the key? S->G doesn't hold because a student name can't determine a grade, and C -> G doesn't hold because just a course can't determine a grade. So Grade is not functionally dependent on any subsets of the key.
     * So, Grade is functionally dependent on the key, and it is not functionally dependent on any proper subset of the key => **Grade is fully functionally dependent on the key**.
   * We check for the FacultyMember attribute: is it fully functionally dependent on the key? Fully functionally dependent on the key means: 
     * Is F functionally dependent on StudentName and Course? Yes. SC -> F
     * Is F not functionally dependent on any subsets of the key? S->F doesn't hold because a student name can't determine a faculty member, but C->F does hold.
     * So, while FacultyMember is functionally dependent on the key, it is also functionally dependent on a proper subset of the key => **FacultyMember is not fully functionally dependent on the key**.

The second rule isn't respected. We can get rid of this redundancy(due to this functional dependency) by decomposiong our original relation into two relations: RESULTS[**StudentName, Course**, Grade] and COURSES[**Course**, FacultyMember]. From the original relation we'll remove the dependent(FacultyMmember), and the determinant(Course) we'll be the primary key. 

So this table:
| StudentName | Course | Grade | Faculty Member |
| -- | -- | -- | -- |
| Pop Ioana | Computer Networks | 10 | Matei Ana |
| Vlad Ana | Probabilities and Statistics | 10 | Simion Bogdan |
| Vlad Ana | Computer Networks | 9.98 | Matei Ana |
| Dan Andrei | Probabilities and Statistics | 10 | Simion Bogdan |
| Popescu Alex | Operating Systems | 9.99 | Matei Ana |

Becomes these tables:
|RESULTS|COURSES|
|--|--|
|<table> <tr><th>StudentName</th><th>Course</th><th>Grade</th></tr><tr><td>Pop Ioana</td><td>Computer Networks</td><td>10</td></tr><tr><td>Vlad Ana</td><td>Probabilities and Statistics</td><td>10</td></tr><tr><td>Vlad Ana</td><td>Computer Networks</td><td>9.98</td></tr><tr><td>Dan Andrei</td><td>Probabilities and Statistics</td><td>10</td></tr><tr><td>Popescu Alex</td><td>Operating Systems</td><td>9.99</td></tr> </table>| <table> <tr><th>Course</th><th>FacultyMember</th></tr><tr><td>Computer Networks</td><td>Matei Ana</td></tr><tr><td>robabilities and Statistics</td><td>Simion Bogdan</td></tr><tr><td>Operating Systems</td><td>Matei Ana</td></tr> </table>|


## 3NF
Rules:
* **Be in 2NF**
* **no non-prime attribute is transitevely dependent on any key**

A **transitive functional dependency** is when changing a non-key column, might cause any of the other non-key columns to change(in the example below: changing either salary or reputation causes changes in the other column). 

From lecture: **attribute Z is transitively dependent on attribute X if it exists a Y sush that X->Y, Y->Z, Y->X does not hold.**

Example: 

| PID | Name | Reputation | Salary |
| -- | -- | -- | -- |
| p1 | Jack Sparrow | 5 | 10k |
| p2 | Elizabeth Swan | 6 | 15k |
| p3 | Captain Barbossa | 5 | 10k |
| p4 | Will Turner | 6 | 15k |
| p5 | Davy Jones | 4 | 9k |

This table is in 2NF. We also see that {Reputation} -> {Salary}. We still have redundancy because of this dependency. Salary is transitively dependent on reputation.
* we said that: attribute Z is transitively dependent on attribute X if it exists a Y such that X->Y, Y->Z, Y->X does not hold.
* for this example, PID determines Reputation (because it's a key). Reputation determines Salary(which is not a subset of PID or Reputation). Reputation does not determine PID. **By our definition, Salary is transitively dependent on PID**, so the second rule is broken.

A decomposition can be:
|Table 1|Table 2|
|--|--|
|<table> <tr><th>PID</th><th>Name</th><th>Reputation</th><th>Ship</th></tr><tr><td>p1</td><td>Jack Sparrow</td><td>5</td><td>BP</td></tr><tr><td>p2</td><td>Elizabeth Swan</td><td>6</td><td>BP</td></tr><tr><td>p3</td><td>Captain Barbossa</td><td>5</td><td>BP</td></tr><tr><td>p4</td><td>Will Turner</td><td>6</td><td>FD</td></tr><tr><td>p5</td><td>Davy Jones</td><td>4</td><td>FD</td></tr> </table>| <table> <tr><th>Reputation</th><th>Salary</th></tr><tr><td>5</td><td>10k</td></tr><tr><td>6</td><td>15k</td></tr><tr><td>4</td><td>9k</td></tr> </table>|


## BCNF
BCNF = (Boyce-Codd Normal Form)

Definition from lecture: **A relation is in BCNF if the determinant for each and every dependency is a candidate key.**

Even when a database is in 3rd Normal Form, still there would be anomalies resulted if it has more than one Candidate Key. Sometimes is BCNF is also referred as 3.5 Normal Form.

Example: For table EX_SCHEDULE(Date, Hour, FacultyMember, Room, Group) we can have these keys:
* key{Date, Group}: a group of students has at most one exam per date.
* key{FacultyMember, Date, Hour}: on a certain date and time, a faculty member has at most one exam
* key{Room, Date, Hour}:  on a certain date and time, in a certain room, we have at most one exam
* **and this functional dependency: FD{FacultyMember, Date}->{Room}**

This relation is in 3NF, but we still have redundancy.  We decompose it like this: 
* EX_SCHEDULE[Date, Hour, FacultyMember, Group] (we took out the dependent)
   * we still have the keys {Date, Group} and {FacultyMember, Date, Hour}, but {Room, Date, Hour} is lost.
* ROOM_ALLOCATION[FacultyMember, Date, Room] 
   * here we move {Room, Date, Hour}  

Now there are not any dependencies in which the left side is not a key. Reformulation: **in the left side, we only need to have keys**. Before, we had the key{Room, Date, Hour} and the dependency: FD{FacultyMember, Date}->{Room}, and FacultyMember was not a key. 
 
## 4NF 
Definition from lecture: A relation is in 4NF if and only if for every MVD that holds over our relation, one of the following statements is true:
* the MVD is trivial
* the left side of the MVD is a super key.

Basically: If no database table instance contains two or more, independent and multivalued data describing the relevant entity, then it is in 4th Normal Form.

Rules for 4th Normal Form:
* It should be in the Boyce-Codd Normal Form.
* And, the table should not have any Multi-valued Dependency.

### What is Multi-valued Dependency?
A table is said to have multi-valued dependency, if the following conditions are true:
* For a dependency A → B, if for a single value of A, multiple value of B exists, then the table may have multi-valued dependency.
* Also, a table should have at-least 3 columns for it to have a multi-valued dependency.
* And, for a relation R(A,B,C), if there is a multi-valued dependency between, A and B, then B and C should be independent of each other.

If all these conditions are true for any relation(table), it is said to have multi-valued dependency.

### Time for an Example
Below we have a college enrolment table with columns s_id, course and hobby.

| s_id | course | hobby |
| -- | -- | -- |
| 1	| Science |	Cricket |
| 1	| Maths |	Hockey |
| 2	| C# | Cricket |
| 2	| Php | Hockey |

As you can see in the table above, student with s_id 1 has opted for two courses, Science and Maths, and has two hobbies, Cricket and Hockey.

You must be thinking what problem this can lead to, right?

Well the two records for student with s_id 1, will give rise to two more records, as shown below, because for one student, two hobbies exists, hence along with both the courses, these hobbies should be specified.

| s_id | course | hobby |
| -- | -- | -- |
| 1	| Science | Cricket |
| 1	| Maths	| Hockey |
| 2	| Science	| Hockey |
| 2	| Maths	| Cricket |

And, in the table above, there is no relationship between the columns course and hobby. They are independent of each other. So there is multi-value dependency, which leads to un-necessary repetition of data and other anomalies as well.

How to satisfy 4th Normal Form?
To make the above relation satify the 4th normal form, we can decompose the table into 2 tables.

|CourseOpted Table|Hobbies Table|
|--|--|
|<table> <tr><th>s_id</th><th>course</th></tr><tr><td>1</td><td>Science</td></tr><tr><td>1</td><td>Maths</td></tr><tr><td>2</td><td>C#</td></tr><tr><td>2</td><td>PHP</td></tr> </table>| <table> <tr><th>s_id</th><th>hobby</th></tr><tr><td>1</td><td>Cricket</td></tr><tr><td>1</td><td>Hockey</td></tr><tr><td>2</td><td>Cricket</td></tr><tr><td>2</td><td>Hockey</td></tr> </table>|

## 5NF 
A table is in 5th Normal Form only if it is in 4NF and it cannot be decomposed into any number of smaller tables without loss of data.

If a table can be recreated by joining multiple tables and each of this table have a subset of the attributes of the table, then the table is in **Join Dependency**. It is a generalization of Multivalued Dependency

That would mean that if by doing a join relation on some relations and the result is equal to our original relation, then it;s not in 5NF.

## 6NF (Sixth Normal Form) Proposed
6th Normal Form is not standardized, yet however, it is being discussed by database experts for some time. Hopefully, we would have a clear & standardized definition for 6th Normal Form in the near future…
