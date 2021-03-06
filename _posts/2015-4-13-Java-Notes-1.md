---
layout: post
title: Java Notes (1) - Introduction to Java & OOP
---

Course: [Java Programming (Coursera)](https://class.coursera.org/pkujava-001)  
Instructor: [Dashi Tang](https://www.coursera.org/instructor/~3838), [Peking University](http://english.pku.edu.cn/)

###Java History
* Born in 1995 by James Gosling, SUN.
* Platforms:
 * Java SE: J2SE, Standard Edition.
 * Java EE: J2EE, Enterprise Edition.
 * Java ME: J2ME, Micro Edition.

###What is Java
* Simple, OOP, cross-platform, secure, muti-threads.
* "**C++--**":
 * No pointers, automatical memory control, stable data types, no header files, no macros, no multiple inheritance, no global variables other than classes...

###Java Mechanism
* **JVM (Java Virtual Machine)**
 * source.java --_compile (javac)_--> source.class (bytecode) --_run_--> JVM for different platforms
* JRE = JVM + API (lib)
 * Load code (by _class loader_).
 * Check code (by _bytecode verifier_).
 * Run code (by _runtime interpreter_). 
* **Code Security**  
* **Garbage Collection**  
* JDK (Java Development Kit) = JRE + Tools  

###Object-Oriented Programming
*  **Class** is an abstract of objects, **Object** is an instance of class.
 * Class = Field + Method
* Features:
   * **Encapsulation**
     * Pack data and functions into a class.
     * Allow selective hiding of properties and methods in an object.
   * **Inheritance**
     * Superclass and subclass could share data and methods.
     * e.g.  

     ```java 
     //Superclass
     class Person{
         int age;
         String name;
         void sayHello(){...}
     }
     
     //Subclass
     class Student extends Person{
         String school;
         double score;
         void meetTeacher(){...}
     }  
     ```
   * **Polymorphism**
     * Implementing the same fuction on different objects may generate different results.
     * e.g.
     
     ```java
     foo(Person p){p.sayHello();}
     foo(new Student());
     foo(new Teacher());
     //Different results!  
     ```
