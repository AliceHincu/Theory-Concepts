# Introduction
Components of an application :
- we have the **data** we are working with
- we have a **management algorithm** handling various operations on the data
- **user interface**

Data storage methods:
- **files** (ex: txt, xml, binary)
- **databases** (sql, mysql, oracle)
- **distributed** databases (a subset in a city, another one in bucharest etc etc)

P.S: query means a request for information.
# Why not choose files as a data storage method? Files vs DBMS
### File System 
File system is basically a way of arranging the files in a storage medium like hard disk. File system organizes the files and helps in retrieval of files when they are required. File systems consists of different files which are grouped into directories. The directories further contain other folders and files. File system performs basic operations like management, file naming, giving access rules etc.
### DBMS
Database Management System is basically a software that manages the collection of related data. It is used for storing data and retrieving the data effectively when it is needed. It also provides proper security measures for protecting the data from unauthorized access. In Database Management System the data can be fetched by SQL queries and relational algebra. It also provides mechanisms for data recovery and data backup. (ex: Oracle, MySQL, MS SQL server.)

### Disadvantages of the File system
- multiple data storage formats
- data redundancy (some data can be sotred in multiple files => potential inconsistencies)
- read / write operations are described in the program. Certain record structures are taken into account => difficulties in program development. When the file structre changes, the program must be changed as well.
- difficult to retreive data meeting certain criteria, difficult to change data
- what if we also want to specify corectness constrains? Integrity constrains are checked in the program...we need to write code for this.
- data concurrently accessed by multiple users (updates to be applied consistently), questions need quick answears, restrict access to some parts of the data. So, much more
data + many more user => more challenges => a collection of files is not enough
----- CHALLENGES: 
- there are no adequate security procedures
- concurrent data access control is a challenge
- recovery mechanisms -> restoring data to a consistent state when the system fails. Ex: a bank transaction, transferring money from account A1 to account A2. There are 2 update
operations here:taking money from account A1 and adding money to account A2. If there is a power failure between these, money should be restored to A1.
- operations on data can be quite epensive.
**THEY ARE USEFUL FOR SMALL AMOUNT OF DATA AND ONE USER.**

### Advantages of DBMS over File system
* **Data redundancy and inconsistency -** 
Redundancy is the concept of repetition of data i.e. each data may have more than a single copy. The **file system cannot control redundancy** of data as each user defines and maintains the needed files for a specific application to run. There may be a possibility that two users are maintaining same files data for different applications. Hence changes made by one user does not reflect in files used by second users, which leads to inconsistency of data. Whereas **DBMS controls redundancy** by maintaining a single repository of data that is defined once and is accessed by many users. As there is no or less redundancy, data remains consistent.
* **Data sharing –** 
**File system does not allow sharing of data** or sharing is too complex. Whereas **in DBMS, data can be shared easily** due to centralized system.
* **Data concurrency –**
Concurrent access to data means more than one user is accessing the same data at the same time. Anomalies occur when changes made by one user gets lost because of changes made by other user. F**ile system does not provide any procedure to stop anomalies**. Whereas **DBMS provides a locking system to stop anomalies to occur**.
* **Data searching –**
For every search operation performed on file system, a different application program has to be written. While DBMS provides inbuilt searching operations. User only have to write a small query to retrieve data from database.
* **Data integrity -**  
There may be cases when some constraints need to be applied on the data before inserting it in database. The file system does not provide any procedure to check these constraints automatically. Whereas DBMS maintains data integrity by enforcing user defined constraints on data by itself.
* **System crashing –** 
In some cases,systems might have crashes due to various reasons. It is a bane in case of file systems because once the system crashes, there will be no recovery of the data that’s been lost. A DBMS will have the recovery manager which retrieves the data making it another advantage over file systems. 
* **Data security –** 
A file system provides a password mechanism to protect the database but how longer can the password be protected?No one can guarantee that. This doesn’t happen in the case of DBMS. DBMS has specialized features that help provide shielding to its data. 

# Database Management System
We are dealing with unprecedented data growths. Huge, complex data sets. Organizations today can succeed if they are able to:
- extract correct infomation about their operations in a timely manner.
- use data to support operations.
- efficient data management capabilities.
=> hence the need flexible and powerful data management systems that simplify data management and are able to quicly extract information.
