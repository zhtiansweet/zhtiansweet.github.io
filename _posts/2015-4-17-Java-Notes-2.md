---
layout: post
title: Java Notes (2) - Data Type & Operation & Flow Control & Array
---
Course: [Java Programming (Coursera)](https://class.coursera.org/pkujava-001)  
Instructor: [Dashi Tang](https://www.coursera.org/instructor/~3838), [Peking University](http://english.pku.edu.cn/)

## Data Type
* Primitive Type: stored in the stack (_"Here"_)
  * Numeric Type
     * Integral Type: **byte, short, int, long**
     * Floatint-point Type: **float, double**
  * **char**
  * **boolean**
* Reference Type: pointer to the object stored in the heap (_"There"_)
  * **class**
  * **interface**
  * **Array**

* boolean
 
    ```java
    if (a = 5) {}  //Wrong!!! Nonzero doesn't mean false!
    ```
* char: Unicode
 
    ```java
    char c1 = '\u0061' //c1 = 'a'
    ```
* Integral Type (_Fixed on different OS_)

    _Also see my blog: [Play with Integral Types in Java](http://zhtiansweet.github.io/Java-Integral-Types/)_
 
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
    long l = 3L;
    ```
    
    * No _unsigned_ integer!

* Floatint-point Type (_Fixed on different OS_)
    
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
    print("d2 =", d2);  //d2 = 11111011 = -5
    print("a1>>2 =", a1>>2);  //a1>>2 = 00000000000000000000000000000001 = 1
    print("a1>>34 =", a1>>34);  //a1>>34 = 00000000000000000000000000000001 = 1
    print("a2>>2 =", a2>>2);  //a2>>2 = 11111111111111111111111111111110 = -2
    print("a2>>>2 =", a2>>>2);  //a2>>>2 = 00111111111111111111111111111110 = 1073741822
    print("d1>>2 =", d1>>2);  //d1>>2 = 00000000000000000000000000000001 = 1
    print("d2>>2 =", d2>>2);  //d2>>2 = 11111111111111111111111111111110 = -2
  }

  static void print(String prefix, int n){
    String s = Integer.toBinaryString(n);  //change int into binary string
      while(s.length() < 32) s="0"+s;  //make the output be 32 bits
        System.out.println(prefix + " " + s + " = " + n);
  }

  static void print(String prefix, byte n){
     String s = String.format("%8s", Integer.toBinaryString(n & 0xFF)).replace(' ', '0');  //make the output be 8 bits
     System.out.println(prefix + " " + s + " = " + n);
  }
```

* Numeric Promotion: byte, short, char -> int -> long -> float -> double

## Flow Control
* Sequence
* Selection  
  e.g. Auto Test & Score
* Iteration  
  e.g. Draw Circles

## Array
* Read-only Traversal
    
    ```java
    int[] ages = new int[10]:
    for(int age: ages){
      System.out.println(age);
    }
    ```
    
* Copy
  * System.arraycopy(Object src, int srcPos, Object dest, int destPos, int length)
  * Arrays.copyOf(Array original, int newLength)
  * Arrays.copyOfRange(Array original, int from, int to)

  ```java
    int[] src = new int[]{2, 3, 5, 1, 6};
    int[] dest1 = new int[10];

    System.arraycopy(src, 0, dest1, 3, 5);  
    int[] dest2 = Arrays.copyOfRange(src, 2, 7);  
    int[] dest3 = Arrays.copyOf(src, 3);  

    System.out.println(Arrays.toString(dest1));  //dest1 = [0, 0, 0, 2, 3, 5, 1, 6, 0, 0]
    System.out.println(Arrays.toString(dest2));  //dest2 = [5, 1, 6, 0, 0]
    System.out.println(Arrays.toString(dest3));  //dest3 = [2, 3, 5]
  ```

* Two-dimenstional Array

  ```java
    int[][] t1 = new int[4][];
    t1[0] = new int[]{1,2,3,4,5};
    t1[1] = new int[3];

    int[][] t2 = new int[4][5];
    t2[0] = new int[]{1,2,3,4,5};
    t2[1] = new int[]{1,2,3};
    for(int i=0;i<t2[2].length;i++) t2[2][i] = i;

    System.out.println(Arrays.deepToString(t1));  //t1 = [[1, 2, 3, 4, 5], [0, 0, 0], null, null]
    System.out.println(Arrays.deepToString(t2));  //t2 = [[1, 2, 3, 4, 5], [1, 2, 3], [0, 1, 2, 3, 4], [0, 0, 0, 0, 0]]
  ```

## _Exercise_
* Generate 7 different integers in [1, 36] randomly

  ```java
    public static void main(String[] args) {
        int[] a = new int[7];
        for(int i=0;i<a.length;i++) {
            begin:
            while(true) {
                a[i] = random(1, 36);  //Generate a random integers in [1, 36]
                
                //Ensure that the selected numbers are different
                for (int j = 0; j < i; j++) {
                    if (a[j] == a[i]) continue begin;
                }
                break;
            }
            System.out.print(a[i]+" ");
        }
    }
    
    //Generate a random integer in [min, max]
    public static int random(int min, int max){
        Random r = new Random();
        return r.nextInt(max-min+1)+min;
    }
  ```

* Output all prime numbers less than 100 with [Sieve of Eratosthenes](http://en.wikipedia.org/wiki/Sieve_of_Eratosthenes)

  ```java
      public static void main (String arg[]){
        //Initialize an array
        boolean[] b = new boolean[101];
        for(int i=2;i<101;i++){
            b[i] = true;
        }

        for(int i=0;i<=10;i++){     //There is no need to traverse i>sqrt(100)
            if (b[i]) {
                //Delete i's multiples
                for (int j = i*i; j < 101; j += i) {      //Multiples less than i*i have been checked
                    b[j] = false;
                }
            }
        }
        
        //Output
        for (int i=0;i<101;i++){
            if (b[i])   System.out.print(i+" ");
        }
    }
  ```
It will print out: 2 3 5 7 11 13 17 19 23 29 31 37 41 43 47 53 59 61 67 71 73 79 83 89 97
