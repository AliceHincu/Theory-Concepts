# Relational Model :nerd_face:
![](https://www.tutorialspoint.com/dbms/images/relational_model_table.png)

**Relational Model represents the database as a collection of relations**. A relation is nothing but a table of values. Every row in the table represents a collection of related data values. These rows in the table denote a real-world entity or relationship. This model is based on first-order predicate logic and defines a table as an **n-ary relation**. 

**The schema** of a relation specifies:
* **the name of the relation**, 
* **the name and type of each field/attribute/column**.  

Data is stored in **tables called relations**. Each row in a relation contains a unique value. Each column in a relation contains values from a same domain.

### Example
**The relation schema**: Movie(mid: string, title: string, director: string, year: integer)

**The instance** of the Movie relation(the whole table):
![image](https://user-images.githubusercontent.com/53339016/150638929-06490d0d-2fd6-4706-a430-96cbd93c9783.png)


## Relational Model Concepts
* **Attribute**: Each column in a Table. Attributes are the properties which define a relation. e.g., Student_Rollno, NAME,etc.
* **Tables** – In the Relational model, **the relations are saved in the table format**. It is stored along with its entities. A table has two properties: rows and columns. **Rows represent records and columns represent attributes.**
* **Tuple** – It is nothing but a single row of a table, which contains a single record.
* **Relation Schema**: A relation schema represents the name of the relation with its attributes.
* **Degree**: The total number of attributes which in the relation is called the degree of the relation.
* **Cardinality**: Total number of rows present in the Table.
* **Column**: The column represents the set of values for a specific attribute.
* **Relation instance** – Relation instance is a finite set of tuples in the RDBMS system. Relation instances never have duplicate tuples.
* **Relation key** – Every row has one, two or multiple attributes, which is called relation key.
* **Attribute domain** – Every attribute has some pre-defined value and scope which is known as attribute domain

![](https://cdn.guru99.com/images/1/091318_0803_RelationalD1.png)

## Relational Integrity Constraints
**Information Integrity** is the trustworthiness and dependability of information. More specifically, it is the accuracy, consistency and reliability of the information content, processes and systems. Information integrity is also a prerequisite, because you need it for many other management decisions. If certain information cannot be trusted and has a low level of integrity, than a business has a low chance of success. You need information integrity to have a successful business.
  
**Relational Integrity constraints** in DBMS are referred to conditions which must be present for a valid relation. These Relational constraints in DBMS are derived from the rules in the mini-world that the database represents. They are **sets of rules that can help maintain the quality of information that is put up**. Integrity constraints are mostly used when trying to promote accuracy and consistency of data that is found in a relational database.  This is very important to companies because information can be considered as an asset to certain organizations and it must be protected.

There are many types of Integrity Constraints in DBMS. Constraints on the Relational database management system is mostly divided into three main categories are: 
1. Domain Constraints 
2. Key Constraints 
3. Referential Integrity Constraints 

### ---- Domain Constraints
**Domain constraints can be violated if an attribute value is not appearing in the corresponding domain or it is not of the appropriate data type.**

A domain integrity constraint is a set of rules that restricts the kind of attributes or values a column or relation can hold in the database table. For example, we can specify if a particular column can hold null values or not, if the values have to be unique or not, the data type or size of values that can be entered in the column, the default values for the column, etc.

**Example:**

Create DOMAIN CustomerName \
CHECK (value not NULL)

The example shown demonstrates creating a domain constraint such that CustomerName is not NULL

### ---- Key Constraints
An attribute that can uniquely identify a tuple in a relation is called the key of the table. The value of the attribute for different tuples in the relation has to be unique.

**Example:**

In the given table, CustomerID is a key attribute of Customer Table. It is most likely to have a single key for one customer, CustomerID=1 is only for the CustomerName=”Google”.

| CustomerID | CustomerName | Status |
| -- | -- | -- |
| 1	| Google | Active |
| 2	| Amazon | Active |
| 3	| Apple	| Inactive |

### ---- Referential Integrity Constraints
Referential Integrity Constraint ensures that there always exists a valid relationship between two tables. This makes sure that if a foreign key exists in a table relationship then it should always reference a corresponding value in the second table or it should be null. **A FOREIGN KEY is a field (or collection of fields) in one table, that refers to the PRIMARY KEY in another table.** Example of foreign key:

#### Persons Table
| PersonID | LastName | FirstName | Age |
| -- | -- | -- | -- |
| 1	| Hansen | Ola | 30 |
| 2	| Svendson | Tove |	23 |
| 3	| Pettersen | Kari | 20 |

#### Orders Table
| OrderID	| OrderNumber	| PersonID |
| -- | -- | -- |
| 1	| 77895 |	3 |
| 2	| 44678 |	3 |
| 3	| 22456 |	2 |
| 4	| 24562 |	1 |

* The table with the foreign key is called the child table, and the table with the primary key is called the referenced or parent table. 
* Notice that the "PersonID" column in the "Orders" table points to the "PersonID" column in the "Persons" table. 
* The "PersonID" column in the "Persons" table is the **PRIMARY KEY** in the "Persons" table. (=>parent table)
* The "PersonID" column in the "Orders" table is a **FOREIGN KEY** in the "Orders" table. (=> child table)

The **FOREIGN KEY constraint** prevents invalid data from being inserted into the foreign key column, because it has to be one of the values contained in the parent table.
**Example:**

![](https://cdn.guru99.com/images/1/091318_0803_RelationalD2.png)

In the above example, we have 2 relations, Customer and Billing. Tuple for CustomerID =1 is referenced twice in the relation Billing. So we know CustomerName=Google has billing amount $300

[Read more about Integrity Constraints in DBMS](https://www.educba.com/integrity-constraints-in-dbms/)

## Operations in Relational Model
Four basic update operations performed on relational database model are: Insert, update, delete and select.
* **Insert** is used to insert data into the relation
* **Delete** is used to delete tuples from the table.
* **Modify** allows you to change the values of some attributes in existing tuples.
* **Select** allows you to choose a specific range of data.

## Best Practices for creating a Relational Model
* Data needs to be represented as a collection of relations
* Each relation should be depicted clearly in the table
* Rows should contain data about instances of an entity
* Columns must contain data about attributes of the entity
* Cells of the table should hold a single value
* Each column should be given a unique name
* No two rows can be identical
* The values of an attribute should be from the same domain

## Advantages of using Relational Model
* **Simplicity**: A Relational data model in DBMS is simpler than the hierarchical and network model.
* **Structural Independence**: The relational database is only concerned with data and not with a structure. This can improve the performance of the model.
* **Easy to use**: The Relational model in DBMS is easy as tables consisting of rows and columns are quite natural and simple to understand
* **Query capability**: It makes possible for a high-level query language like SQL to avoid complex database navigation.
* **Data independence**: The Structure of Relational database can be changed without having to change any application.
* **Scalable**: Regarding a number of records, or rows, and the number of fields, a database should be enlarged to enhance its usability.

## Disadvantages of using Relational Model
* Few relational databases have limits on field lengths which can’t be exceeded.
* Relational databases can sometimes become complex as the amount of data grows, and the relations between pieces of data become more complicated.
* Complex relational database systems may lead to isolated databases where the information cannot be shared from one system to another.

Information taken from [here](https://www.guru99.com/relational-data-model-dbms.html)
