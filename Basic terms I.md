### Namespace

In computing, a namespace is a set of signs (names) that are used to identify and refer to objects of various kinds. A namespace ensures that all of a given set of objects 
have unique names so that they can be easily identified. Namespaces are commonly structured as hierarchies to allow reuse of names in different contexts. As an analogy, 
consider a system of naming of people where each person has a given name, as well as a family name shared with their relatives. If the first names of family members are 
unique only within each family, then each person can be uniquely identified by the combination of first name and family name; there is only one Jane Doe, though there may 
be many Janes. Within the namespace of the Doe family, just "Jane" suffices to unambiguously designate this person, while within the "global" namespace of all people, the 
full name must be used.

### Pass by value
The argument is evaluated, and a copy of the evaluation result is bound to the formal parameter of the function

### Pass by reference
Function receives a reference to the actual argument, rather than a copy to its value

### Object oriented programming
A programming paradigm that uses objects that have data and which "talk" to each other to design applications.

### Class
A construct used as a template to create instances of itself - referred to as class instances, class objects, instance objects or simply objects. A class defines constituent members which enable these class instances to have state and behaviour.

### Instance
In a computer system, any time a new context is created based on some model, it is said that the model has been instantiated. In practice, this instance usually has a data structure in common with other instances, but the values stored in the instances are separate. Changing the values in one instance will then not interfere with the values of some other instance. In object-oriented programming (OOP), an instance is a concrete occurrence of any object, existing usually during the runtime of a computer program. Formally, "instance" is synonymous with "object" as they are each a particular value (realization), and these may be called an instance object; "instance" emphasizes the distinct identity of the object. The creation of an instance is called instantiation.

### Object
In object-oriented programming, an object refers to a particular instance of a class, and is a combination of variables, functions and other data structures. Objects support two kinds of operations: attribute (data or method) references and instantiation.

### Encapsulation
The **state** of the object is the data that represents it (in most cases, the class fields)
The **behaviour** is represented by the class methods
**Encapsulation** means that state and behaviour are kept together, in one cohesive unit
P.S: cohesive = coerent =  Care se compune din elemente strâns legate (și armonizate) între ele; închegat

### Data abstraction
**Data abstraction** is a principle of data modeling theory that emphasizes the clear separation between the external interface of objects and internal data handling and manipulation. In many programming languages, interfaces (or abstract classes) provide abstraction, and their concrete implementations form the implementation.

This abstraction allows a much simpler API for the system models, mostly objects of different classes while having a complex internal structure. This separation enables APIs to remain essentially unchanged while the implementation of the API can improve over time. The net result is that the ecosystem built around the APIs does not break with every iterative refinement of the implementation.

Basically: Function and class specification have to be independent of the data representation and the method's implementation

### Interface
**Interfaces** are a structure of object-oriented programming language that defines the external behavior of data structures without defining how the data is stored. Each interface outlines the basic operations allowed on the data type. It becomes the responsibility of any data type that implements the interface to populate the functionality.

For example, the "map" type is an interface that offers a lookup functionality. This interface can be implemented by a binary search tree or by a list of two-element tuples. Either implementation can offer the lookup method and act the same for any user of the map data type.

### Abstract data type 
Data type + Data Abstraction + Data Encapsulation
