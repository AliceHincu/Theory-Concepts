# GRASP
**General Responsibility Assignment Software Patterns** (or Principles), abbreviated GRASP, is a set of "nine fundamental principles in object design and responsibility 
assignment". The different patterns and principles used in GRASP are controller, creator, indirection, information expert, low coupling, high cohesion, polymorphism, 
protected variations, and pure fabrication. All these patterns solve some software problem common to many software development projects. These techniques have not been 
invented to create new ways of working, but to better document and standardize old, tried-and-tested programming principles in object-oriented design.

##  High Cohesion
**Main idea**: Create functions, classes and modules so that they have a single, well defned responsibility. 

High Cohesion - attempts to keep objects focused, manageable and understandable. High cohesion means that the responsibilities of a given element are strongly related and 
highly focused. Low cohesion is a situation in which an element has too many unrelated responsibilities. Elements with low cohesion often suffer from being hard to 
comprehend, hard to reuse, hard to maintain and adverse to change. 

High cohesion is an evaluative pattern that attempts to keep objects appropriately focused, manageable and understandable. High cohesion is generally used in support of low 
coupling. High cohesion means that the responsibilities of a given element are strongly related and highly focused. Breaking programs into classes and subsystems is an example 
of activities that increase the cohesive properties of a system. Alternatively, low cohesion is a situation in which a given element has too many unrelated responsibilities. 
Elements with low cohesion often suffer from being hard to comprehend, reuse, maintain and change.

## Low Coupling
**Main idea**: Minimize the dependencies between functions, classes and modules. A function call is a good example of a dependency.

Coupling is a measure of how strongly one element is connected to, has knowledge of, or relies on other elements. Low coupling is an evaluative pattern that dictates how to 
assign responsibilities for the following benefits:
<ul>
  <li>lower dependency between the classes</li>
  <li>change in one class having a lower impact on other classes</li>
  <li>higher reuse potential</li>
</ul>

Forms of coupling:
<ul>
  <li><strong>TypeX</strong> has an attribute (field) that refers to a <strong>TypeY</strong> instance, or <strong>TypeY</strong> itself.</li>
  <li><strong>TypeX</strong> has a method which references an instance of <strong>TypeY</strong>, or <strong>TypeY</strong> itself, by any means. (parameter, local variable, 
    return value, method invocation) </li>
  <li><strong>TypeX</strong> is a direct or indirect subclass of <strong>TypeY</strong>.</li>
</ul>

## Information Expert
**Main idea**:How do I decide where the code for a functionality goes.
Information expert (also expert or the expert principle) is a principle used to determine where to delegate responsibilities such as methods, computed fields, and so on.

Using the principle of information expert, a general approach to assigning responsibilities is to look at a given responsibility, determine the information needed to fulfill 
it, and then determine where that information is stored. This will lead to placing the responsibility on the class with the most information required to fulfill it.

## Controller
**Main idea**: Create a class that has a method for each user action. The first layer below the UI, its job is to control how the application fulfills required 
functionalities.

The controller pattern assigns the responsibility of dealing with system events to a non-UI class that represents the overall system or a use case scenario. A controller 
object is a non-user interface object responsible for receiving or handling a system event.

Problem: Who should be responsible for handling an input system event? \
Solution: A use case controller should be used to deal with all system events of a use case, and may be used for more than one use case. For instance, for the use cases 
Create User and Delete User, one can have a single class called UserController, instead of two separate use case controllers.

<ul>
  <li>Decouple the event sources (usually the application UI) from the objects that actually handle the events. </li>
  <li>It is the first object beyond the UI layer that receives and controls system operation. </li>
  <li>The controller should delegate to other objects the work that needs to be done </li>
</ul>

## Protected variations
**Main idea**:Create a class where I can control allowed object variations.

The protected variations pattern protects elements from the variations on other elements (objects, systems, subsystems) by wrapping the focus of instability with an interface 
and using polymorphism to create various implementations of this interface.

<ul>
  <li>Make sure current or future variations in the system do not cause major problems with system operation</li>
  <li>Create new classes to encapsulate such variations</li>
  <li>The protect variation pattern protects elements from the variations on other elements (objects, systems, subsystems) by wrapping the focus of instability to a separate 
    class. </li>
</ul>

## Creator
**Main idea**:How to decide who is responsible for creating domain entity objects.

The creation of objects is one of the most common activities in an object-oriented system. Which class is responsible for creating objects is a fundamental property of 
the relationship between objects of particular classes.

Problem: Who creates object A?
Solution: In general, Assign class B the responsibility to create object A if one, or preferably more, of the following apply:
<ul>
  <li>Instances of B contain or compositely aggregate instances of A</li>
  <li>Instances of B record instances of A</li>
  <li>Instances of B closely use instances of A</li>
  <li>Instances of B have the initializing information for instances of A and pass it on creation</li>
</ul>

## Pure fabrication
**Main idea**: Create a class that represents a persistent object store .

A pure fabrication is a class that does not represent a concept in the problem domain, specially made up to achieve low coupling, high cohesion, and the reuse potential 
thereof derived (when a solution presented by the information expert pattern does not).


# GRASP in Layered Architecture
| Layer | Main ideas |
| -- | -- |
| All | **High cohesion** (each layer, class has a single, well-defined responsibility), **low coupling** (dependencies between layers and their classes are reduced and made clear) |
| User-Interface | "Thin", contains as little functionality as possible |
| Controller | Application logic, the GRASP controller, uses the **creator** pattern |
| Domain | Entities from program domain |
| Validators | **Protect variation**, separate into its own class |
| Repository | **Pure fabrication**, responsible for storing domain entity objects |

