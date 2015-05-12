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

1. Primitive Type
   * boolean
  
    ```java
    if (a = 5) //Wrong!!! Nonzero doesn't mean false!
    ```
   * char: Unicode
  
    ```java
    char c1 = '\u0061' //c1 = 'a'
    ```
   *  Integer

     | Type | Size (Byte) | Range |
     | :---: | :---: | :---: |
     | byte | 1 | -128 ~ 127 |

   * Float
