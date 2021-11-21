# What is normalization?
**Normalization** is a database design technique that **reduces data redundancy** and **eliminates undesirable characteristics like Insertion, Update and Deletion Anomalies**. Normalization rules **divides larger tables into smaller tables and links them** using relationships. The purpose of Normalisation in SQL is to eliminate redundant (repetitive) data and ensure data is stored logically.

## Database Normal Forms
Here is a **list of Normal Forms** in SQL:
* 1NF (First Normal Form)
* 2NF (Second Normal Form)
* 3NF (Third Normal Form)
* BCNF (Boyce-Codd Normal Form)
* 4NF (Fourth Normal Form)
* 5NF (Fifth Normal Form)
* 6NF (Sixth Normal Form)

Let's say we have this example: Assume, a video library maintains a database of movies rented out. Without any normalization in database, all information is stored in one table as shown below
![](https://www.guru99.com/images/NormalizationTable1.png)

## 1NF 
Rules: 
* **Each table cell should contain a single value.**
* **Each record needs to be unique**.

The above example in 1NF:
![](https://www.guru99.com/images/1NF.png)

In our database, we have two people with the same name Robert Phil, but they live in different places. Hence, we require both Full Name and Address to identify a record uniquely. That is a **composite key**. A composite key is a primary key composed of multiple columns used to identify a record uniquely

## 2NF
Rules:
* **Be in 1NF**
* **Have a single column Primary Key that does not functionally depend on any subset of candidate key relation**

It is clear that we can’t move forward to make our simple database in 2nd Normalization form unless we partition the table above:

Table1: \
![](https://www.guru99.com/images/Table1.png) \
Table2: \
![](https://www.guru99.com/images/Table2.png)

We have divided our 1NF table into two tables :Table 1 and Table2. Table 1 contains member information. Table 2 contains information on movies rented. We have introduced a new column called Membership_id which is the primary key for table 1. In Table 2, Membership_ID is the Foreign Key

## Functional dependency

| EXAM | StudentName | Course | Grade | FacultyMember |
| -- | -- | -- | -- | -- |
| 1 | Pop Ioana | Computer Networks | 10 | Matei Ana |
| 2 | Vlad Ana | Operating Systems | 10 | Simion Bogdan |
| 3 | Vlad Ana | Computer Networks | 9.98 | Matei Ana |
| 4 | Dan Andrei | Computer Networks | 10 | Matei Ana |
| 5 | Popescu Alex | Operating Systems | 9.99 | Simion Bogdan |

**Functional Dependency** (FD) is a constraint that determines the relation of one attribute to another attribute in a Database Management System (DBMS). Functional Dependency helps to maintain the quality of data in the database. It plays a vital role to find the difference between good and bad database design. If the relation contains such a functional dependency, the following problems can arise (some of them need to be solved through additional programming efforts - executing a SQL command is not enough):
* **wasting space**: the same associations are stored multiple times, e.g., the one among Computer Networks and Matei Ana is stored 3 times;
* **update anomalies**: if the FacultyMember is changed for course c, the change must be carried out in all associations involving course c (without knowing how many such associations exist), otherwise the database will contain errors (it will be inconsistent); if the FacultyMember value is changed in the 2nd record, but not in the 5th record, the operation will introduce an error in the relation (the data will be incorrect);
* **insertion anomalies**: one cannot specify the FacultyMember for a course c, unless there’s at least one student with a grade in course c;
* **deletion anomalies**: when some records are deleted, data that is not intended to be removed can be deleted as well; e.g., if records 1, 3 and 4 are deleted, the association among Course and FacultyMember is also removed from the database

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
