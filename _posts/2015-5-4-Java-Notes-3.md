---
layout: post
title: Java Notes (3) - Class & Interface & Modifier
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
Access Modifier: **public, private, protected**  
Other Modifier: **abstract, static, final**  

Modifiers could modify classes and members (fields & methods) in classes

### Access Modifiers
* Modify Fields & Methods  

    * Accessibility:

    |  | Within Class | Within Packet | Subclass out of Packet | Non-subclass out of Packet |
    | :---: | :---: | :---: | :---: | :---: |
    | ```private``` | Y | N | N | N |
    | Default | Y | Y | N | N |
    | ```protected``` | Y | Y | Y | N |
    | ```public``` | Y | Y | Y | Y |
      
    * Setter & Getter -- Encapsulation
      
       ```java
       class Person{
          private int age;
          public void setAge(int age){
             if(age>0 && age<200) this.age = age;
          }
          public int getAge(){
             return age;
          }
       }
       ```
      
* Modify Classes

    * Accessibility:

    |  | Within Packet | Out of Packet |
    | :---: | :---: | :---: |
    | Default | Y | N |
    | ```public``` | Y | Y |

### Other Modifiers

|  | Modify Classes | Modify Members | Modify Local Variables |
| :---: | :---: | :---: | :---: |
| ```static``` | Inner Class | Y | N |
| ```final``` | Y | Y | Y |
| ```abstract``` | Y | Y | N |

* static
    * ```static``` Field
       * Not belong to any instance, stored in the memory block of class
       * Could be accessed by class name or an instance, same result
       * "Global variable"
    * ```static``` Method
       * Not belong to any instance
       * Can't use ```super``` or ```this```
* final
    * ```final``` Class: Can't be inherited
    * ```final``` Method: Can't be overrided by subclasses
    * ```final``` Field & Local Variable
       * Read-only 
       * ```static final``` fields represent constants. If not be initialized, the default values are 0 for numbers, false for boolean values, null for references.
       * ```final``` fields and local variables **MUST** be and could only be assigned once.
* abstract
    * ```abstract``` Class: Can't be instantiated
    * ```abstract``` Method
       * Only declared, not implemented: ```abstract returnType abstractMethod([paramlist]);```
       * An ```abstract``` class may or may not contain ```abtract``` methods; but if a class contains an abtract methods, it is an ```abstract``` class.
       * ```abstract``` methods MUST be implemented (overrided) in the subclass, otherwise the subclass is still abstract.

## Interface
Define an interface: all methods are ```public abstract```.  
Implement an interface: multi-inherite; have nothing to do with class inheritence.

* Constant in Interface
    * ```(public static final) type NAME = value```
* Enumeration

    ```java
    enum Light{Red, Yellow, Green}
    Light light = Light.Red;
    switch(light){case Red:......Break;}
    ```
* ```static``` Method (above Java8): not only declared, also implemented; no need to be overrided in subclasses.

## Definition Summary
* Class

   ```java
   [public][abstract|final] class ClassName [extends SuperclassName][implements InterfaceNameList]{
         [public|protected|private][static][final][transient][colatile] type variableName;      //Fields
         [public|protected|private][static][final|abstract][native][synchronized] returnType methodName ([paramList])      //Methods
         [throws exceptionList]{
               statements
         }
   }
   ```

* Interface

   ```java
   [public] interface InterfaceName [extends SuperInterfaceList]{
         type constantName = value;    //Constants
         returnType methodName([paramList]);    //Methods
   }
   ```

* Method
    * Constructor
    
       ```java
       className([paramList]){
            ......
       }
       ```
    
    * main()
    
       ```java
       public static void main (String arg[]){
            ......
       }
       ```
    
    * finalize()
    
       ```java
       protected void finalize() throws throwable{
            ......
       }
       ```

* .java File

   ```java
   package packageName;    //0 or 1
   import packageName.[className|*];      //0 or many
   public classDefinition     //0 or 1, className = fileName
   interfaceDefinition and classDefinition      //0 or many
   ```

## OO Design: Course Enrollment System
In this project, I used all elements metioned above, including class, interface, various modifiers, inheritence, and etc. View the whole project [here](https://github.com/zhtiansweet/CourseEnrollment).
