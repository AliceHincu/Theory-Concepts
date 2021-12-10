Typecasting is one of the most important concepts which basically deals with the conversion of one data type to another datatype implicitly or explicitly

# Primitive conversions
| Datatype | Bits Acquired In Memory |
| ---      | ---                     |
| boolean	 | 1                       |
| byte	   | 8 (1 byte)              |
| char	   | 16 (2 bytes)            | 
| short	   | 16(2 bytes)             |
| int	     | 32 (4 bytes)            |
| long	   | 64 (8 bytes)            |
| float	   | 32 (4 bytes)            |
| double	 | 64 (8 bytes)            |

In Java, there are two types of casting:

### Widening Casting (automatically)
Widening Casting (largire) - **converting a smaller type to a larger type size** <br>
`byte` -> `short` -> `char` -> `int` -> `long` -> `float` -> `double`
``` java
public class Main {
  public static void main(String[] args) {
    int myInt = 9;
    double myDouble = myInt; // **Automatic casting: int to double**

    System.out.println(myInt);      // Outputs 9
    System.out.println(myDouble);   // Outputs 9.0
  }
}
```

### Narrowing Casting (manually)
Narrowing Casting (ingustare) - **converting a larger type to a smaller size type** <br>
`double` -> `float` -> `long` -> `int` -> `char` -> `short` -> `byte`
``` java
public class Main {
  public static void main(String[] args) {
    double myDouble = 9.78d;
    int myInt = (int) myDouble; // Manual casting: double to int

    System.out.println(myDouble);   // Outputs 9.78
    System.out.println(myInt);      // Outputs 9
  }
}
```

# Reference variable casting
Although primitive conversions and reference variable casting may look similar, they're quite different concepts. In both cases, we're “turning” one type into another. But, in a simplified way, a primitive variable contains its value, and **conversion of a primitive variable means irreversible changes in its value.**  After the conversion in the below example, myInt variable is 1, and we can’t restore the previous value 1.1 from it.

``` java
double myDouble = 1.1;
int myInt = (int) myDouble;
        
assertNotEquals(myDouble, myInt);
```

Reference variables are different:
* **the reference variable only refers to an object but doesn’t contain the object itself**.
* casting a reference variable **doesn’t touch the object it refers to, but only labels this object in another way**, expanding or narrowing opportunities to work with it. 

Just like the data types, the objects can also be typecasted. However, in objects, there are only two types of objects, i.e. parent object and child object. There are two types of typecasting. They are: 
* Upcasting 
  * **child to parent**: the typecasting of a child object to a parent object. 
  * it can be done **implicitly**. 
  * **narrows the list** of methods and properties available to this object. Upcasting gives us the flexibility to access the parent class members but it is not possible to access all the child class members using this feature. Instead of all the members, we can access some specified members of the child class. For instance, we can access the overridden methods.
* Downcasting 
  * **parent to child**: the typecasting of a parent object to a child object. 
  * It cannot be implicit. 
  * **extends the list** of methods and properties available to this object.

**Example**: Let there be a parent class. There can be many children of a parent. Let’s take one of the children into consideration. The child inherits the properties of the parent. Therefore, there is an “is-a” relationship between the child and parent(Cat is an animal). Therefore, the child can be implicitly upcasted to the parent. However, a parent may or may not inherits the child’s properties(An animal can be a cat but it's not only a cat). However, we can forcefully cast a parent to a child which is known as downcasting. After we define this type of casting explicitly, the compiler checks in the background if this type of casting is possible or not. If it’s not possible, the compiler throws a ClassCastException. 

## Upcasting
**Casting from a subclass to a superclass is called upcasting**. Typically, the upcasting is implicitly **performed by the compiler**.

``` java
// To demonstrate upcasting, let’s define an Animal class:

public class Animal {

    public void eat() {
        // ... 
    }
}

//Now let’s extend Animal:

public class Cat extends Animal {

    public void eat() {
         // ... 
    }

    public void meow() {
         // ... 
    }
}
```

Now we can create an object of Cat class and assign it to the reference variable of type Cat: <br>
``` java
Cat cat = new Cat(); 
```
And we can also assign it to the reference variable of type Animal:
``` java
Animal animal = cat;
```
**In the above assignment, implicit upcasting takes place.**


We could do it explicitly: ```animal = (Animal) cat;``` But there is no need to do explicit cast up the inheritance tree. The compiler knows that cat is an Animal and doesn’t display any errors.

**Using upcasting, we’ve restricted the number of methods available** to Cat instance but haven't changed the instance itself. Now **we can’t do anything that is specific to Cat** — we can’t invoke meow() on the animal variable, calling meow() would cause the compiler error: ```// animal.meow(); The method meow() is undefined for the type Animal```

Thanks to upcasting, we can take advantage of polymorphism.

## Polymorphism
Let’s define another subclass of Animal, a Dog class:
``` java
public class Dog extends Animal {

    public void eat() {
         // ... 
    }
}

// Now we can define the feed() method, which treats all cats and dogs like animals:

public class AnimalFeeder {

    public void feed(List<Animal> animals) {
        animals.forEach(animal -> {
            animal.eat();
        });
    }
}
```
We don’t want AnimalFeeder to care about which animal is on the list — a Cat or a Dog. In the feed() method they are all animals.

**Implicit upcasting occurs when we add objects of a specific type to the animals list:**
``` java
List<Animal> animals = new ArrayList<>();
animals.add(new Cat());
animals.add(new Dog());
new AnimalFeeder().feed(animals);
// We add cats and dogs, and they are upcast to Animal type implicitly. Each Cat is an Animal and each Dog is an Animal. They're polymorphic.
```


**Upcasting to an interface is also common.**

We can create Meow interface and make Cat implement it:
``` java
public interface Meow {
    public void meow();
}

public class Cat extends Animal implements Meow {
    @overriden
    public void eat() {
         // ... 
    }

    public void meow() {
         // ... 
    }
}
```
Now any Cat object can also be upcast to Mew: ```Meow meow = new Cat(); // Cat is a Meow; upcasting is legal and done implicitly.``` Therefore, Cat is a Meow, Animal, Object and Cat. It can be assigned to reference variables of all four types in our example.

## Overriding
In the example above, the eat() method is overridden. This means that although eat() is called on the variable of the Animal type, the work is done by methods invoked on real objects — cats and dogs:

``` java
public void feed(List<Animal> animals) {
    animals.forEach(animal -> {
        animal.eat();
    });
}
```
If we add some logging to our classes, we'll see that Cat and Dog methods are called:
```
web - 2018-02-15 22:48:49,354 [main] INFO com.baeldung.casting.Cat - cat is eating
web - 2018-02-15 22:48:49,363 [main] INFO com.baeldung.casting.Dog - dog is eating
```

## Downcasting
What if we want to use the variable of type Animal to invoke a method available only to Cat class? Here comes the downcasting. 
**It’s the casting from a superclass to a subclass.**

Let’s look at an example:

``` java
Animal animal = new Cat();
```

We know that animal variable refers to the instance of Cat. And we want to invoke Cat’s meow() method on the animal. But the compiler complains that meow() method doesn’t exist for the type Animal.

To call meow() we should downcast animal to Cat:

``` java
((Cat) animal).meow();
```
The inner parentheses and the type they contain are sometimes called **the cast operator**. Note that external parentheses are also needed to compile the code.

Let’s rewrite the previous AnimalFeeder example with meow() method:

``` java
public class AnimalFeeder {

    public void feed(List<Animal> animals) {
        animals.forEach(animal -> {
            animal.eat();
            if (animal instanceof Cat) {
                ((Cat) animal).meow();
            }
        });
    }
}
```
Now we gain access to all methods available to Cat class. Look at the log to make sure that meow() is actually called:
```
web - 2018-02-16 18:13:45,445 [main] INFO com.baeldung.casting.Cat - cat is eating
web - 2018-02-16 18:13:45,454 [main] INFO com.baeldung.casting.Cat - meow
web - 2018-02-16 18:13:45,455 [main] INFO com.baeldung.casting.Dog - dog is eating
```
Note that in the above example we're trying to downcast only those objects that are really instances of Cat. To do this, we use the operator instanceof.
