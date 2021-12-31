# Java Language Basics 





## primitive types 

java has 8 primitive type 
primtives includes 
boolean and numbers 
number includes integer, floating point and character 



### ints 
integer includes byte 8 bits, short 16 bits, int 32 bits, long 64 bits 
```java
byte age = 18; 
short rank = 165; // -128 - 127
int integer = 100;
long number = 223_122_324L; // java 7
int binary = 0b0100; // java 7
int hex = 0x0042;


```

### floats 
floating point includes float and double 
float has 32 bits 6-7 decimal points 0.0f.
we have to use the 0.0f otherwise it will generate a compilation error for double precision lossy 

double has 64 bits which has 15-16 decimal points 0.0d

```java
float number = 3.2f;


```

### char [0,65535]

character includes char 
char is a single character 
the data representation is 16 unsigned integer java uses unicode 16 
0 - 2^16

```java

char a = 'a';
char a = 65; // A
char a = 0x0041; // A 
char a = 0b010; //A
```

a char variable can be 1. unicode escape sequece 2. char litearl 3. int litearl 


### boolean types 

by default, a boolean variable is initialized with false 
by depth, it is defined under the specifc jvm implementation so it can vary 



## Type casting

### implicit casting 
once the variable has been declared with one type, it has to stick to that type but sometimes if we want to assign variable with a value which is of other data typse 

assign variables or literals of one type to variable of another type explicitly or implicitly 

only numeric to numeric casting is possible, you cannot cast to boolean or vice versa. 

smaller to larget ~ windening conversion int to long is implicit casting by compiler 
byte 8 bit -> short/char 16 bits -> int 32 bits -> long 64 bits -> float 32 bits -> double 64 bits 


```java
public class Hello{
    public static void main(String []args){
        byte a = 10;
        short b = a;
        int c = b;
        //char d = c;
      //  long e = d; d cannot be resolved to a variable
       // float f = e; e cannot be resolved to a variable
      //  double g = f; f cannot be resolved to a variable

       int d = 10;
       long e = d;
       // pass 

       float f = e;
       double g = f;


       int h = 10;
       double i = h;
 
    }
}

```


```java
public class Hello{
    public static void main(String []args){
        boolean hello = true;
        // type mismatch int hello2 = hello;

        

        System.out.println(hello);
    }
}

```

### explicit casting 

type_a variable_a = value;
type_b variable_b = (type_b) variable_a;

```java
public class Hello{
    public static void main(String []args){

        long a  = 100;
        int b = (int) a;
        System.out.println(b);

        byte c = 65;
        char d = (char) c;
        System.out.println(d);
     
    }
}
```


### loss in explicit casting 
1. out of range assignemnt 

```java
byte number = byte(123456); // 64

```


2. truncation , floating point to integer/char always truncate 

```java
int x = (int) 3.14;

```

3. loss of precssion from byte to short to int to long to float to double 
```java
int a = 123456789;
float b = a;
int c = (int)b; // no longer the same 123456792

```


### casting use csaes 
1. implicit casting 


```java
float arg1 = 1.32f;
float arg2 = 1.334f
method(arg1,arg2);

```

2. explicit casting 
```java
double number = (2 + 3) / 2;
double number = (double) (2 + 3) / 2;
public class Hello{
    public static void main(String []args){
     byte a = (byte)128;
     System.out.println(a);
     int c = 'A';
     System.out.println(c); 



    }
}
```



## Variables
variable means its value can be changed 

### Variable declaration
#### <type><name> [= literal or exprsesion]
#### literal -> raw data 
java is statically typed language 

primite variable is not a reference 

```java
data_type variableName = value;
ClassType objectName = new ClassType(); // object reference 


```
 

### initializing multiple variables 
```java
datatype variable, variable2, variable3;

datatype variable = literal, variable2, variable3;
```

#### assigment statement <name> = literal or expression 


```java
variable = value;
//cannot appear at class level 
```


## operators 

operator performs operation on its operands and produces a result 

### unary operators:
1. operator operand ~ prefix -x 
2. operand operator x++
 


### binary operator includes 
1. assignment operator =, +=, -=, %=, *=, /=
2. arithmetic operator +, -, *, /, % 
3. comparison operators >, <, >=, <=, ==, !=
```java

public class Hello{
    public static void main(String []args){
   System.out.println(1 == 1);
   System.out.println(1 < 2);
   System.out.println(1 > 0);
   System.out.println(1 >= 1);
   System.out.println(1 <= 1);
   System.out.println(1 != 2);

    }
 
}
```
4. logical operators !, ||, &&
&& short circut left operand is false, return false -- conditional and . if object !- null && conditonal 
|| left operand is true, return true 
&& prevents NullPointerException
```java
public class Hello{
    public static void main(String []args){
    System.out.println(1 == 1 && 2 == 2);
    System.out.println(1 == 1 || 2 == 2);

    }
 
}

```

5. bitewise operator
Bitwise operators are used to perform the manipulation of individual bits of a number. They can be used with any integral type (char, short, int, etc.). They are used when performing update and query operations of the Binary indexed trees. 

operate on invidual bits of operands 
operands: integer primitives ~ operand promotion rules applies 
boolean is rare 

it is used mostly in embedded systems or hash table e.g. hashmap or compression & encription 


bitwise and & 
returns 1 if both input bits are 1 
00000001
00000011
00000001

bitwise or | 
returns 1 if either of input bits is 1 

00000001
00000011
00000011

bitwise xor ^
returns 1 only if one of the input bits is 1 but not both 
00000001
00000011
00000010

non short circuit operators 
& and | alaways checks both operands 
operand1 = operand1 & operand2





6. bit shift operator 
shift bits, operands ~ integer primitives 

left-shift operator <<
left shifts left operand by number of bits specified on the right 

6 -> 00000110
6 << 1 -> 00001100
insert zeros at lower order bits 
#### same as mulitplication by powers of 2
```java
public class Hello{
    public static void main(String []args){
      int variable = 2;
      System.out.println(variable << 1);
      System.out.println(variable << 4);



    }
 
}

```

unsigned right shift operator >>> 
right shifts left operand by number of bits specified on the right 
insert zeros at higher order bits 

12 -> 00001100
12 >>> 1 -> 00000110 -> 6

same as division by powers of 2

```java
public class Hello{
    public static void main(String []args){
      int variable = 16;
      System.out.println(variable >>> 1);

 System.out.println(variable >>> 3);
      

    }
 
}
```


signed right-shift operator >> 
same as >>> but padded with MSB, sign is preserved 


the real application of bit shift operators are for compiler optimizations: replace mulitplication & division 
it is also used in hastable 
embeddeing programming, games prgramming, systems with no floating point support 






7. instanceof operator 

### tenary operator:
?:
operand operator operand operator opernad x > 3 ? x : 0
tenary operator always uses two symbols 

### operator precedence 
rule1: muliplitcative opreators *,/,% have higger precedence over additive operators +,-
rule2: operators in the same type are evalauted from left to right 
rules3: use parenthesis to change evaluation order 

### operand promotion
operands which are smaller than int are promoted to int e.g. byte + int = int 

### same type opeations 
if both operands are int , long, float, or double, then operatiosn are carried in that type and evaluated to a value of that type 

### mixed type operations 
if operands belong to different types, then smaller type is promoted to larger types 
order of promotion: int-> long -> float-> double 
char + float -> int + float -> float

```java
public class Hello{
    public static void main(String []args){
     int a = 1;
     double b = 1.000001;

System.out.println(a + b);

    }
 
}

```


### compoud bit shift assignment
operand = operand1 << operand2
operand1 <<= operand2
operand = operand1 >>> operand2 
operand1 >>>= operand3
operand1 = operand1 >> operand2 
operand1 >>= operand2

left shifts is same as multiplying by the power of two while performing unsigned right shift is the same as division bipolar self-dual and that is about it 







## statement
statements are command to be executed. e.g. declare a variable. change variable values. invoke a method 
change a program state

statement involves one or more exprsesions 
exprssion ~ evaluated to single value -- involves literals, variables, operators, and method calls 


1. declaration statements data_type variable = value;
2. expression statements 
3. control flow statements 
all of them are not at class level 




## Arrays 


array is a container object that holds fixed number values of single types 

it has index and elements 


```java
datatype [] variableName = new dataType[numberOfElements];
variableName[index] = element;

```

```java

datatype [] variableName = new dataType[]{elements};
datatype [] variableName = new dataType[]{};
```

### array operatiosn 
1. length 

```java
array.length

```

### 2D Arrays 

it means array of array such as type[][] array;


```java
datatype [][] variableName = new dataType[numberOfElements][numberOfElements];
variableName[index][index] = element;

```


initilization

```java

dataType [][] array = new int[][]{
    {element1,element2},
    {element3,element4}
};

```

irregular rows 

```java
type [][] array = new type[numberOfElement][];
array[numberOfElement] = new int[number];

```

notably we can also have 3D arrays 

```java

dataType [][][] array = new int[][][]{
    {element1,element2,element3},
    {element4,element5,element5}
};

```


## if statement 

```java
if(conditional){

}else if(conditional){
    
}else{

}

```


## control switch 
control flow statements which is a swtich statement, a switch statement has a lot of details involved 

it can be an alternative to if statement 

```java 
switch(case){
    case label1: statement;
    break;
    case label2: statement;
    break;
    case label3: statement;
    break;
    default: statement;
    break;


}

```

Integer, e.g. 
byte, short, char, int cannot be long 
byte -> Byte 
short -> Short 
char -> Character 
int -> Integer 

String 
enum 


### Case Label Restrictions 

1. must be within range of data type of swtich expression 
2. constant exprssion: value known at compile time 
3. value must be unique 
4. cannot be null 

must be within range of data type of switch expression 

constant expression: value known at compile-time 
integer or string literal, cosntant variable 


when is switch infeasible? more than one condition to test, tests other than equality, switch exprssion is not integer, string, or enum.

a case label restriction does not apply 

when is switch preferred, readability. intent, switch deliberately states that only one variable is involved 

### control flow: ternary

shorthand for if-else with single statements
result = (boolean-expression) ? true-expr : false-expr


```java
if(boolean-conditional){
    
}else{

}

```

when is ternary preferred? improved readability 
smart string construction 


ternary as expression statement? cannot be an expression statement. however it cannot be expressed as an expression statement that is only certain kinds of experience 


cannot be an expression statement: 
(boolean-expression) ? true-expr: false-expr; // invalid 

```java
public class Hello{
    public static void main(String []args){
       
        int a = 10;
        int b = 20;

      //  (a >= 10) ? System.out.println(a); : System.out.println("condition is false");
      /*
        Syntax error on token ">=", invalid AssignmentOperator
        Type mismatch: cannot convert from int to boolean
        Syntax error on token ";", delete this token 

        at Hello.main(Hello.java:6
      
      */
       int result = a > b ? a : b;
       System.out.println(result);
    }
 
}
```

## for statement 

iteartion statement 

```java
for(initialization; condition-exprssion;expression-list){

}

for(int i = 0; i < number; i++){

}

```

declaration statement. initilization part is optional. 


you cannot use double as the data type to initialize, you cannot use different variables such as (int i = 0; j < 10; j++)


the condition exprssion must evaluate to boolean. it is optional if omitted, a true is assumed then it is a infinite loop 

```java

for(int i = 0; ; i++){

}
```


```java

public class Hello{
    public static void main(String []args){
     int i = 0, j = 0;

     for(; i < 10 && j < 10; i++, j++){
         System.out.println(i + ":" + j);
     }

    }
 
}
```

```java

public class Hello{
    public static void main(String []args){
     

     for(int i = 0, j = 0; i < 10 && j < 10; i++, j++){
         System.out.println(i + ":" + j);
     }

    }
 
}
```

expression list can have list of comma separted exprsesion statements, below is wrong 

```java
public class Hello{
    public static void main(String []args){
 

     for(int i = 0; i< 10; System.out.println(i),i++){
    }

    }
 
}

```


## for each statement 


```java

for(dataType element : collection){

}

```


## while statement 

iteration statement use for ~ if the number of iterations is known 

while statement only has condition expression 


```java
while(condition-expression){

}

```


## do while statement 
similar to while statement but runs at least once 

```java

do{

}while(condition);
```
## infinte loop 

```java
while(true){

}

for(;;){

}

```


## break statement 
exit the enclosing switch or loop aka while/for loop immediately 


```java
// only exit inner loop 
for(){
    for(){
        break;
    }
}
```


## continue statement 
it is used with only loops, it continues with next iteration of innermost loop 


```java
while(condition){
    if(condition){
        continue;
    }
}

for(initilization; condition; exprssion){
    if(condition){
        continue;
    }
}

```




## variable scopes 

every variable has a scope 
1. entire class 
2. cannot be assigned to variables declared before it 


the scope of local variable is from declaration point to end of block 

methods invoked from lcoal variables will have a new scope 





## String Class

string is an object of class java.lang.String 


```java

String s  = new String(); // empty string 
String s = new String("content is a string");
char [] characters = {'a','b'};
String s = new String(characters);
String s = "hello";

```

#### string literal is a string object!!

String classes uses character array to store text, java uses UTF16 for characters 
string is a sequence of unicode characters 
string is immutable 

#### String immutablity 

string values cannot never be changed. but why does it matter? 
1. because if mutable, sharing is not possible. also for concurrency,
2. that is if a string object is mutable between different threads and one thread modifies it then the remaining would get affected without them being offered 
3. security --- FileInputStream(String name)


```java
String s = "hello";
// you cannot do s[1] = "a";
s - new String('a'); // the oject is abandoned 

```

#### String + concatenation 

```java
String s = "1" + "2";

```
String pool ~ saves memory 

beware, combing few strings is fine, with each concatenation, contents of both strings are copied 
new StringBuilder is created to be appeded with both String, return string via toString() so that StringBuilder is created for each concatenation 
+= is time consuming ~ O(N^2) and space consuming too 




there are two classes allow us to mutate strings that is: 
1. StringBuilder ~ java 5
StringBuilder is not syncronized, 

```java
StringBuilder sb = new StringBuilder();
sb.append("a");
sb.append(b);
String s = sb.toString();
sb.length();
sb.delete();
sb.insert();
sb.reverse();
sb.replace();
```
Using string builder is O(N) 


2. StringBuffer ~ Obsolete 
although it is synchronous but it is slow. .we should always use StringBuilder, API wise it is comptaible with StringBuilder 








### common string methods 

1. comparison 
```java
s.isEmpty(s2);
s.length();
s.equals(s2);


```

2. searching 

```java
s.startsWith(c);
s.endsWith(c);
s.contains(c);

```

3. find individual characters 
```java
s.indexOf('c');
s.lastIndexOf('c');
s.charAt(index);
```




4. extract substring 
```java
s.substring(start,end);
```

5. case translation 
```java
s.toUpperCase()
s.toLowerCase();
```

6. replace 

```java
s.trim(); // trim any leading or trailing spaces 
s.replaceAll(c1,c2);

```

7. split 
```java
s.split(delimiter);

```




### String literals versus using new 
string literal 
1. String via string literal. it is stored in string pool on heap
String pool stores single copy of each string literal as string object 

2. literals with same content share storage 

```java
String s1 ="A";
String s2 ="A";
String s3 = s2;
s1 -> s2 -> s3 -> string pool 
```

string via new 
same as regular object with no storage sharing 


```java
String s4 = new String("A");
// not with s1 or s2 or s3 in the same string pool 

```

#### String interning 
it processes of building string pool 

for jvm, it is encountering a string literal for first time 

1. create a new Strin object with given literal 
2. invoke intern() 
if(string in string pool) returns existing reference 
else add to string pool and return reference 

```java
String s1 = 'a';
String s2 = "a" + "b"; // new intern
String s3 = s1 + "c"; // not interned 
s3 = s2.inern(); //~ explicitly interned 

```
is explictly interning useful? mostly like not, only for JVM . or natural language processing 
Basically doing String.intern() on a series of strings will ensure that all strings having same contents share same memory. So if you have list of names where 'john' appears 1000 times, by interning you ensure only one 'john' is actually allocated memory.

This can be useful to reduce memory requirements of your program. But be aware that the cache is maintained by JVM in permanent memory pool which is usually limited in size compared to heap so you should not use intern if you don't have too many duplicate values.
There are some "catchy interview" questions, such as why you get equals! if you execute the below piece of code.
```java
String s1 = "testString";
String s2 = "testString";
if(s1 == s2) System.out.println("equals!");
```
If you want to compare Strings you should use equals(). The above will print equals because the testString is already interned for you by the compiler. You can intern the strings yourself using intern method as is shown in previous answers....

#### Escape sequence 
character preceded by \
to use special characters in strings and character literals 
it has 
1. \" 
2. \'
3. \n 
4. \t 
5. \\
6. \r 
7. \b
8. \f 



## Math Class 

```java
Math.ceil(number);
Math.max(number1, number2);
Math.abs(number);
Math.sqrt(number);
Math.pow(float_number,float_number);
Math.log(float_number);

```






