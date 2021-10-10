# Entity-Relationship Model
![](https://www.tutorialspoint.com/dbms/images/er_model_intro.png)

Entity Relationship Model (ER Modeling) is a **graphical approach to database design**. It is a high-level data model that **defines data elements and their relationship** for a specified software system. An ER model is used to represent real-world objects. Entity-Relationship (ER) Model is based on the **notion of real-world entities and relationships among them**. While formulating real-world scenario into the database model, the ER Model creates entity set, relationship set, general attributes and constraints.

**ER Model is best used for the conceptual design of a database.**

# ER Diagrams Symbols & Notations
Entity Relationship Diagram Symbols & Notations mainly contains three basic symbols which are **rectangle, oval and diamond** to represent r**elationships between elements, entities and attributes**. There are some sub-elements which are based on main elements in ERD Diagram. ER Diagram is a visual representation of data that describes how data is related to each other using different ERD Symbols and Notations.

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

# Entity
An Entity is a **thing or object in real world that is distinguishable from surrounding environment**. An entity can be place, person, object, event or a concept, which stores data in the database. Every entity is made up of some ‘attributes’ which represent that entity, and they have an unique key. Every attribute is defined by its set of values called domain. For example, in a school database, a student is considered as an entity. Student has various attributes like name, age, class, etc. 

**Examples of entities:**
* Person: Employee, Student, Patient
* Place: Store, Building
* Object: Machine, product, and Car
* Event: Sale, Registration, Renewal
* Concept: Account, Course

An **entity set** is a group of similar kind of entities

# Relationship
**The logical association among entities** is called relationship. Entities can have relationships with each other. Relationship is nothing but an association among two or more entities. E.g., Tom works in the Chemistry department.

Relationships are mapped with entities in various ways. Mapping cardinalities define the number of association between two entities.

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
**Example**: *see seminar*

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
**Example**: many students belong to the same class.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Many-to-One-Cardinality-Ratio.png)

### Many-to-Many:
By this cardinality constraint:
* An entity in set A can be associated with any number (zero or more) of entities in set B.
* An entity in set B can be associated with any number (zero or more) of entities in set A.
**Example**: students as a group are associated with multiple faculty members, and faculty members can be associated with multiple students.

![](https://www.gatevidyalay.com/wp-content/uploads/2018/05/Many-to-Many-Cardinality-Ratio.png)

# Attributes
Attribute -> **It is a single-valued property of either an entity-type or a relationship-type.** For example, a lecture might have attributes: time, date, duration, place, etc. An attribute in ER Diagram examples, is represented by an Ellipse

| Types of Attributes	| Description |
| -- | -- |
| Simple attribute | Can’t be divided any further. For example, a student’s contact number. It is also called an atomic value. |
| Composite attribute	| It is possible to break down composite attribute. For example, a student’s full name may be further divided into first name, second name, and last name.|
| Derived attribute	| This type of attribute is not included in the physical database. However, their values are derived from other attributes present in the database. For example, age should not be stored directly. Instead, it should be derived from the date of birth of that employee. |
| Multivalued attribute |	Multivalued attributes can have more than one values. For example, a student can have more than one mobile number, email address, etc. |


Read more about ER: [1](https://www.gatevidyalay.com/er-diagrams/), [2](https://www.guru99.com/er-diagram-tutorial-dbms.html#2)
