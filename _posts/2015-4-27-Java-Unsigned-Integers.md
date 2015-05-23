---
layout: post
title: Play with Unsigned Integers in Java
---
_For basic knowledge of data types in Java, please see [here](http://zhtiansweet.github.io/Java-Notes-2/)._

There is no unsigned integral type in Java. In Java SE 8 and later, however, we could use int and long to represent unsined integers, with the range of 0 ~ 2^{32}-1 (32 bits) and 0 ~ 2^{64} (64 bits). And the [Integer][1] and [Long][2] class also contains methods like compareUnsigned and divideUnsigned etc to support arithmetic perations for unsigned integers. 

Let's play with these methods! 

[1]: https://docs.oracle.com/javase/8/docs/api/java/lang/Integer.html
[2]: https://docs.oracle.com/javase/8/docs/api/java/lang/Long.html

Below are some examples for toUnsignedLong, toUnsignedString, parseUnsignedInt, compareUnsigned, divideUnsigned, remainderUnsigned methods, and also the comparisons between them and the ones for signed integers. IntegralType.print is a function to print out the 32-bit binary representation for int and 64-bit for long, please see details <a href="http://zhtiansweet.github.io/Java-Integral-Types/#binary">here</a>. I wrote the results in the console as comments. 

```java
int x = 5;
int y = -2;
String s = "11111111111111111111111111111110";
long z = -2L;

IntegralType.print("x =", x);   //x = 00000000000000000000000000000101 = 5
IntegralType.print("y =", y);   //y = 11111111111111111111111111111110 = -2
IntegralType.print("(unsigned) y =", Integer.toUnsignedLong(y));    //(unsigned) y = 0000000000000000000000000000000011111111111111111111111111111110 = 4294967294
IntegralType.print("z =", z);   //z = 1111111111111111111111111111111111111111111111111111111111111110 = -2
System.out.println("(unsigned) z =" + Long.toBinaryString(z) + " = " + Long.toUnsignedString(z));   //(unsigned) z =1111111111111111111111111111111111111111111111111111111111111110 = 18446744073709551614

IntegralType.print("y =", Integer.parseInt("-2"));    //y = 11111111111111111111111111111110 = -2
IntegralType.print("y =", Integer.parseInt("-10", 2));    //y = 11111111111111111111111111111110 = -2
//IntegralType.print("y =", Integer.parseInt(s, 2));    //Wrong!!!
//IntegralType.print("y = ", Integer.parseUnsignedInt("-2"));    //Wrong!!!
IntegralType.print("y =", -Integer.parseUnsignedInt("2"));    //y = 11111111111111111111111111111110 = -2
//IntegralType.print("y =", Integer.parseUnsignedInt("-10", 2));    //Wrong!!!
IntegralType.print("y =", Integer.parseUnsignedInt(s, 2));    //y = 11111111111111111111111111111110 = -2

System.out.println("Compare x and y: " + Integer.compare(x, y));    //Compare x and y: 1
System.out.println("Unsigned Compare x and y: "+Integer.compareUnsigned(x, y));   //Unsigned Compare x and y: -1

System.out.println("x/y= "+x/y);    //x/y= -2
System.out.println("x%y = "+x%y);   //x%y = 1    
System.out.println("(unsigned) x/y = "+Integer.divideUnsigned(x, y));   //(unsigned) x/y = 0
System.out.println("(unsigned) x%y = "+Integer.remainderUnsigned(x, y));    //(unsigned) x%y = 5

System.out.println("y/x= "+y/x);    //y/x= 0
System.out.println("y%x = "+y%x);   //y%x = -2
System.out.println("(unsigned) y/x = "+Integer.divideUnsigned(y, x));   //(unsigned) y/x = 858993458
System.out.println("(unsigned) y%x = "+Integer.remainderUnsigned(y, x));    //(unsigned) y%x = 4
```

Integer.parseInt(s, 2) tends to parse s as a signed integer in radix 2. You could initialize an int as ```int i = 0b11111111111111111111111111111110```, and i is actually -2. For parseInt, however, Java will consider "11111111111111111111111111111110" as 4294967294, which is larger than the maximum int. So this line will cause an NumberFormatException. The right way is to input a human-read string representing a negetive int like Integer.parseInt("-10", 2).

Integer.parseUnsignedInt("-2") doesn't work because -2 is less than the minimun unsigned int 0. The same reason goes to Integer.parseUnsignedInt("-10", 2).

