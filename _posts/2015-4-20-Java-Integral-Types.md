---
layout: post
title: Play with Integral Types in Java
---
First of all, let's list all integral types in Java here.

| Type | Size (Byte) | Range |
| :---: | :---: | :---: |
| byte | 1 | -128 ~ 127 |
| short | 2 | -2^15 ~ 2^15-1 |
| int | 4 | -2^31 ~ 2^31-1 |
| long | 8 | -2^63 ~ 2^63-1 |

## Literal   
All integral types are in integral literals. An integer literal is of type long if it is suffixed with an ASCII letter L (preferred) or l; otherwise it is of type int. It means that **byte and short are initialized by int literals**, for there is no byte or short literal in Java. **Don't consider the first bit as a sign bit when using a binary literal for byte or short!!!** 

```java
  int a1 = 5;   //a1 = 00000000000000000000000000000101 = 5
  int a2 = -5;    //a2 = 11111111111111111111111111111011 = -5
  int a3 = -0b101;    //a3 = 11111111111111111111111111111011 = -5
  int a4 = 0b1111_1111_1111_1111_1111_1111_1111_1011;   //a4 = 11111111111111111111111111111011 = -5
  int a5 = 0b1000_0000_0000_0000_0000_0000_0000_0101;   //a5 = 10000000000000000000000000000101 = -2147483643

  byte d1 = 5;    //d1 = 00000101 = 5
  byte d2 = -5;   //d2 = 11111011 = -5
  byte d3 = -0b101;   //d3 = 11111011 = -5
  byte d4 = 0b1111_1011;    //Wrong!!!   
  byte d5 = (byte)-0b1000_0000_0000_0000_0000_0000_0000_0101;   //d5 = 11111011 = -5
  byte d6 = -0b1000_0000;   //d6 = 10000000 = -128
  byte d7 = 0b1000_0000;    //Wrong!!!
  byte d8 = 0b0111_1111;    //d8 = 01111111 = 127
  byte d9 = (byte)0b1000_0000;    //d9 = 10000000 = -128
```

Since there is no unsigned number in Java, we can always use the equation **-x = ~x + 1** ("~" means bitwise NOT) for the two's complement integers. For example, byte 5 is 00000101, so ~00000101 + 1 = 11111011 = -5.

For ```byte d4 = 0b1111_1011;```, d4 is actually 00000000000000000000000011111011 = 251 because it is in an **int literal**. And 251 exceeds the maximum value of byte, 127, so this expression is illegal.  

For ```byte d5 = (byte)-0b1000_0000_0000_0000_0000_0000_0000_0101;```, first we could get -10000000000000000000000000000101 = 01111111111111111111111111111011. And when casting an int to a byte, we could abandon the first 24 bits, getting 11111011 which is byte -5.  

For ```byte d7 = 0b1000_0000;```, d7 is actually 00000000000000000000000010000000 = 128 which exceeds the maxmum value of byte, 127. So this expression is illegal.  

For ```byte d9 = (byte)0b1000_0000;```, "0b1000_0000" is actually 00000000000000000000000010000000. When casting it to a byte, we get 10000000 which is byte -128.

## Operation   
If an integer operator other than a shift operator has at least one operand of type long, then the operation is carried out using 64-bit precision, and the result of the numerical operator is of type long. If the other operand is not long, it is first widened to type long by numeric promotion.  

Otherwise, the operation is carried out using 32-bit precision, and the result of the numerical operator is of type int. If either operand is not an int, it is first widened to type int by numeric promotion.

Any value of any integral type may be cast to or from any numeric type. 

```java
  byte b = 39;    //b = 00100111 = 39
  short s = -130;   //s = 1111111101111110 = -130
  int i = -10000;   //i = 11111111111111111101100011110000 = -10000
  long l = 1234567890123456789l;    //l = 0001000100100010000100001111010001111101111010011000000100010101 = 1234567890123456789

  print("b&l =", b&l);    //b&l = 0000000000000000000000000000000000000000000000000000000000000101 = 5
  print("i|l =", i|l);    //i|l = 1111111111111111111111111111111111111111111111111101100111110101 = -9739
  print("b^s =", b^s);    //b^s = 11111111111111111111111101011001 = -167
  print("b+i =", b+i);    //b+i = 11111111111111111101100100010111 = -9961
  print("int b =", (int)b);   //int b = 00000000000000000000000000100111 = 39
  print("byte l =", (byte)l);   //byte l = 00010101 = 21
```

## Convert an Integers into a Binary String  
For int and long, we could directly use ```Integer.toBinaryString()``` and ```Long.toBinaryString()```. But for byte and short, we need to play a trick using ```Integer.toBinaryString()```.

```java
  public static void main(String[] args) {
      byte b = 39;
      short s = -130;
      int i = -10000;
      long l = 1234567890123456789l;

      print("b =", b);
      print("s =", s);
      print("i =", i);
      print("l =", l);
  }

  static void print(String prefix, byte n){
      String s = String.format("%8s", Integer.toBinaryString(n & 0xFF)).replace(' ', '0');
      System.out.println(prefix + " " + s + " = " + n);
  }

  static void print(String prefix, short n){
      String s = String.format("%16s", Integer.toBinaryString(n & 0xFFFF)).replace(' ', '0');
      System.out.println(prefix + " " + s + " = " + n);
  }

  static void print(String prefix, int n){
      String s = Integer.toBinaryString(n);
      while(s.length() < 32) s="0"+s;
      System.out.println(prefix + " " + s + " = " + n);
  }

  static void print(String prefix, long n){
      String s = Long.toBinaryString(n);
      while(s.length() < 64) s="0"+s;
      System.out.println(prefix + " " + s + " = " + n);
  }
```

It will print out:  
![print]()

This ```print``` function is also helpful when judging the data type of the operation results:)
