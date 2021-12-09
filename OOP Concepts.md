# Class

# Object
### Object Definitions:
* An object is **a real-world entity**.
* An object is **a runtime entity**.
* The object is **an entity which has state and behavior**.
* The object is **an instance of a class**.

### Real-world entity
Objects are defined as real world entities such as a table , chair , laptop etc ... all are objects ... and the collection of these objects is called a class.

### Runtime entity
` Student stud = new Student() ` Here if you think that stud is an object, then you're mistaken. Here **stud is a reference variable NOT an object**. 

**An object is a memory area created at runtime whose reference/address/location is accessed by the reference variable** (it's a reference to an object is stored hence the name "reference variable" ). A reference variable is created while coding (before compilation and also before runtime). An object is created at runtime (after compilation).

### It is characterized by three features:
* **Identity** - is a characteristic used to uniquely identify that object – such as a random ID number or **an address in memory**.
* **State** - is stored in **fields** (variables)  that represent the individual characteristics of that object
* **Behavior** -  is exposed through **methods** that operate its internal state.
* For example, a cat’s state includes its color, size, gender, and age, while its behavior is sleeping, purring, meowing for food, or running around like crazy at 4 AM.

### new
The `New` keyword in Java is used very often to create a new object. But what `new` does is allocate memory for the object of class you are making and returns a reference. That means, **whenever you create an object as static or local, it gets stored in heap**.

There are three steps to **creating a Java object**:
* **Declaration** of the object - When a Java object is declared, a name is associated with that object
 ``` java
 ClassName obj;
 ``` 
* **Instantiation** of the object - The object is instantiated so that memory space can be allocated
 ``` java
 // Simple meaning of instantiate is creating an object from class.
    ClassName obj = new ClassName(); 
 ``` 
* **Initialization** of the object - Initialization is the process of assigning initial values to the object attribute
