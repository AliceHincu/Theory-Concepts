# Entity-Relationship Model
![](https://www.tutorialspoint.com/dbms/images/er_model_intro.png)

Entity Relationship Model (ER Modeling) is a **graphical approach to database design**. It is a high-level, more abstract data model that **defines data elements and their relationship** for a specified software system. An ER model is used to represent real-world objects. 

Entity-Relationship (ER) Model is based on the **notion of real-world entities and relationships among them**. ER modelling is based on two concepts:
* Entities, defined as tables that hold specific information (data)
* Relationships, defined as the associations or interactions between entities

**The schema of the model**: the set of entity sets and relationship sets.

**ER Model is best used for the conceptual design of a database.**

# ER Diagrams Symbols & Notations
Entity Relationship Diagram Symbols & Notations mainly contains three basic symbols which are **rectangle, oval and diamond** to represent **relationships between elements, entities and attributes**. 

ER Diagram is a visual representation of data that describes how data is related to each other using different ERD Symbols and Notations.

Following are the main components and its symbols in ER Diagrams:
* **Rectangles**: for ENTITY 
* **Ellipses** : for ATTRIBUTES
* **Diamonds**: for RELATIONSHIP
* **Lines**: It links attributes to entity types and entity types with other relationship types
* **Primary key**: attributes are underlined

![](https://cdn.guru99.com/images/1/100518_0621_ERDiagramTu12.png)

# Components of the ER Diagram
This model is based on three basic concepts:
* Entities
* Attributes
* Relationships

![](https://cdn.guru99.com/images/1/100518_0621_ERDiagramTu2.png)

# 1. Entity
An Entity is a **thing or object in real world that is distinguishable from surrounding environment**. An entity can be place, person, object, event or a concept, which stores data in the database. 

Every entity is described by a set of **‘attributes’** and they:
* have a name 
* are defined by a set of values called **domain**.
* can have conditions to check correctness

For example, in a school database, a student is considered as an entity. Student has various attributes like name, age, class, etc.  The **entity set**(entity schema) is the set of students

An important constraint on an entity is the **key**. The key is an attribute or a group of attributes whose values can be used to uniquely identify an individual entity in an entity set. 

**Examples of entities:**
* Person: Employee, Student, Patient
* Place: Store, Building
* Object: Machine, product, and Car
* Event: Sale, Registration, Renewal
* Concept: Account, Course

# 2. Relationship
**The logical association among entities** is called relationship. 

Ex: Tom **works** in the Chemistry department.

**Relationship set**(schema) describes all relationships with the same structure

The **degree** of a relationship is the number of entity types that participate in the relationship. The three most common relationships in ER models are Binary, Unary and Ternary

## Unary relationships
An unary relationship, also called recursive, is one in which a relationship exists between occurrences of the same entity set. In this relationship, the primary and foreign keys are the same, but they represent two entities with different roles

**Example1**: Employee(EID, Name, Address, Birthdate, Salary, Super-EID)

You can have a supervisor and a supervisee. Both are employees, but the Super-EID in the supervisee row references a supervisor record. 

**Example 2:** Subjects may be prerequisites for other subjects.

![image](https://user-images.githubusercontent.com/53339016/150641971-9df3ddce-0e07-422e-89c6-da8c16077a68.png)


## Binary relationships
Mapping cardinalities:
* **One-to-One** Relationships
* **One-to-Many** Relationships
* **Many-to-One** Relationships
* **Many-to-Many** Relationships

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Cardinality-Ratios-in-DBMS.png)

### One-to-one:
By this cardinality constraint:
* An entity in set A can be associated with **at most one** entity in set B.
* An entity in set B can be associated with **at most one** entity in set A.

**Example**: the association between group and faculty member (to specify the groups' tutors)

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/One-to-One-Cardinality-Ratio.png)


### One-to-many:
By this cardinality constraint:
* An entity in set A can be associated with any number (zero or more) of entities in set B.
* An entity in set B can be associated with at most one entity in set A.

**Example**: one class is consisting of multiple students.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/One-to-Many-Cardinality-Ratio.png)

### Many-to-One:
By this cardinality constraint:
* An entity in set A can be associated with at most one entity in set B.
* An entity in set B can be associated with any number (zero or more) of entities in set A.

**Example**: the association between group and students

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Many-to-One-Cardinality-Ratio.png)

### Many-to-Many:
By this cardinality constraint:
* An entity in set A can be associated with any number (zero or more) of entities in set B.
* An entity in set B can be associated with any number (zero or more) of entities in set A.
**Example**: the association between courses and students

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Many-to-Many-Cardinality-Ratio.png)

## Ternary Relationships
A ternary relationship is a relationship type that **involves many to many relationships between three tables. **

Note n-ary means multiple tables in a relationship. (Remember, N = many.). 
* For each n-ary (> 2) relationship, create a new relation to represent the relationship.
* The primary key of the new relation is a combination of the primary keys of the participating entities that hold the N (many) side.
* In most cases of an n-ary relationship, all the participating entities hold a many side.

**Example**: The University might need to record which teachers taught which subjects in which courses.

![image](https://user-images.githubusercontent.com/53339016/150641993-54130d07-afb5-45d8-a397-b534a932ff5b.png)



# 3. Attributes
Attribute -> **It is a single-valued property of either an entity-type or a relationship-type.** For example, a lecture might have attributes: time, date, duration, place, etc. An attribute in ER Diagram examples, is represented by an Ellipse

| Types of Attributes	| Description |
| -- | -- |
| Simple attribute | Can’t be divided any further. For example, a student’s contact number. It is also called an atomic value. |
| Composite attribute	| It is possible to break down composite attribute. For example, a student’s full name may be further divided into first name, second name, and last name.|
| Derived attribute	| This type of attribute is not included in the physical database. However, their values are derived from other attributes present in the database. For example, age should not be stored directly. Instead, it should be derived from the date of birth of that employee. |
| Multivalued attribute |	Multivalued attributes can have more than one values. For example, a student can have more than one mobile number, email address, etc. |


Read more about ER: [1](https://www.gatevidyalay.com/er-diagrams/), [2](https://www.guru99.com/er-diagram-tutorial-dbms.html#2), [3](https://www.dlsweb.rmit.edu.au/Toolbox/ecommerce/tbn_respak/tbn_e2/html/tbn_e2_devsol/er_model_relnshps.htm)
