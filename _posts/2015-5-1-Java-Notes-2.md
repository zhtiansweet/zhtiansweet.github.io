---
layout: post
title: Java Programming Notes (2) - Data Type & Expression & Array
---
Course: [Java Programming (Coursera)](https://class.coursera.org/pkujava-001)  
Instructor: [Dashi Tang](https://www.coursera.org/instructor/~3838), [Peking University](http://english.pku.edu.cn/)

### Data Type
* Primitive Type: stored in the stack (_"Here"_)
  * Numeric Type
     * Integer: **byte, short, int, long**
     * Float: **float, double**
  * **char**
  * **boolean**
* Reference Type: pointer to the object stored in the heap (_"There"_)
  * **class**
  * **interface**
  * **Array**

1. boolean
 
    ```java
    if (a = 5) {}  //Wrong!!! Nonzero doesn't mean false!
    ```
2. char: Unicode
 
    ```java
    char c1 = '\u0061' //c1 = 'a'
    ```
3. Integer
 
   | Type | Size (Byte) | Range |
   | :---: | :---: | :---: |
   | byte | 1 | -128 ~ 127 |
   | short | 2 | -2^{15} ~ 2^{15}-1 |
   | int | 4 | -2^{31} ~ 2^{31}-1 |
   | long | 8 | -2^{63} ~ 2^{63}-1 |

  * Expression
  
   ```java
   int i = 12;  //Decimal
   int i = 012;  //Octal
   int i = 0x12;  //Hexadecimal
   int i = 0b00010010  //Binary (Java7 and above)
   ```
  * No _unsigned_
 
