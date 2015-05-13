---
layout: post
title: Java Programming Notes (2) - Data Type & Expression & Array
---
Course: [Java Programming (Coursera)](https://class.coursera.org/pkujava-001)  
Instructor: [Dashi Tang](https://www.coursera.org/instructor/~3838), [Peking University](http://english.pku.edu.cn/)

## Data Type
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
3. Integer (_Fixed on different OS_)
 
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
   int i = 0b00010010;  //Binary (Java7 and above)
   long l = 3l;
   ```
  * No _unsigned_ integer!
   * Use ```long``` to deal with uint 
4. Float (_Fixed on different OS_)
    | Type | Size (Byte) | Range |
    | :---: | :---: | :---: |
    | float | 4 | -3.403E38 ~ 3.403E38 |
    | double | 8 | -1.798E308 ~ 1.798E308 |

  * Expression
  
   ```java
   double d = 3.14;
   float f = 3.14f;
   ```
* Identifier
  *  Class: Pascal (e.g. Racer)
  *  Others: camel (e.g. racerList)

## Operator
* Division /
 * 15/4 = 3, 15.0/2 = 7.5
* Short-circuit && ||

  ```java
  if ((d != null) && (d.day > 31)) {}  //When (d = null), the latter will not be evaluated
  ```
* Shift
 *  Left shift <<, signed right shift >>, unsigned right shift >>>
 *  Integer Promotion: promote byte and short to int before operation
 *  a>>b: if a is int, b = b mod 32; if a is long, b = b mod 64
 
  ```java
    public static void main(String[] args) {
        int a1 = 5;
        int a2 = -5;
        byte d1 = 5;
        byte d2 = -5;
        print("a1 =", a1);  //a1 = 00000000000000000000000000000101 = 5
        print("a2 =", a2);  //a2 = 11111111111111111111111111111011 = -5
        print("d1 =", d1);  //d1 = 00000101 = 5
        print("d2 =", d2);  //d2 = 1111111111111111111111111111111111111111111111111111111111111011 = -5
        print("a1>>2 =", a1>>2);  //a1>>2 = 00000000000000000000000000000001 = 1
        print("a1>>34 =", a1>>34);  //a1>>34 = 00000000000000000000000000000001 = 1
        print("a2>>2 =", a2>>2);  //a2>>2 = 11111111111111111111111111111110 = -2
        print("a2>>>2 =", a2>>>2);  //a2>>>2 = 00111111111111111111111111111110 = 1073741822
        print("d1>>2 =", d1>>2);  //d1>>2 = 00000000000000000000000000000001 = 1
        print("d2>>2 =", d2>>2);  //d2>>2 = 11111111111111111111111111111110 = -2
    }

    static void print(String prefix, int n){
        String s = Integer.toBinaryString(n);  //change int
        while(s.length() < 32) s="0"+s;  //make the output be 32 bits
        System.out.println(prefix + " " + s + " = " + n);
    }

    static void print(String prefix, byte n){
        String s = Byte.toBinaryString(n);
        while(s.length() < 8) s="0"+s;  //make the output be 8 bits
        System.out.println(prefix + " " + s + " = " + n);
    }
  ```
