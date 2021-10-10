# ANSI-SPARC Architecture (Data abstraction)
In 1971, DBTG(DataBase Task Group) realized the requirement for a two-level approach having views and schema and afterward, in 1975, ANSI-SPARC realized the need for a three-level approach with the **three levels of abstraction** comprises of an **external/view**, **conceptual/logical** and an **internal/physycal** level. The three-level architecture aims to separate each user’s view of the database from the way the database is physically represented.

**Data Abstraction** is a process of hiding unwanted or irrelevant details from the end user. It provides a different view and helps in achieving data independence which is used to enhance the security of data. The database systems consist of complicated data structures and relations. For users to access the data easily, these complications are kept hidden, and only the relevant part of the database is made accessible to the users through data abstraction.

![](https://cdn.guru99.com/images/1/042919_0417_DataIndepen1.png)


### ---- Internal level / Physical
At the internal level, **the database is represented physically on the computer**. It emphasizes the physical implementation of the database to do **storage space utilization** and to **achieve the optimal runtime performance, and data encryption techniques**. It interfaces with the operating system to place the data on storage files and build the storage space, retrieve the data, etc.

**This is the lowest level of data abstraction**. It tells us **how the data is actually stored in memory**. It defines data-structures to store data and access methods used by the database. Actually, it is decided by developers or database application programmers how to store the data in the database. It is a very complex level to understand. 

For example, customer's information is stored in tables and data is stored in the form of blocks of storage such as bytes, gigabytes etc. Suppose we need to store the details of an employee. Blocks of storage and the amount of memory used for these purposes are kept hidden from the user. 


### ---- Conceptual level / Logical Level
Logical level is the intermediate level or next higher level. **It describes what data is stored in the database and what relationship exists among those data**. It tries to describe the entire or whole data because it describes what tables to be created and what are the links among those tables that are created. It is less complex than the physical level. Logical level is used by developers or database administrators (DBA). So, overall, the logical level contains tables (fields and attributes) and relationships among table attributes.

**This level comprises(cuprinde) the information that is actually stored in the database in the form of tables**. It also stores the relationship among the data entities in relatively simple structures. At this level, the information available to the user at the view level is unknown. 

We can store the various attributes of an employee and relationships, e.g. with the manager can also be stored. 


### ---- External level
**It is how the user views the database**. The data of the database that is relevant to that user is described at this level. The external level consists of several different external views of the database. In the external view **only the entities, attributes, and relationships that the user wants are included**. The different views may have different ways of representing the same data. For example, one user may view name in the form (firstname, lastname), while another may view as (lastname, firstname). It also simplifies interaction with the user and it provides many views or multiple views of the same database.

**This is the highest level of abstraction**. Only a part of the actual database is viewed by the users. This level exists to ease the accessibility of the database by an individual user. Users view data in the form of rows and columns. Tables and relations are used to store data. Multiple views of the same database may exist. Users can just view the data and interact with the database, storage and implementation details are hidden from them. 

For example, a user can interact with a system using GUI that is view level and can enter details at GUI or screen and the user does not know how data is stored and what data is stored, this detail is hidden from the user.

Taken from: [1](https://www.geeksforgeeks.org/the-three-level-ansi-sparc-architecture/), [2](https://www.geeksforgeeks.org/data-abstraction-and-data-independence/), [3](https://www.tutorialspoint.com/what-is-data-abstraction-in-dbms)

# Data Independence
Data Independence is defined as a property of DBMS that **helps you to change the Database schema at one level of a database system without requiring to change the schema at the next higher level**. Data independence helps you to keep data separated from all programs that make use of it. You can use this stored data for computing and presentation. In many systems, data independence is an essential function for components of the system.

**Data independence is the ability to modify the scheme without affecting the programs and the application to be rewritten**. Data is separated from the programs, so that the changes made to the data will not affect the program execution and the application. We know the main purpose of the three levels of data abstraction is to achieve data independence. If the database changes and expands over time, it is very important that the changes in one level should not affect the data at other levels of the database. This would save time and cost required when changing the database.

There are two levels of data independence based on three levels of abstraction:
* Physical Data Independence
* Logical Data Independence

### ---- Physical Data Independence
**Physical Data Independence means changing the physical level without affecting the logical level or conceptual level**. Using this property, we can change the storage device of the database without affecting the logical schema.

The changes in the physical level may include changes using the following:
* A new storage device like magnetic tape, hard disk, etc.
* A new data structure for storage.
* A different data access method or using an alternative files organization technique.
* Changing the location of the database.

### ---- Logical Data Independence
Logical view of data is the user view of the data. It presents data in the form that can be accessed by the end users.

Codd’s Rule of Logical Data Independence says that u**sers should be able to manipulate the Logical View of data without any information of its physical storage**. Software or the computer program is used to manipulate the logical view of the data.

Database administrator is the one who decides what information is to be kept in the database and how to use the logical level of abstraction. It provides the global view of Data. It also describes what data is to be stored in the database along with the relationship.

The data independence provides the database in simple structure. It is based on application domain entities to provide the functional requirement. It provides abstraction of system functional requirements. Static structure for the logical view is defined in the class object diagrams. Users cannot manipulate the logical structure of the database.

The changes in the logical level may include:
* Change the data definition.
* Adding, deleting, or updating any new attribute, entity or relationship in the database.

### Difference between Physical and Logical Data Independence
| Logica Data Independence | Physical Data Independence |
| --- | --- |
| Is mainly concerned with the structure or changing the data definition. | Mainly concerned with the storage of the data. |
| It is difficult as the retrieving of data is mainly dependent on the logical structure of data | It is easy to retrieve. |
| Compared to Physical independence it is difficult to achieve logical data independence. |	Compared to Logical Independence it is easy to achieve physical data independence. |
| You need to make changes in the Application program if new fields are added or deleted from the database. |	A change in the physical level usually does not need change at the Application program level. |
| Modification at the logical levels is significant whenever the logical structures of the database are changed. | Modifications made at the internal levels may or may not be needed to improve the performance of the structure. |
| Concerned with conceptual schema | Concerned with internal schema |
| Example: Add/Modify/Delete a new attribute | Example: change in compression techniques, hashing algorithms, storage devices, etc |

### Importance of Data Independence
* Helps you to **improve the quality of the data**
* Database system **maintenance becomes affordable**
* Enforcement of standards and improvement in database security
* You don’t need to alter data structure in application programs
* Permit developers to **focus on the general structure of the Database rather than worrying about the internal implementation**
* It allows you to improve state which is undamaged or undivided
* Database incongruity is vastly reduced.
* Easily make modifications in the physical level is needed to improve the performance of the system.


Taken from: [1](https://www.tutorialspoint.com/what-is-data-independence-in-dbms), [2](https://www.guru99.com/dbms-data-independence.html)
