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
Suppose you want to change the salary for a particular reputation. If you only change it in a tuple and not the other ones, we will have an inconsistancy in the database. We have tomake sure all the tuples are modified accordigly. (For repuration 5, you need to change both the first and third row)

### Insertion Anomaly
Can we add a salary for a particular reputation value if currently, in the database, there is no pirate with that reputation ? (Let's say for reputation 7 we want 20k salary). There is no pirate, but can we add a row like  "NULL, NULL, 7, NULL, 20K" ? No, because the PK is null. So we cannot do it. To add a new rep, we also need to add a pirate with that rep. It;s too restrictive

### Deletion Anomaly
What if we fire Sparrow and Barbossa (both with reputation 5 and salary 10k)? Then we lose the salary for reputation 5. We lose the association between them. 

### How to solve this?
Normalization rules **divides larger tables into smaller tables and links them** using relationships. The purpose of Normalisation in SQL is to eliminate redundant (repetitive) data and ensure data is stored logically.

We can eliminate those 3 anomalies by creating 2 tables: One that stores pirates and one that stores the association between reputation and salary:

| PID | Name | Reputation | Ship |
| -- | -- | -- | -- |
| p1 | Jack Sparrow | 5 | BP |
| p2 | Elizabeth Swan | 6 | BP |
| p3 | Captain Barbossa | 5 | BP |
| p4 | Will Turner | 6 | FD |
| p5 | Davy Jones | 4 | FD |

| Reputation | Salary |
| -- | -- |
| 5 | 10k |
| 6 | 15k |
| 4 | 9k |

### Decomposition
A relation R is decomposed into relations R1, R2 .. Rm. A **good decomposition** means that we can recover the original relation (in our case R) from the smaller relations. If the decomposition is irreversible, then it's bad. 

![image](https://user-images.githubusercontent.com/53339016/150659712-1bc5decf-b08c-4c04-a9f5-c03faff08048.png)
See more at Lecture 7 (or the readMe for relational algebra if it exists)

 
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
Definition from lecture: **A relation is in the first normal form if it doesn;t have any repeating attributes.(which is in accordance with the definition of a relation in the relational model)**

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
Before talking about 2NF, let's take a look at "functional dependency"

### Functional dependency

![image](https://user-images.githubusercontent.com/53339016/150660698-4cf1fc2d-d80c-4b8c-b269-0e8b39a4112f.png)

(P.S: {the determinant} -> {the dependent})

**{Reputation} -> {Salary} It's a functional dependence**. (Reputation determines salary). 

**Functional Dependency** (FD) is a constraint that determines the relation of one attribute to another attribute in a Database Management System (DBMS). Functional Dependency helps to maintain  the quality of data in the database. It plays a vital role to find the difference between good and bad database design. If the relation contains such a functional dependency, the following problems can arise (some of them need to be solved through additional programming efforts - executing a SQL command is not enough):
* **are wasting space** (we are stating the fact that the salary for the reputation as many times as there are pirates with that reputation)
* **have update/insertion/deletion anomalies** (see the beginning of this readme).

### Functional dependency properties
* **Property 1**: If K is a key of a relationship R[A1, A2, ..., An], **then K -> V**, oricare V a subset of {A1, A2, ..., An}
   * ex: {the key} -> {any attribute/set of attributes}
* **Property 2**: ![image](https://user-images.githubusercontent.com/53339016/150660935-c1b3296e-14c0-4719-b7ca-bd19a964a9b9.png) 
   * ex: {LastName, FirstName} -> {LastName}, {LastName, FirstName} -> {FirstName}, {LastName, FirstName} -> {LastName, FirstName}
* **Property 3**: ![image](https://user-images.githubusercontent.com/53339016/150661083-42786986-9978-4ca5-9ceb-52a93d0b1a8c.png)


The functional dependency among sets of attributes is what causes the previous anomalies; to eliminate these problems, the associations (dependencies) among values should be kept once in a separate relation, therefore, **the initial relation should be decomposed** (via a good decomposition - data should not be lost or added); such a decomposition is performed in the database design phase, when functional dependencies can be identified

A functional dependency is denoted by an arrow “→”. The functional dependency of X on Y is represented by X → Y. Let’s understand Functional Dependency in DBMS with **this example**:

Consider the following relation, storing students' learning contracts: \
CONTRACTS[LastName, FirstName, CNP, CourseId, CourseName] 
* key: {CNP, CourseId}
* **functional dependencies**: {CNP} → {LastName, FirstName}, {CourseId} → {CourseName}

To eliminate these dependencies, the relation is decomposed into the
following three relations:
* STUDENTS[CNP, LastName, FirstName]
* COURSES[CourseId, CourseName]
* LEARNING_CONTRACTS[CNP, CourseId]

Rules:
* **Be in 1NF**
* **Have a single column Primary Key that does not functionally depend on any subset of candidate key relation**

It is clear that we can’t move forward to make our simple database in 2nd Normalization form unless we partition the table above:

Table1: \
![](https://www.guru99.com/images/Table1.png) \
Table2: \
![](https://www.guru99.com/images/Table2.png)

We have divided our 1NF table into two tables :Table 1 and Table2. Table 1 contains member information. Table 2 contains information on movies rented. We have introduced a new column called Membership_id which is the primary key for table 1. In Table 2, Membership_ID is the Foreign Key


## 3NF (Third Normal Form) Rules
* **Be in 2NF**
* **Has no transitive functional dependencies**

A **transitive functional dependency** is when changing a non-key column, might cause any of the other non-key columns to change. Consider the table 1. Changing the non-key column Full Name may change Salutation.

![](https://www.guru99.com/images/transitive_functional_dependencies.png)

We need to divide again our tables and create a new table which stores Salutations. There are no transitive functional dependencies, and hence our table is in 3NF. In Table 3 Salutation ID is primary key, and in Table 1 Salutation ID is foreign to primary key in Table 3.

![](https://www.guru99.com/images/2NFTable1.png)
![](https://www.guru99.com/images/2NFTable2.png)
![](https://www.guru99.com/images/2NFTable3.png)

## BCNF (Boyce-Codd Normal Form)
Even when a database is in 3rd Normal Form, still there would be anomalies resulted if it has more than one Candidate Key. Sometimes is BCNF is also referred as 3.5 Normal Form.

**CANDIDATE KEY** in SQL is a set of attributes that uniquely identify tuples in a table. Candidate Key is a super key with no repeated attributes. The Primary key should be selected from the candidate keys. Every table must have at least a single candidate key. A table can have multiple candidate keys but only a single primary key.

## 4NF 
If no database table instance contains two or more, independent and multivalued data describing the relevant entity, then it is in 4th Normal Form.

## 5NF 
A table is in 5th Normal Form only if it is in 4NF and it cannot be decomposed into any number of smaller tables without loss of data.

## 6NF (Sixth Normal Form) Proposed
6th Normal Form is not standardized, yet however, it is being discussed by database experts for some time. Hopefully, we would have a clear & standardized definition for 6th Normal Form in the near future…
