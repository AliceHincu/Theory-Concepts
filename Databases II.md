# Introduction to database
**Database**: Database is a **collection of inter-related data** which helps in efficient retrieval, insertion and deletion of data from database and organizes the data in the form of tables, views, schemas, reports etc. For example, university database organizes the data about students, faculty, and admin staff etc. which helps in efficient retrieval, insertion and deletion of data from it

Basically:
* **database design**: we'll describe an organization from the real world, like university, hospital, in terms of the data stored in the database
* **data analysis**: we'll answear questions about the organization by writing querys over the data in the database

**If we want to use a database, we must first describe the data according to a data model.**

# Data description model (DDM)
**Data modeling** (data modelling) **is the process of creating a data model for the data to be stored in a database**. Data modeling helps in the visual representation of data and enforces business rules, regulatory compliances, and government policies on the data. 

**The Data Description Model is a set of concepts and rules used to model data**. These concepts are used to **describe the structure of the data**, to **specify consistency 
constraints**(that is correctness constrains) and to **describe relationships among data**. It is defined as an abstract model that organizes data description, data semantics, and consistency constraints of data. The data model **emphasizes on what data is needed and how it should be organized** instead of what operations will be performed on data. Data Model is like an architect’s building plan, which helps to build conceptual models and set a relationship between data items.

**schema of the database** = certain data structures are used in order to describe a collection of data stored in a database, and they constitute the schema.
**instances of the schema** = the data items in the collection that follow the schema

Examples of DDM:
* **Entity-Relationship Model**
* **Relational Model**


## Entity-Relationship Model
![](https://www.tutorialspoint.com/dbms/images/er_model_intro.png)
Entity-Relationship (ER) Model is based on the notion of real-world entities and relationships among them. While formulating real-world scenario into the database model, the ER Model creates entity set, relationship set, general attributes and constraints.

ER Model is best used for the conceptual design of a database.

ER Model is based on:
* **Entities** and their attributes.
* **Relationships** among entities.

**Entity** − An entity in an ER Model is a real-world entity having properties called attributes. Every attribute is defined by its set of values called domain. For example, in a school database, a student is considered as an entity. Student has various attributes like name, age, class, etc. \
**Relationship** − The logical association among entities is called relationship. Relationships are mapped with entities in various ways. Mapping cardinalities define the number of association between two entities.

Mapping cardinalities:
* one to one
* one to many
* many to one
* many to many


Read more: [1](https://www.tutorialspoint.com/dbms/dbms_data_models.htm)
