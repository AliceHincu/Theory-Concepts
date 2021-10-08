# Relational Model
![](https://www.tutorialspoint.com/dbms/images/relational_model_table.png)

The most popular data model in DBMS is the Relational Model. It is more scientific a model than others. This model is based on first-order predicate logic and defines a table as an **n-ary relation**. **The schema** of a relation specifies **the name of the relation, the name and type of each field/attribute/column**.

ex: Movie(mid: string, title: string, director: string, year: integer)

Data is stored in tables called **relations**. Relations can be normalized. In normalized relations, values saved are atomic values. \
Each row in a relation contains a unique value. \
Each column in a relation contains values from a same domain.

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
Relational Integrity constraints in DBMS are referred to conditions which must be present for a valid relation. These Relational constraints in DBMS are derived from the rules in the mini-world that the database represents.

There are many types of Integrity Constraints in DBMS. Constraints on the Relational database management system is mostly divided into three main categories are: 
1. Domain Constraints 
2. Key Constraints 
3. Referential Integrity Constraints 

### -- Domain Constraints
**Domain constraints can be violated if an attribute value is not appearing in the corresponding domain or it is not of the appropriate data type.**

Domain constraints specify that within each tuple, and the value of each attribute must be unique. This is specified as data types which include standard data types integers, real numbers, characters, Booleans, variable length strings, etc.

**Example:**

Create DOMAIN CustomerName \
CHECK (value not NULL)

The example shown demonstrates creating a domain constraint such that CustomerName is not NULL

### -- Key Constraints
An attribute that can uniquely identify a tuple in a relation is called the key of the table. The value of the attribute for different tuples in the relation has to be unique.

**Example:**

In the given table, CustomerID is a key attribute of Customer Table. It is most likely to have a single key for one customer, CustomerID=1 is only for the CustomerName=”Google”.

| CustomerID | CustomerName | Status |
| -- | -- | -- |
| 1	| Google | Active |
| 2	| Amazon | Active |
| 3	| Apple	| Inactive |

### -- Referential Integrity Constraints
Referential Integrity constraints in DBMS are based on the concept of Foreign Keys. **A foreign key is an important attribute of a relation which should be referred to in other relationships**. Referential integrity constraint state happens where **relation refers to a key attribute of a different or same relation**. However, that key element must exist in the table.

**Example:**

![](https://cdn.guru99.com/images/1/091318_0803_RelationalD2.png)

In the above example, we have 2 relations, Customer and Billing. Tuple for CustomerID =1 is referenced twice in the relation Billing. So we know CustomerName=Google has billing amount $300

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
