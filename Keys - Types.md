# Composite key
A **composite key** is composed of two or more attributes, but it must be minimal.

From our COMPANY database example, if the entity is Employee(EID, First Name, Last Name, SIN, Address, Phone, BirthDate, Salary, DepartmentID), possible composite keys are:
* First Name and Last Name – assuming there is no one else in the company with the same name
* Last Name and Department ID – assuming two people with the same last name don’t work in the same department

# Candidate key
A **candidate key** is a simple or composite key that is unique and minimal.  It is unique because no two rows in a table may have the same value at any time. It is minimal because every column is necessary in order to attain uniqueness.

From our COMPANY database example, if the entity is Employee(EID, First Name, Last Name, SIN, Address, Phone, BirthDate, Salary, DepartmentID), possible candidate keys are:
* EID, SIN
* First Name and Last Name – assuming there is no one else in the company with the same name
* Last Name and DepartmentID – assuming two people with the same last name don’t work in the same department

# Primary key
The primary key(PK) is a candidate key that is selected by the database designer to be **used as an identifying mechanism for the whole entity set**. It must:
* **uniquely identify tuples** in a table 
* **not be null**. 
 
In the following example, EID is the primary key:

Employee(**_EID_**, First Name, Last Name, SIN, Address, Phone, BirthDate, Salary, DepartmentID)

**Alternate keys** are all candidate keys not chosen as the primary key.

# Foreign key
A **foreign key** (FK) is an attribute in a table that references the primary key in another table OR it can be null. Both foreign(_from this table_) and primary keys(_from the reference table not this one_) must be of the same data type.

In the COMPANY database example below, DepartmentID is the foreign key:

Employee(EID, First Name, Last Name, SIN, Address, Phone, BirthDate, Salary, **_DepartmentID_**)
