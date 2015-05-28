---
layout: post
title: Java Notes (3) - Class & Interface & Modifiers
---
Course: [Java Programming (Coursera)](https://class.coursera.org/pkujava-001)  
Instructor: [Dashi Tang](https://www.coursera.org/instructor/~3838), [Peking University](http://english.pku.edu.cn/)

## Class
* Field (variable) + Method (function)
    * Constructor
       * No return type!
       * If not defined, system will generate a default constructor.
    * Overload - _Polymorphism_
       * Functions with different signatures can be recognized when compling.
        * Signature: # and type of variables.
    * "this"
        * Tell the difference from fields and local variables.
    
        ```java
       Person (int age, string name){
           this.age = age;
           this.name = name;
       }
       ```
    
       * In a constructor, call another constructor. **MUST put at first!**
    
       ```java
       Person(){
            this(0, "");
            ...
        }
       ```
       
* Inheritance
    * Subclass & Superclass
       * A subclass could have only one direct superclass.
       * Subclasses could modify and add fields & methods of their superclasses.
    * "extends"
       * All classes inherit from java.lang.**Object**
       
       ```java
       class Student extends Person {     //A Student "is a" Person
            ...
      }
      ```
      
    * Field
       * Inherite & Re-define (Hide) & Add
    * Method
       * Inherite
       * **@Override** (Modify)
          * Re-define a method with same name and signature in the superclass.
       * Add
       * Overload
          * Define a method with same name and different signature in the superclass.
          * Acually a **NEW** fuction.
    * "super"
       * Access fields and methods in the superclass
       * Override and use the superclass
       
       ``` java
       void sayHello(){
            super.sayHello();
            ...
       }
       ```
       
       * Call the supre class's constructor
       
       ```java
       Student(String name, int age, String school){
            super(name, age);    //MUST put at first!
            this.school = school;
       }
       ```
    * Casting

## Package
* Classes in the same package could access each other.

## Modifiers
## Interface