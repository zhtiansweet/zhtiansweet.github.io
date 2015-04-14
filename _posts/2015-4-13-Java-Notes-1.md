---
layout: post
title: Java Programming Notes (1) - Introduction to Java and OOP
---

Course: [Java Programming (coursera.com)](https://class.coursera.org/pkujava-001)  
Instructor: [Dashi Tang](https://www.coursera.org/instructor/~3838), [Peking University](http://english.pku.edu.cn/)

###Java History
* Born in 1995 by James Gosling, SUN.
* Platforms:
 * Java SE: J2SE, Standard Edition.
 * Java EE: J2EE, Enterprise Edition.
 * Java ME: J2ME, Micro Edition

###What is Java
* Simple, OOP, cross-platform, secure, muti-threads.
* "**C++--**":
 * No pointers, automatical memory control, stable data types, no header files, no macros, no multiple inheritance, no global variables other than classes...

###Java Mechanism
1. JVM (Java Virtual Machine)
 * source.java --_compile (javac)_--> source.class (bytecode) --_run_--> JVM for different platforms
 * JRE = JVM + API (lib)
   1. load codes (by _class loader_)
    2. check codes (by _bytecode verifier_)
    3. run codes (by _runtime interpreter_)  
2. Code Security  
3. Garbage Collection  
4. JDK (Java Development Kit) = JRE + Tools  

###Object-Oriented Programming
*  **Class** is an abstract of objects, **Object** is an instance of class.
 * Class = Field + Method
* Features:
  1. **Encapsulation**
     * Pack data and functions into a class.
     * Allow selective hiding of properties and methods in an object.
  2. **Inheritance**
     * Parent class and child class could share data and methods.
     * e.g.
     ```java
     //Parent Class
     class Person{
         int age;
         String name;
         void sayHello(){...}
     }
     
     //Child Class
     class Student extends Person{
         String school;
         double score;
         void meetTeacher(){...}
     }
     ```
  3. **Polymorphism**
     *Implementing the same fuction on different objects may generate different results.
     * e.g.
     ```java
     foo(Person p){p.sayHello();}
     foo(new Student());
     foo(new Teacher());
     //Different results!
     ```
