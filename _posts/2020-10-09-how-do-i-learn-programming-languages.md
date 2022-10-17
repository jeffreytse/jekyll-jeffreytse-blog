---
layout: post
title: How do I Learn Programming Languages
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

Programming itself is engineering, not science. This means that all roads
lead to Rome, and there is no one size fits all. So, in fact, many people
argue about them by different aspects, from coding style to performance,
which language is the best, which framework is better, these are actually
philosophical questions, because there is no unified standard answer.

Different programming languages have some similarities in common, but also
have their own uniqueness, they are all born to solve certain problems, no
one language is absolutely good, and they all have their own philosophical
ideas.

- Ruby: Optimized for programmer happiness
- Python: Beautiful is better than ugly
- PHP: Quick and dirty
- Java: Compile once, run everywhere
- ...

## Categories

### Dynamically Typed Language

A language that checks the type of data at runtime. Such languages do not
assign a type to a variable, but get the data type when a value is assigned.

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

- C/C++
- Java
- ...

### Strongly Typed Language

A strongly typed language is a language that enforces the definition of data
types. That is to say, once a variable is assigned a data type, if it is not
casted, it will always be this data type.

Typical of strongly typed languages, they don't handle an operation that
clearly contradicts the type definition, but instead flag it as a problem and
throw it as an error.

E.g. `1 / 3 = 0`, `int / int = int`

- C/C++
- C#
- Object-C
- Java
- Python
- Ruby
- ...

### Weakly (Loosely) Typed Language

Weakly typed languages are looser in checking variable types and tolerate
implicit type conversions.

E.g. `1 / 3 = 0.33333...`, `int / int = float`

- JavaScript
  - Duck Typing (i.e. looks like a duck, talks like a duck, it's a duck)
- PHP
- ...

### Compiled Language

Compiled language means that a special compilation process is required before
the program is executed, and the program source file is compiled into a file
in machine language, which can be executed by the machine and has high
execution efficiency.

- C/C++
- Object-C
- Pascal
- Swift
- ...

### Interpreted Language

Interpreted language means that the source code does not need to be compiled
in advance, at runtime, it must be interpreted before running.

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

### Tree Basic Structure

- Sequences
- Selections
- Loops

## Object-oriented Programming (OOP)

Abstraction:

- Encapsulation
- Inheritance
- Polymorphism

Accessibility:

## Advanced

### Generics Programming

### Lambda

### Garbage Collection (GC)

### Closure

### Higher-order Function (HOF)

### Dynamic Type conversion

### Meta Programming

