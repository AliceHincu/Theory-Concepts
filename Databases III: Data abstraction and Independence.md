# ANSI-SPARC Architecture (Data abstraction)
In 1971, DBTG(DataBase Task Group) realized the requirement for a two-level approach having views and schema and afterward, in 1975, ANSI-SPARC realized the need for a three-level approach with the **three levels of abstraction** comprises of an **external/view**, **conceptual/logical** and an **internal/physycal** level. The three-level architecture aims to separate each user’s view of the database from the way the database is physically represented.

**Data Abstraction** is a process of hiding unwanted or irrelevant details from the end user. It provides a different view and helps in achieving data independence which is used to enhance the security of data. The database systems consist of complicated data structures and relations. For users to access the data easily, these complications are kept hidden, and only the relevant part of the database is made accessible to the users through data abstraction.

![](https://cdn.guru99.com/images/1/042919_0417_DataIndepen1.png)


## Internal level / Physical
At the internal level, **the database is represented physically on the computer**. It emphasizes the physical implementation of the database to do **storage space utilization** and to **achieve the optimal runtime performance, and data encryption techniques**. It interfaces with the operating system to place the data on storage files and build the storage space, retrieve the data, etc.

**This is the lowest level of data abstraction**. It tells us **how the data is actually stored in memory**. It defines data-structures to store data and access methods used by the database. Actually, it is decided by developers or database application programmers how to store the data in the database. It is a very complex level to understand. 

For example, customer's information is stored in tables and data is stored in the form of blocks of storage such as bytes, gigabytes etc. Suppose we need to store the details of an employee. Blocks of storage and the amount of memory used for these purposes are kept hidden from the user. 


## Conceptual level / Logical Level
Logical level is the intermediate level or next higher level. **It describes what data is stored in the database and what relationship exists among those data**. It tries to describe the entire or whole data because it describes what tables to be created and what are the links among those tables that are created. It is less complex than the physical level. Logical level is used by developers or database administrators (DBA). So, overall, the logical level contains tables (fields and attributes) and relationships among table attributes.

**This level comprises(cuprinde) the information that is actually stored in the database in the form of tables**. It also stores the relationship among the data entities in relatively simple structures. At this level, the information available to the user at the view level is unknown. 

We can store the various attributes of an employee and relationships, e.g. with the manager can also be stored. 


## External level
**It is how the user views the database**. The data of the database that is relevant to that user is described at this level. The external level consists of several different external views of the database. In the external view **only the entities, attributes, and relationships that the user wants are included**. The different views may have different ways of representing the same data. For example, one user may view name in the form (firstname, lastname), while another may view as (lastname, firstname). It also simplifies interaction with the user and it provides many views or multiple views of the same database.

**This is the highest level of abstraction**. Only a part of the actual database is viewed by the users. This level exists to ease the accessibility of the database by an individual user. Users view data in the form of rows and columns. Tables and relations are used to store data. Multiple views of the same database may exist. Users can just view the data and interact with the database, storage and implementation details are hidden from them. 

For example, a user can interact with a system using GUI that is view level and can enter details at GUI or screen and the user does not know how data is stored and what data is stored, this detail is hidden from the user.

Taken from: [1](https://www.geeksforgeeks.org/the-three-level-ansi-sparc-architecture/), [2](https://www.geeksforgeeks.org/data-abstraction-and-data-independence/), [3](https://www.tutorialspoint.com/what-is-data-abstraction-in-dbms)
