---
layout: post
title: The handbook of programming languages
banner:
  image: https://user-images.githubusercontent.com/9413601/196836913-385eec05-6e38-4f91-adf4-c9a7365e4d87.png
  opacity: 0.76
author: Jeffrey Tse
categories: computer
tags:
  - computer
  - software
  - note
---

The historical development of programming languages has gone through one
stage after another, from machine language to high-level language, it is
also closer to the way of human thinking, easy to write, good readability,
and more efficient to develop.

- Machine-oriented programming (MOP)
- Procedure-oriented Programming (POP)
- Object-oriented Programming (OOP)
- ...

Programming itself is engineering, not science. This means that all roads
lead to Rome, and there is no one size fits all. So, in fact, many people
argue about them by different aspects (e.g. coding style, performance, the
difficulty of mastering), which language is the best, which framework is
better, these are actually philosophical questions, because there is no
unified standard answer.

![Difficulty of Mastering](https://user-images.githubusercontent.com/9413601/196746710-a3eaa742-4494-405b-b836-33236b212771.png)

Different programming languages have some similarities in common, but also
have their own uniqueness, they are all born to solve certain problems, no
one language is absolutely good, and they all have their own philosophical
ideas.

Languages:

- Ruby: Optimized for programmer happiness
- Python: Beautiful is better than ugly
- PHP: Quick and dirty
- Java: Compile once, run everywhere
- ...

## Categories

### Dynamically Typed Language

A language that checks the type of data at runtime. Such languages do not
assign a type to a variable, but get the data type when a value is assigned.

Languages:

- ECMAScript (JavaScript)
- Python
- Ruby
- PHP
- Erlang
- VBScript
- Swift
- Perl
- ...

### Statically Typed Language

Statically typed languages check the type at compile time before running.
When writing code, each variable declared must specify the type.

Languages:

- C/C++
- C#
- Object-C
- Java
- Scala
- Go
- ...

PS. Whether a language is dynamically typed or not is completely irrelevant
to whether the language is typesafe, don't tie them together.

### Dynamic Programing Language

Dynamic languages (Dynamic Programming Languages) are a class of languages
that can change their structure at runtime.

Languages:

- C#
- Object-C
- Python
- PHP
- Erlang
- JavaScript
- ...

### Static Programing Language

Static languages (Static Programming Languages) are languages whose structure
cannot be changed at runtime.

Languages:

- C/C++
- Java
- ...

### Strongly Typed Language

Strongly typed means that the type of a value doesn't change in unexpected
ways. A string containing only digits doesn't magically become a number, as
may happen in Perl. Every change of type requires an explicit conversion.

E.g. `1 / 3 = 0`, `int / int = int`

Languages:

- C/C++
- C#
- Object-C
- Java
- Python
- Ruby
- Go
- ...

### Weakly (Loosely) Typed Language

Weakly typed languages are looser in checking variable types and tolerate
implicit type conversions.

E.g.

- `1 / 3 = 0.33333...`, `int / int = float`
- `1 + "3" = 13`, `int / string = string`

Languages:

- JavaScript
  - Duck Typing (i.e. looks like a duck, talks like a duck, it's a duck)
- PHP
- ...

### Compiled Language

Compiled language means that a special compilation process is required before
the program is executed, and the program source file is compiled into a file
in machine language, which can be executed by the machine and has high
execution efficiency.

Languages:

- C/C++
- Object-C
- Pascal
- Swift
- ...

### Interpreted Language

Interpreted language means that the source code does not need to be compiled
in advance, at runtime, it must be interpreted before running.

Languages:

- JavaScript
- Python
- PHP
- Perl
- Ruby
- Erlang
- Java
- C#
- ...

For Java and C#, it can be said to be a semi-compiled and semi-interpreted
language. The source code needs to be converted into an intermediate file
(bytecode file), and then the intermediate file is taken to the virtual machine
for execution.

- [StackOverflow - Is Java a Compiled or an Interpreted programming language?](https://stackoverflow.com/questions/1326071/is-java-a-compiled-or-an-interpreted-programming-language)

## Basic

### Data Types

- Basic
  - Number
    - Byte
    - Short
    - Integer
    - Long
    - Float
    - Double
  - Character
  - String
  - Boolean
  - Null
  - Undefined
- Collection
  - Linear
    - List
    - Linked list
    - Tuple
    - Queue
    - Stack
  - Non-linear
    - Map

### Variable Lifecycle

- Static
- Dynamic

### Basic Structure

In structured programming, a program is written with only 3 basic structure:

- Sequences
- Selections
- Loops

### Functions

- Variadic function
- Default value
- Keyword arguments

## Programming Paradigms

### Functional Programming

FP is a high level way of programming, the level stands for the degree of
abstraction, the higher the programming level is, the least the concern of
machine execution details is, such as memory allocation and release, all
low level stuff just let the compiler to handle. And it is very worthwhile
to exchange a little performance for a clean program.

Behavior: Use imperative rather than declarative

- Imperative
  - Focus on the steps of execution (machine-oriented)
  - Examples
    - Assembly Language
- Declarative
  - Focus on the expression of execution (human-oriented)
    - `numbers.filter(num => num % 2)`
    - `SELECT name, age from Students`
  - Examples
    - SQL

Basic Concept:

- Pure Functions
  - It's actually a kind of functions
  - But it must meet certain restrictions
    - The same input always result the same output
    - No side effects (i.e. Closure)
    - How to handle the side effects
      - It's to use monad to push the impure part to the boundary of
        the program, and keep the core part pure
  - Try to make all functions pure as much as possible
  - Advantages
    - Its result is predictable
    - Make unit test very easy, as no any external dependency
- State Immutability
  - All variables can't be changed once they are declared.
- Avoid Loops
  - Recursion > Loops
  - Using recursion rather than explicit looping structure
  - The nature of the loop is actually very mutable

Languages:

- Haskell
- Erlang
- Scala
- ...

### Structured or modular programming

Languages:

- C#
- PHP
- ...

### Imperative programming

This alternative to OOP focuses on function rather than models.

Languages:

- C++
- Java
- ...

### Declarative programming

This programming method involves statements on what the task or desired
outcome is but not how to achieve it.

Languages:

- Prolog
- Lisp
- ...

### Logical programming

This programming method, which is based mostly in formal logic. It contains
a set of sentences that express facts or rules about a problem domain. It
focuses on tasks that can benefit from rule-based logical queries.

Languages:

- Prolog
- ...

### Object-oriented Programming (OOP)

Abstraction:

- Encapsulation
- Inheritance
  - Override (Type and quantity of parameters are the same)
  - Overload (Anyone of type and quantity of parameters is different)
- Polymorphism

Accessibility (Access modifier):

- Public
  - Access by any class
- Protected
  - Access by subclass
- Friendly
  - Access by friend's class (e.g. the same package)
- Private
  - Access by the class itself

Lifecycle:

- Construction
- Destruction

## Programming Model

In programming, the way of abstraction, organization or reuse of code. The
programming model is mainly methods and ideas.

- Event-driven (Publish/Subscribe Model)
  - Basic
    - Don't care about who is the receiver
  - Components
    - Event Queue
    - Event Mediator
    - Event Channel
    - Event Processor
  - Frameworks
    - select
    - poll
    - epoll
    - libev
    - interrupt system
- Message-driven
  - Basic
    - Care about who is the receiver
  - Framework
    - API Gateway
    - gRPC
    - Micro-service Architect
- Data-driven

## Advanced

### Iterator

### Generator

### Decorator

### Exception Handle

### Lambda

### Closure

### Asynchronous Programming

- .NET: delegate
- Java:
  - Anonymous inner class
  - Closure (Java 7)
- C++
  - tr1::function/bind (C++0X)
- ...

### Generics Programming

### Garbage Collection (GC)

### Higher-order Function (HOF)

### Dynamic Type conversion

### Meta Programming

- Introspection
  - JAVA: Reflection

### Serialization & Deserialization


## Language Characteristics

- Ruby
  - Block
  - Range
  - Symbols
- Java
  - Dynamic Proxy
- C#
  - LINQ
  - Extension Method

## How to choose a language?

- Whether the developer is familiar with a language.
- Which language provides more powerful features that can be applied to
  the current project.
- Focus on robustness or flexibility and expressiveness.
- Whether there are tools to improve development efficiency, such as
  peripheral frameworks (libraries), etc.
- ...

## References

- [Declarative programming](https://www.wikiwand.com/en/Declarative_programming)
- [The principal programming paradigms](https://www.info.ucl.ac.be/~pvr/paradigmsDIAGRAMeng108.pdf)
