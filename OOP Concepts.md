Content:
* [Object](#object)
* [Class](#class)
  * [Modifiers](#modifiers)  
  * [Method Overloading](#method-overloading)
  * [Method Overriding ](#method-overriding )
* [Encapsulation](#encapsulation)
* [Inheritance](#inheritance)
* [Polymorphism](#polymorphism)
* [Abstraction](#abstraction)
* [Interface](#interface)
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
* **State** - is stored in **fields** (variables/attributes)  that represent the individual characteristics of that object
* **Behavior** -  is exposed through **methods** that operate its internal state.
* For example, a cat’s state includes its color, size, gender, and age, while its behavior is sleeping, purring, meowing for food, or running around like crazy at 4 AM.

### New
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

# Class
A class is a group of objects which have common properties. **It is a blueprint from which objects are created**. It is a logical entity. It can't be physical. A class in Java can contain:
* Fields
* Methods
* Constructors
* Blocks
* Nested class and interface

### Variable types
A class can contain any of the following variable types:
* **Local variables** − Variables defined inside methods, constructors or blocks are called local variables. The variable will be declared and initialized within the method and the variable will be destroyed when the method has completed.
* **Instance variables** − Instance variables are variables within a class but outside any method. These variables are initialized when the class is instantiated. Instance variables can be accessed from inside any method, constructor or blocks of that particular class. (Basically fields/attributes)
* **Class variables** − Class variables are variables declared within a class, outside any method, with the `static` keyword.

### Constructors
When discussing about classes, one of the most important sub topic would be **constructors**. Every class has a constructor. If we do not explicitly write a constructor for a class, the **Java compiler builds a default constructor for that class**. Each time a new object is created, at least one constructor will be invoked. The main rule of constructors is that they should have **the same name as the class**. A class can have more than one constructor.

### finalize
It is possible to define a method that will be called just before an object's final destruction by the garbage collector. This method is called finalize( ), and it can be used to ensure that an object terminates cleanly.

For example, you might use finalize( ) to make sure that an open file owned by that object is closed.

To add a finalizer to a class, you simply define the finalize( ) method. The Java runtime calls that method whenever it is about to recycle an object of that class.

Inside the finalize( ) method, you will specify those actions that must be performed before an object is destroyed.

The finalize( ) method has this general form −
```java
protected void finalize( ) {
   // finalization code here
}
```
Here, the keyword protected is a specifier that prevents access to finalize( ) by code defined outside its class.

This means that you cannot know when or even if finalize( ) will be executed. For example, if your program ends before garbage collection occurs, finalize( ) will not execute.

### Modifiers
**Access Control Modifiers** <br>
Java provides a number of access modifiers to set access levels for classes, variables, methods and constructors. The four access levels are :
* Visible to the package, the default. No modifiers are needed.
* Visible to the class only (**private**).
* Visible to the world (**public**).
* Visible to the package and all subclasses (**protected**).

**Non-Access Modifiers** <br>
Java provides a number of non-access modifiers to achieve many other functionality:
* The **static** modifier for creating class methods and variables.
* The **final** modifier for finalizing the implementations of classes, methods, and variables.
* The **abstract** modifier for creating abstract classes and methods.
* The **synchronized** and **volatile** modifiers, which are used for threads.

### Method Overloading
When there are multiple functions with same name but different parameters then these functions are said to be overloaded. Functions can be overloaded by:
* **change in number of arguments** 
* or/and **change in type of arguments**.

``` java
// Java program for Method overloading
  
class MultiplyFun {
    // Method with 2 parameter
    static int Multiply(int a, int b)
    {
        return a * b;
    }
   
    // Example by using different types of arguments
    // Method with the same name but 2 double parameter
    static double Multiply(double a, double b)
    {
        return a * b;
    }
    
    // Example by using different numbers of arguments
    // Method with the same name but 3 parameter
    static int Multiply(int a, int b, int c)
    {
        return a * b * c;
    }
}
  
class Main {
    public static void main(String[] args)
    {
  
        System.out.println(MultiplyFun.Multiply(2, 4));
        System.out.println(MultiplyFun.Multiply(5.5, 6.3));
        System.out.println(MultiplyFun.Multiply(2, 7, 3));
    }
}
Output:
8
34.65
42
```

### Method Overriding 
Method overriding is where a child class can override a method in its parent. An overridden method is essentially hidden in the parent class, and is not invoked unless the child class uses the super keyword within the overriding method.


``` java
// Java program for Method overriding
  
class Parent { 
    void Print() { System.out.println("parent class"); }
}
  
class subclass1 extends Parent {
    void Print() { System.out.println("subclass1"); }
}
  
class subclass2 extends Parent {
    void Print() { System.out.println("subclass2"); }
}
  
class TestPolymorphism3 {
    public static void main(String[] args)
    {
        Parent a;
  
        a = new subclass1();
        a.Print();
  
        a = new subclass2();
        a.Print();
    }
}
```
Output:
```
subclass1
subclass2
```

# Encapsulation 
It is one of the four fundamental OOP concepts. The other three are inheritance, polymorphism, and abstraction.

Encapsulation in Java is a mechanism of wrapping the data (variables) and the code acting on the data (methods) together as a single unit. In encapsulation, the variables of a class will be hidden from other classes, and can be accessed only through the methods of their current class. Therefore, it is also known as **data hiding**.

To achieve encapsulation in Java:
* Declare the variables of a class as private.
* Provide public setter and getter methods to modify and view the variables values.

Benefits of Encapsulation:
* The fields of a class can be made read-only or write-only.
* A class can have total control over what is stored in its fields.

# Inheritance
Inheritance can be defined as the process where one class acquires the properties (methods and fields) of another. With the use of inheritance the information is made manageable in a hierarchical order.

The class which inherits the properties of other is known as subclass (derived class, child class) and the class whose properties are inherited is known as superclass (base class, parent class).

Keywords:
* **extends** is the keyword used to inherit the properties of a class. With the use of the extends keyword, the subclasses will be able to inherit all the properties of the superclass except for the private properties of the superclass.
* The **super** keyword is similar to this keyword. Following are the scenarios where the super keyword is used:
 * It is used to **differentiate the members** of superclass from the members of subclass, if they have same names.
 * It is used to **invoke the superclas**s constructor from subclass.
* **implements** keyword is used with classes to inherit the properties of an interface. Interfaces can never be extended by a class.
* **instanceof** keyword is used to check determine whether Mammal is actually an Animal, and dog is actually an Animal.

### IS-A Relationship
**IS-A** is a way of saying: This object is a type of that object. Let us see how the extends keyword is used to achieve inheritance.
``` java
public class Animal {}

public class Mammal extends Animal {}

public class Reptile extends Animal {}

public class Dog extends Mammal {}
```

Now, based on the above example, in Object-Oriented terms, the following are true:
* Animal is the superclass of Mammal class.
* Animal is the superclass of Reptile class.
* Mammal and Reptile are subclasses of Animal class.
* Dog is the subclass of both Mammal and Animal classes.

Now, if we consider the IS-A relationship, we can say:
* Mammal IS-A Animal
* Reptile IS-A Animal
* Dog IS-A Mammal
* Hence: Dog IS-A Animal as well

### HAS-A relationship
This relationship helps to reduce duplication of code as well as bugs.
``` java
public class Vehicle{}
public class Speed{}

public class Van extends Vehicle {
   private Speed sp;
} 
```
This shows that class Van HAS-A Speed. By having a separate class for Speed, we do not have to put the entire code that belongs to speed inside the Van class, which makes it possible to reuse the Speed class in multiple applications.

In Object-Oriented feature, the users do not need to bother about which object is doing the real work. To achieve this, the Van class hides the implementation details from the users of the Van class. So, basically what happens is the users would ask the Van class to do a certain action and the Van class will either do the work by itself or ask another class to perform the action.

![](https://www.tutorialspoint.com/java/images/types_of_inheritance.jpg)
A very important fact to remember is that Java does not support multiple inheritance. This means that a class cannot extend more than one class. Therefore following is illegal:
```public class extends Animal, Mammal{} ```
However, a class can implement one or more interfaces, which has helped Java get rid of the impossibility of multiple inheritance.

# Polymorphism
**Polymorphism is the ability of an object to take on many forms**. The most common use of polymorphism in OOP occurs when a parent class reference is used to refer to a child class object. The word “poly” means many and “morphs” means forms, So it means many forms.

Any Java object that can pass more than one IS-A test is considered to be polymorphic. In Java, all Java objects are polymorphic since any object will pass the IS-A test for their own type and for the class Object. Real life example of polymorphism: A person at the same time can have different characteristic. Like a man at the same time is a father, a husband, an employee. So the same person posses different behavior in different situations. This is called polymorphism.

Another Example:
``` java
public interface Vegetarian{}
public class Animal{}
public class Deer extends Animal implements Vegetarian{}
```
Now, the Deer class is considered to be polymorphic since this has multiple inheritance. Following are true for the above examples:
* A Deer IS-A Animal
* A Deer IS-A Vegetarian
* A Deer IS-A Deer
* A Deer IS-A Object
When we apply the reference variable facts to a Deer object reference, the following declarations are legal:
``` java
Deer d = new Deer();
Animal a = d;
Vegetarian v = d;
Object o = d;
```
All the reference variables d, a, v, o refer to the same Deer object in the heap. 

In Java polymorphism is mainly divided into two types:
* Compile time Polymorphism - It is also known as static polymorphism. This type of polymorphism is achieved by **function overloading** or **operator overloading**. But **Java doesn’t support the Operator Overloading**.
* Runtime Polymorphism - It is also known as Dynamic Method Dispatch. It is a process in which a function call to the overridden method is resolved at Runtime. This type of polymorphism is achieved by **Method Overriding**. The method becomes a **virtual** one.

Read more about polymorphism (here)[https://secure-media.collegeboard.org/apc/Intro_to_Polymorphismin_Umbargar.pdf]

# Abstraction
Abstraction is a process of hiding the implementation details from the user, only the functionality will be provided to the user. In other words, **the user will have the information on what the object does instead of how it does it.**

In Java, abstraction is achieved using Abstract classes and interfaces. An Abstract Class is a class which contains the **abstract** keyword in its declaration is known as abstract class.
* Abstract classes may or may not contain **abstract methods**, i.e., methods without body ( public void get(); )
* If a class has at least one abstract method, then the class must be declared abstract.
* **If a class is declared abstract, it cannot be instantiated**.
* To use an abstract class, you have to inherit it from another class and **if you inherit an abstract class, you have to provide implementations to all the abstract methods** in it.

``` java
// Java program to illustrate the concept of Abstraction
  
abstract class Shape {
    String color;
  
    // these are abstract methods
    abstract double area();
    public abstract String toString();
  
    // abstract class can have a constructor
    public Shape(String color)
    {
        System.out.println("Shape constructor called");
        this.color = color;
    }
  
    // this is a concrete method
    public String getColor()
    {
        return color;
    }
}

class Circle extends Shape {
    double radius;
  
    public Circle(String color, double radius)
    {  
        // calling Shape constructor
        super(color);
        System.out.println("Circle constructor called");
        this.radius = radius;
    }
  
    @Override
    double area()
    {
        return Math.PI * Math.pow(radius, 2);
    }
  
    @Override
    public String toString()
    {
        return "Circle color is " + super.color + "and area is : " + area();
    }
}
  
class Rectangle extends Shape {
  
    double length;
    double width;
  
    public Rectangle(String color, double length, double width)
    {
        // calling Shape constructor
        super(color);
        System.out.println("Rectangle constructor called");
        this.length = length;
        this.width = width;
    }
  
    @Override
    double area()
    {
        return length * width;
    }
  
    @Override
    public String toString()
    {
        return "Rectangle color is " + super.color + "and area is : " + area();
    }
}
  
public class Test {
    public static void main(String[] args)
    {
        Shape s1 = new Circle("Red", 2.2);
        Shape s2 = new Rectangle("Yellow", 2, 4);
  
        System.out.println(s1.toString());
        System.out.println(s2.toString());
    }
}
```
Output:
```
Shape constructor called
Circle constructor called
Shape constructor called
Rectangle constructor called
Circle color is Redand area is : 15.205308443374602
Rectangle color is Yellowand area is : 8.0
```

# Interface
An interface is a reference type in Java. It is similar to class. It is a collection of abstract methods. A class implements an interface, thereby inheriting the abstract methods of the interface. The **interface keyword** is used to declare an interface

Interfaces have the following properties:
* An interface is implicitly abstract. You do not need to use the abstract keyword while declaring an interface.
* Each method in an interface is also implicitly abstract, so the abstract keyword is not needed.
* Methods in an interface are implicitly public.

When a class implements an interface, you can think of the class as signing a contract, agreeing to perform the specific behaviors of the interface. If a class does not perform all the behaviors of the interface, the class must declare itself as abstract.

``` java
interface Animal {
   public void eat();
   public void travel();
}

public class MammalInt implements Animal {
   public void eat() { System.out.println("Mammal eats"); }

   public void travel() { System.out.println("Mammal travels"); } 

   public int noOfLegs() { return 0; }

   public static void main(String args[]) {
      MammalInt m = new MammalInt();
      m.eat();
      m.travel();
   }
}
```

Output
```
Mammal eats
Mammal travels
```

When implementation interfaces, there are several rules :
* A class can implement more than one interface at a time.
* A class can extend only one class, but implement many interfaces.
* An interface can extend another interface, in a similar way as a class can extend another class.
