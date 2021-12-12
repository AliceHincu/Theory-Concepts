Content:
* [Generic Methods](#generic-methods)
* [Generic Classes](#generic-classes)
* [Bounded Type Parameters](#bounded-type-parameters)
* [Wildcards](#wildcards)
* [Erasure](#erasure)
* [Restrictions on Generics](#restrictions-on-generics)
# Why Use Generics?
**Generics enable types** (classes and interfaces) **to be parameters when defining classes, interfaces and methods**. Generics **add stability** to your code by making more of your bugs detectable at compile time. Type parameters provide a way for you to **re-use the same code with different inputs type**.

Code that uses generics has many benefits over non-generic code:
* **Stronger type checks at compile time**. A Java compiler applies strong type checking to generic code and issues errors if the code violates type safety. Fixing compile-time errors is easier than fixing runtime errors, which can be difficult to find.
* **Elimination of casts**. The following code snippet without generics requires casting:
```java
List list = new ArrayList();
list.add("hello");
String s = (String) list.get(0);
```
When re-written to use generics, the code does not require casting:
```java
List<String> list = new ArrayList<String>();
list.add("hello");
String s = list.get(0);   // no cast
```
* **Enabling programmers to implement generic algorithms**. By using generics, programmers can implement generic algorithms that work on collections of different types, can be customized, and are type safe and easier to read.

Example: It would be nice if we could write a single sort method that could sort the elements in an Integer array, a String array, or an array of any type that supports ordering. Using Java Generic concept, we might write a generic method for sorting an array of objects, then invoke the generic method with Integer arrays, Double arrays, String arrays and so on, to sort the array elements.

# Generic Methods
**You can write a generic method declaration that can be called with arguments of different types**. Based on the types of the arguments passed to the generic method, the compiler handles each method call appropriately. Static methods cannot use the type variables of the class.

**Example**: Following example illustrates how we can print an array of different type using a single Generic method :

``` java
public class GenericMethodTest {
   // generic method printArray
   public static < E > void printArray( E[] inputArray ) {
      // Display array elements
      for(E element : inputArray) {
         System.out.printf("%s ", element);
      }
      System.out.println();
   }

   public static void main(String args[]) {
      // Create arrays of Integer, Double and Character
      Integer[] intArray = { 1, 2, 3, 4, 5 };
      Double[] doubleArray = { 1.1, 2.2, 3.3, 4.4 };
      Character[] charArray = { 'H', 'E', 'L', 'L', 'O' };

      System.out.println("Array integerArray contains:");
      printArray(intArray);   // pass an Integer array

      System.out.println("\nArray doubleArray contains:");
      printArray(doubleArray);   // pass a Double array

      System.out.println("\nArray characterArray contains:");
      printArray(charArray);   // pass a Character array
   }
}
```
This will produce the following result
```
Array integerArray contains:
1 2 3 4 5 

Array doubleArray contains:
1.1 2.2 3.3 4.4 

Array characterArray contains:
H E L L O
```

# Generic Classes
A generic class declaration looks like a non-generic class declaration, except that **the class name is followed by a type parameter section**. Just like generic methods, the _type parameter section_ of a generic class can have one or more type parameters separated by commas. These classes are known as _parameterized classes_ or parameterized types because they accept one or more parameters.

### non-generic Box class
Begin by examining a  that operates on objects of any type. It needs only to provide two methods: _set_, which adds an object to the box, and _get_, which retrieves it:
```java
public class Box {
    private Object object;

    public void set(Object object) { this.object = object; }
    public Object get() { return object; }
}
```
Since its methods accept or return an Object, you are free to pass in whatever you want, provided that it is not one of the primitive types. **There is no way to verify, at compile time, how the class is used**. One part of the code may place an Integer in the box and expect to get Integers out of it, while another part of the code may mistakenly pass in a String, resulting in a runtime error.

### generic Box class
To update the Box class to use generics, you create a _generic type declaration_ by changing the code ```public class Box``` to ```public class Box<T>```. This introduces the type variable, T, that can be used anywhere inside the class.

With this change, the Box class becomes:
```java
/**
 * Generic version of the Box class.
 * @param <T> the type of the value being boxed
 */
public class Box<T> {
    // T stands for "Type"
    private T t;

    public void set(T t) { this.t = t; }
    public T get() { return t; }
}
```
As you can see, all occurrences of Object are replaced by T. To reference the generic Box class from within your code, you must perform a generic type invocation, which replaces T with some concrete value, such as Integer: ```Box<Integer> integerBox;```
  
**A type variable can be any non-primitive type you specify**: any class type, any interface type, any array type, or even another type variable. This same technique can be applied to create generic interfaces. **So, type variables can be instantiated only with reference types**. Primitive types: int, byte, char, float, double,.... are not allowed. Therefore the corresponding reference types are used.
```java
  Stiva<int> si=new Stiva<int>(); //error at compile-time
  Stiva<Integer> si=new Stiva<Integer>();
```
**Autoboxing**: automatic conversion of:
* a value of a primitive type to an object instance of a corresponding reference type when an object is expected, 
* and vice-versa when a primitive value is expected.
```java
Stiva<Integer> si=new Stiva<Integer>();
si.push(23); //autoboxing
si.push(new Integer(23));
int val=si.pop();
```
  
| primitive types | Correspondingreference types |
| -- | -- |
| boolean | Boolean |
| byte | Byte |
| short | Short |
| int | Integer |
| long | Long |
| float | Float |
| double | Double |
  
### Type Parameter Naming Conventions
By convention, type parameter names are single, uppercase letters. This stands in sharp contrast to the variable naming conventions that you already know about, and with good reason: Without this convention, **it would be difficult to tell the difference between a type variable and an ordinary class or interface name**.

The most commonly used type parameter names are:
* E - Element (used extensively by the Java Collections Framework)
* K - Key
* N - Number
* T - Type
* V - Value
* S,U,V etc. - 2nd, 3rd, 4th types
  
### Raw type
**A raw type is the name of a generic class or interface without any type arguments**. For example, given the generic Box class:
```java
public class Box<T> {
    public void set(T t) { /* ... */ }
    // ...
}
```

To create a parameterized type of ```Box<T>```, you supply an actual type argument for the formal type parameter T: <br>
```Box<Integer> intBox = new Box<>();```
  
If the actual type argument is omitted, you create a raw type of ```Box<T>```: <br>
```Box rawBox = new Box();```
  
Therefore, the raw type of the generic type ```Box<T>``` is Box and the raw type Box is the non-generic class ```Box<T>```. However, a non-generic class or interface type is not a raw type.
  
# Bounded Type Parameters
There may be times when you want to restrict the types that can be used as type arguments in a parameterized type. For example, a method that operates on numbers might only want to accept instances of Number or its subclasses. This is what bounded type parameters are for.

To declare a bounded type parameter, list the type parameter's name, followed by the **extends** keyword, followed by its upper bound, which in this example is Number. Note that, in this context, extends is used in a general sense to mean either "extends" (as in classes) or "implements" (as in interfaces).
```java
public class Box<T> {
    private T t;          

    public void set(T t) {
        this.t = t;
    }

    public T get() {
        return t;
    }

    public <U extends Number> void inspect(U u){
        System.out.println("T: " + t.getClass().getName());
        System.out.println("U: " + u.getClass().getName());
    }

    public static void main(String[] args) {
        Box<Integer> integerBox = new Box<Integer>();
        integerBox.set(new Integer(10));
        integerBox.inspect("some text"); // error: this is still String!
    }
}
```
By modifying our generic method to include this bounded type parameter, compilation will now fail, since our invocation of inspect still includes a String:
```
Box.java:21: <U>inspect(U) in Box<java.lang.Integer> cannot
  be applied to (java.lang.String)
                        integerBox.inspect("10");
                                  ^
1 error
```
The preceding example illustrates the use of a type parameter with a single bound, but a type parameter can have multiple bounds: ```<T extends B1 & B2 & B3>```

### Example
Bounded type parameters are key to the implementation of generic algorithms. Consider the following method that counts the number of elements in an array T[] that are greater than a specified element elem.
```java
public static <T> int countGreaterThan(T[] anArray, T elem) {
    int count = 0;
    for (T e : anArray)
        if (e > elem)  // compiler error
            ++count;
    return count;
}
```
The implementation of the method is straightforward, but it does not compile because the greater than operator (>) applies only to primitive types such as short, int, double, long, float, byte, and char. You cannot use the > operator to compare objects. To fix the problem, use a type parameter bounded by the `Comparable<T>` interface:
```java
public interface Comparable<T> {
    public int compareTo(T o);
}
// The resulting code will be:

public static <T extends Comparable<T>> int countGreaterThan(T[] anArray, T elem) {
    int count = 0;
    for (T e : anArray)
        if (e.compareTo(elem) > 0)
            ++count;
    return count;
}
```

# Wildcards
In generic code, **the question mark (?), called the wildcard, represents an unknown type**. The wildcard can be used in a variety of situations: as the type of a parameter, field, or local variable; sometimes as a return type (though it is better programming practice to be more specific). **The wildcard is never used as a type argument for a generic method invocation, a generic class instance creation, or a supertype.**

### Generics, Inheritance, and Subtypes
Consider the following method: <br>
```public void boxTest(Box<Number> n) { /* ... */ }```

What type of argument does it accept? By looking at its signature, you can see that it accepts a single argument whose type is `Box<Number>`. But what does that mean? Are you allowed to pass in `Box<Integer>` or `Box<Double>`, as you might expect? The answer is "no", because `Box<Integer>` and `Box<Double>` **are not subtypes** of `Box<Number>`.

This is a common misunderstanding when it comes to programming with generics, but it is an important concept to learn. `Box<Integer>` is not a subtype of `Box<Number>` even though Integer is a subtype of Number. For that we will use wildcards.

![](https://docs.oracle.com/javase/tutorial/figures/java/generics-subtypeRelationship.gif)
  
Note: **Given two concrete types A and B (for example, Number and Integer), `MyClass<A>` has no relationship to `MyClass<B>`, regardless of whether or not A and B are related. The common parent of `MyClass<A>` and `MyClass<B>` is Object.**

## Upper Bounded Wildcards
You can use an upper bounded wildcard to relax the restrictions on a variable. For example, say you want to write a method that works on `List<Integer>`, `List<Double>`, and `List<Number>`; you can achieve this by using an upper bounded wildcard.

**To declare an upper-bounded wildcard, use the wildcard character ('?'), followed by the extends keyword, followed by its upper bound**. Note that, in this context, extends is used in a general sense to mean either "extends" (as in classes) or "implements" (as in interfaces).

To write the method that works on lists of Number and the subtypes of Number, such as Integer, Double, and Float, you would specify `List<? extends Number>`. The term `List<Number>` is more restrictive than `List<? extends Number>` because the former matches a list of type Number only, whereas the latter matches a list of type Number or any of its subclasses.

```java
public static double sumOfList(List<? extends Number> list) {
    double s = 0.0;
    for (Number n : list)
        s += n.doubleValue();
    return s;
}
```

## Unbounded Wildcards
The unbounded wildcard type is specified using the wildcard character (?), for example, `List<?>`. This is called a list of unknown type. There are two scenarios where an unbounded wildcard is a useful approach:
* If you are writing a method that can be implemented using functionality provided in the Object class. (see example below)
* When the code is using methods in the generic class that don't depend on the type parameter. For example, List.size or List.clear. In fact, `Class<?>` is so often used because most of the methods in `Class<T>` do not depend on T.

Consider the following method, printList:
```java
public static void printList(List<Object> list) {
    for (Object elem : list)
        System.out.println(elem + " ");
    System.out.println();
}
```
  
The goal of printList is to print a list of any type, **but it fails to achieve that goal** — it prints only a list of Object instances; it cannot print `List<Integer>`, `List<String>`, `List<Double>`, and so on, because they are not subtypes of `List<Object>`. To write a generic printList method, use `List<?>`:

``` java
public static void printList(List<?> list) {
    for (Object elem: list)
        System.out.print(elem + " ");
    System.out.println();
}
```
Because for any concrete type A, `List<A>` is a subtype of `List<?>`, you can use printList to print a list of any type:
```java
List<Integer> li = Arrays.asList(1, 2, 3);
List<String>  ls = Arrays.asList("one", "two", "three");
printList(li);
printList(ls);
```

## Lower Bounded Wildcards
In a similar way, **a lower bounded wildcard restricts the unknown type to be a specific type or a super type of that type**.

A lower bounded wildcard is expressed using the wildcard character ('?'), following by the **super** keyword, followed by its lower bound: `<? super A>`.

**Note: You can specify an upper bound for a wildcard, or you can specify a lower bound, but you cannot specify both.**

**Example**: Say you want to write a method that puts Integer objects into a list. To maximize flexibility, you would like the method to work on `List<Integer>`, `List<Number>`, and `List<Object>` — anything that can hold Integer values.

To write the method that works on lists of Integer and the supertypes of Integer, such as Integer, Number, and Object, you would specify `List<? super Integer>`. The term `List<Integer>` is more restrictive than `List<? super Integer>` because the former matches a list of type Integer only, whereas the latter matches a list of any type that is a supertype of Integer.

The following code adds the numbers 1 through 10 to the end of a list:
```java
public static void addNumbers(List<? super Integer> list) {
    for (int i = 1; i <= 10; i++) {
        list.add(i);
    }
}
```

# Erasure
Java does not create a new class for each new instantiation of the type variables in case of the generic classes. The compiler erases all type variables and replaces them with their upper bounds (usually Object) and explicit casts are inserted when it is necessary. **Reason: backward compatibility with the non-generic Java versions**. The generic class is not recompiled for each new instantiation of the type variables like in C++.

Generics were introduced to the Java language to provide tighter type checks at compile time and to support generic programming. To implement generics, the Java compiler applies type erasure to:
* **Replace all type parameters in generic types with their bounds or Object if the type parameters are unbounded**. The produced bytecode, therefore, contains only ordinary classes, interfaces, and methods. (see Example1 and 2)
* Insert type casts if necessary to preserve type safety.
* Generate bridge methods to preserve polymorphism in extended generic types. (see Example3 and 4)
Type erasure ensures that no new classes are created for parameterized types; consequently, generics incur no runtime overhead.

## Erasure of Generic Types
During the type erasure process, the Java compiler erases all type parameters and replaces each with its first bound if the type parameter is bounded, or Object if the type parameter is unbounded.

### Example1
Consider the following generic class that represents a node in a singly linked list:
```java
public class Node<T> {

    private T data;
    private Node<T> next;

    public Node(T data, Node<T> next) {
        this.data = data;
        this.next = next;
    }

    public T getData() { return data; }
    // ...
}
```
Because the type parameter T is unbounded, the Java compiler replaces it with `Object`:
```java
public class Node {

    private Object data;
    private Node next;

    public Node(Object data, Node next) {
        this.data = data;
        this.next = next;
    }

    public Object getData() { return data; }
    // ...
}
```

### Example2
In the following example, the generic Node class uses a bounded type parameter:
```java
public class Node<T extends Comparable<T>> {

    private T data;
    private Node<T> next;

    public Node(T data, Node<T> next) {
        this.data = data;
        this.next = next;
    }

    public T getData() { return data; }
    // ...
}
```
The Java compiler replaces the bounded type parameter T with the first bound class, `Comparable`:
```java
public class Node {

    private Comparable data;
    private Node next;

    public Node(Comparable data, Node next) {
        this.data = data;
        this.next = next;
    }

    public Comparable getData() { return data; }
    // ...
}
```

## Erasure of Generic Methods
The Java compiler also erases type parameters in generic method arguments. 
### Example3
Consider the following generic method:
```java
// Counts the number of occurrences of elem in anArray.
//
public static <T> int count(T[] anArray, T elem) {
    int cnt = 0;
    for (T e : anArray)
        if (e.equals(elem))
            ++cnt;
        return cnt;
}
```
Because T is unbounded, the Java compiler replaces it with Object:
```java
public static int count(Object[] anArray, Object elem) {
    int cnt = 0;
    for (Object e : anArray)
        if (e.equals(elem))
            ++cnt;
        return cnt;
}
```
### Example4
Suppose the following classes are defined:
```java
class Shape { /* ... */ }
class Circle extends Shape { /* ... */ }
class Rectangle extends Shape { /* ... */ }
```
You can write a generic method to draw different shapes:
```java
public static <T extends Shape> void draw(T shape) { /* ... */ }
```
The Java compiler replaces T with Shape:
```java
public static void draw(Shape shape) { /* ... */ }
```

# Restrictions on Generics
To use Java generics effectively, you must consider the following restrictions:
* Cannot Instantiate Generic Types with Primitive Types
* Cannot Create Instances of Type Parameters
* Cannot Declare Static Fields Whose Types are Type Parameters
* Cannot Use Casts or instanceof With Parameterized Types
* Cannot Create Arrays of Parameterized Types
* Cannot Create, Catch, or Throw Objects of Parameterized Types
* Cannot Overload a Method Where the Formal Parameter Types of Each Overload Erase to the Same Raw Type

Read more [here](https://docs.oracle.com/javase/tutorial/java/generics/restrictions.html)
