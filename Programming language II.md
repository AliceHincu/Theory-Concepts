# Design & implementation
In computing, a **programming language specification** (or standard or definition) is a documentation artifact that defines a programming language so that users and 
implementors can agree on what programs in that language mean. Specifications are typically detailed and formal, and primarily used by implementors, with users referring to 
them in case of ambiguity; the C++ specification is frequently cited by users, for instance, due to the complexity. Related documentation includes a programming language 
reference, which is intended expressly for users, and a programming language rationale, which explains why the specification is written as it is; these are typically more 
informal than a specification.

A **programming language implementation** is a system for executing computer programs. There are two general approaches to programming language implementation: interpretation 
and compilation. Interpretation is a method of executing a program. The program is read as input by an interpreter, which performs the actions written in the program. 
Compilation is a different process, where a compiler reads in a program, but instead of running the program, the compiler translates it into some other language, such as 
bytecode or machine code. The translated code may either be directly executed by hardware, or serve as input to another interpreter or another compiler.

# Programming paradigms
**Programming paradigms** are a way to classify programming languages based on their features. Languages can be classified into multiple paradigms.

Some paradigms are concerned mainly with implications for the execution model of the language, such as allowing side effects, or whether the sequence of operations is defined 
by the execution model. Other paradigms are concerned mainly with the way that code is organized, such as grouping a code into units along with the state that is modified by 
the code. Yet others are concerned mainly with the style of syntax and grammar.

Common programming paradigms include:

<ul>
  <li> <strong>imperative</strong> in which the programmer instructs the machine how to change its state(you describe the algorithm step-by-step, at various degrees of abstraction)
    <ul>
      <li><strong>procedural</strong> which groups instructions into procedures,</li>
      <li><strong>object-oriented</strong> which groups instructions with the part of the state they operate on,</li>
    </ul>
  </li>
  <li><strong>declarative</strong> in which the programmer merely declares properties of the desired result, but not how to compute it(In the declarative programming paradigm, you describe a result or a goal, and you get it via a "black box". The opposite of imperative)
    <ul>
      <li><strong>functional</strong> in which the desired result is declared as the value of a series of function applications,</li>
      <li><strong>logic</strong> in which the desired result is declared as the answer to a question about a system of facts and rules,</li>
      <li><strong>mathematical</strong> in which the desired result is declared as the solution of an optimization problem</li>
      <li><strong>reactive</strong> in which the desired result is declared with data streams and the propagation of change</li>
    </ul>
  </li>
</ul>

## Types of programming languages 

### Assembly languages

Assembly languages directly correspond to a machine language (see below), although there may not be a 1-1 mapping between an individual statement and an individual instruction, 
so machine code instructions appear in a form understandable by humans. Assembly languages let programmers use symbolic addresses, which the assembler converts to absolute or 
relocatable addresses. Most assemblers also support macros and symbolic constants.

### Compiled languages

A compiled language is a programming language whose implementations are typically compilers (translators that generate machine code from source code), and not interpreters 
(step-by-step executors of source code, where no pre-runtime translation takes place). Programs compiled into native code at compile time tend to be faster than those 
translated at runtime due to the translation process's overhead. 

Examples: C, C++, Java, Kotlin, Rust, Swift

### Data-oriented languages

Data-oriented languages provide powerful ways of searching and manipulating the relations that have been described as entity relationship tables which map one set of things 
into other sets.

Examples: SQL

### Embeddable languages

**Source embeddable** languages embed small pieces of executable code inside a piece of free-form text, often a web page. \
**Client-side embedded** languages are limited by the abilities of the browser or intended client. They aim to provide dynamism to web pages without the need to recontact the 
server.  (Example: JavaScript) \
**Server-side embedded** languages are much more flexible, since almost any language can be built into a server. The aim of having fragments of server-side code embedded in a 
web page is to generate additional markup dynamically; the code itself disappears when the page is served, to be replaced by its output. languages are limited by the abilities 
of the browser or intended client. They aim to provide dynamism to web pages without the need to recontact the server.  (Example: PHP)

### Garbage collected languages
Garbage Collection (GC) is a form of automatic memory management. The garbage collector attempts to reclaim memory that was allocated by the program but is no longer used.

Example: Java, Python, Kotlin

### Machine languages
Machine languages are directly executable by a computer's CPU. They are typically formulated as bit patterns, usually represented in octal or hexadecimal. Each bit pattern 
causes the circuits in the CPU to execute one of the fundamental operations of the hardware. The activation of specific electrical inputs (e.g., CPU package pins for 
microprocessors), and logical settings for CPU state values, control the processor's computation. 

### Object-oriented class-based languages
Class-based Object-oriented programming languages support objects defined by their class. Class definitions include member data. Message passing is a key concept (if not 
the key concept) in Object-oriented languages.

### Procedural languages
Procedural programming languages are based on the concept of the unit and scope (the data viewing range) of an executable code statement. A procedural program is composed 
of one or more units or modules, either user coded or provided in a code library; each module is composed of one or more procedures, also called a function, routine, 
subroutine, or method, depending on the language. 

[More types here](https://en.wikipedia.org/wiki/List_of_programming_languages_by_type)

## Integrated development environment
An integrated development environment (IDE) is a software application that provides comprehensive facilities to computer programmers for software development. An IDE 
normally consists of at least a source code editor, build automation tools and a debugger. Some IDEs, such as NetBeans and Eclipse, contain the necessary compiler, 
interpreter, or both; others, such as SharpDevelop and Lazarus, do not.
