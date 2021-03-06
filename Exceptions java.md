# Exceptions
**An exception is an unexpected event that occurred during the execution of a program, and disrupts the normal flow of instructions**. The program/Application terminates abnormally, which is not recommended, therefore, these exceptions are to be handled

An exception can occur for many different reasons. Following are some scenarios where an exception occurs:
* A user has entered an invalid data. (**caused by user error**)
* A file that needs to be opened cannot be found. (**caused by programmer error**)
* A network connection has been lost in the middle of communications or the JVM has run out of memory. (**caused by physical resources that have failed in some manner**)

Based on these, we have three categories of Exceptions. You need to understand them to know how exception handling works in Java.
* **Checked exceptions** − A checked exception is an exception that **is checked (notified) by the compiler at compilation-time**, these are also called as **compile time exceptions**. These exceptions cannot simply be ignored, the programmer should take care of (handle) these exceptions.
* **Unchecked exceptions** − An unchecked exception is an exception that occurs at the time of execution. These are also called as Runtime Exceptions. These include programming bugs, such as logic errors or improper use of an API. Runtime exceptions are ignored at the time of compilation.
* **Errors** − These are not exceptions at all, but problems that arise beyond the control of the user or the programmer. Errors are typically ignored in your code because you can rarely do anything about an error. For example, if a stack overflow occurs, an error will arise. They are also ignored at the time of compilation.

## Checked exception example
For example, if you use FileReader class in your program to read data from a file, if the file specified in its constructor doesn't exist, then a **FileNotFoundException** occurs, and the compiler prompts the programmer to handle the exception.

``` java
import java.io.File;
import java.io.FileReader;

public class FilenotFound_Demo {

   public static void main(String args[]) {		
      File file = new File("E://file.txt");
      FileReader fr = new FileReader(file); 
   }
}
```
If you try to compile the above program, you will get the following exceptions.
```
C:\>javac FilenotFound_Demo.java
FilenotFound_Demo.java:8: error: unreported exception FileNotFoundException; must be caught or declared to be thrown
      FileReader fr = new FileReader(file);
                      ^
1 error
```
Note − Since the methods read() and close() of FileReader class throws IOException, you can observe that the compiler notifies to handle IOException, along with FileNotFoundException.

## Unchecked exception example
For example, if you have declared an array of size 5 in your program, and trying to call the 6th element of the array then an **ArrayIndexOutOfBoundsExceptionexception** occurs.

```java
public class Unchecked_Demo {
   
   public static void main(String args[]) {
      int num[] = {1, 2, 3, 4};
      System.out.println(num[5]);
   }
}
```
If you compile and execute the above program, you will get the following exception.
```
Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 5
	at Exceptions.Unchecked_Demo.main(Unchecked_Demo.java:8)
```

# Exception Hierarchy
All exception classes are subtypes of the java.lang.Exception class. The exception class is a subclass of the Throwable class. Other than the exception class there is another subclass called Error which is derived from the Throwable class.

Errors are abnormal conditions that happen in case of severe failures, these are not handled by the Java programs. Errors are generated to indicate errors generated by the runtime environment. Example: JVM is out of memory. Normally, programs cannot recover from errors.

The Exception class has two main subclasses: IOException class and RuntimeException Class.

![](https://www.tutorialspoint.com/java/images/exceptions1.jpg)

# Catching Exceptions
A method catches an exception using a combination of the try and catch keywords. A try/catch block is placed around the code that might generate an exception. Code within a try/catch block is referred to as protected code, and the syntax for using try/catch looks like the following 

```java 
try {
   // Protected code
} catch (ExceptionName e1) {
   // Catch block
}
```
Execution Flow:
* If an abnormal situation occurs in the block try(), JVM creates an exception object and throws it to the block catch.
* If no abnormal situation occurs, try block normally executes.
* If the exception object is compatible with one of the exceptions of the catch blocks then that catch block executes

The code which is prone to exceptions is placed in the try block. When an exception occurs, that exception is handled by the catch block associated with it. Every try block should be immediately followed either by a catch block or a finally block. A catch statement involves declaring the type of exception you are trying to catch. 

A try block can be followed by multiple catch blocks. The syntax for multiple catch blocks looks like the following −

```java
try {
   // Protected code
} catch (ExceptionType1 e1) {
   // Catch block
} catch (ExceptionType2 e2) {
   // Catch block
} catch (ExceptionType3 e3) {
   // Catch block
}
```
The previous statements demonstrate three catch blocks, but you can have any number of them after a single try. If an exception occurs in the protected code, the exception is thrown to the first catch block in the list. If the data type of the exception thrown matches ExceptionType1, it gets caught there. If not, the exception passes down to the second catch statement. This continues until the exception either is caught or falls through all catches, in which case the current method stops execution and the exception is thrown down to the previous method on the call stack.

Since Java 7, you can handle more than one exception using a single catch block, this feature simplifies the code. Here is how you would do it 
```java
catch (IOException|FileNotFoundException ex) {
   logger.log(ex);
   throw ex;
  ```
  
# The Throws/Throw Keywords
If a method does not handle a checked exception, the method must declare it using the **throws** keyword. The throws keyword appears at the end of a method's signature.

You can throw an exception, either a newly instantiated one or an exception that you just caught, by using the **throw** keyword.

```java
import java.io.*;
public class className {
   // throws is used to postpone the handling of a checked exception and throw is used to invoke an exception explicitly.
   public void deposit(double amount) throws RemoteException {
      // Method implementation
      throw new RemoteException();
   }
   // Remainder of class definition
}
```

# The Finally Block
The finally block follows a try block or a catch block. A finally block of code always executes, irrespective of occurrence of an Exception. Using a finally block allows you to run any cleanup-type statements that you want to execute, no matter what happens in the protected code.

A finally block appears at the end of the catch blocks and has the following syntax:
``` java
try {
   // Protected code
} catch (ExceptionType1 e1) {
   // Catch block
} catch (ExceptionType2 e2) {
   // Catch block
} catch (ExceptionType3 e3) {
   // Catch block
}finally {
   // The finally block always executes.
}
```

# The try-with-resources
Generally, when we use any resources like streams, connections, etc. we have to close them explicitly using finally block.  **try-with-resources**, also referred as automatic resource management, is a new exception handling mechanism that was introduced in Java 7, which automatically closes the resources used within the try catch block. To use this statement, you simply need to declare the required resources within the parenthesis, and the created resource will be closed automatically at the end of the block.

Following points are to be kept in mind while working with try-with-resources statement:
* To use a class with try-with-resources statement it should implement **AutoCloseable interface** and the **close() method** of it gets invoked automatically at runtime.
* You can declare more than one class in try-with-resources statement.
* While you declare multiple classes in the try block of try-with-resources statement these classes are closed in reverse order.
* Except the declaration of resources within the parenthesis everything is the same as normal try/catch block of a try block.
* The resource declared in try gets instantiated just before the start of the try-block.
* The resource declared at the try block is implicitly declared as final.

# User-defined Exceptions
You can create your own exceptions in Java. Keep the following points in mind when writing your own exception classes −
* All exceptions must be a child of Throwable.
* If you want to write a checked exception that is automatically enforced by the Handle or Declare Rule, you need to extend the Exception class.
* If you want to write a runtime exception, you need to extend the RuntimeException class.

We can define our own Exception class as below −
```java
class MyException extends Exception {
//code
}
```

Read more about exceptions in java: [1](https://www.tutorialspoint.com/java/java_exceptions.htm)
