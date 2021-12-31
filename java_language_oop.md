

## methods 
method is a self-contained logic that can be used many times which defines behaviours 
methods can receive inputs and generate outputs 


the return type and return value are mandatory 


```java

returnType methodName(type param1, type param2,.....){
    return value;
}

type variable = methodName(arg1,arg2);

```

### Return types 
1. void: nothing to return ~optional return; as last statement 
2. must be primitive, array, class, interface or void 



### instance mtehod 
instance method is an object level methods. invocation is objectReference.methodName()
instance method affects object state: instance variables and other isntance methods 


### static method 
it has the method which has keyword static in declaration, static method is class level method which has no access to state: instance variables and metohds. Henece, it serves as utility methods 
static method can only access static variables or it can access other static methods 

invokcation: className.methodName();

```java 
public class ClassName{
static ReturnType methodName(type param1, type param2){
    return value;
}
}
ClassName.methodName;


```


a) Accessibility from Static Methods:

Cannot directly access instance variables/methods defined in the same class as the static method

Can directly access static variables/methods defined in the same class

Can access anything via an object reference. So, from a static method by using an object reference, we can access instance variables/methods

b) Accessibility from Instance Methods:

Can access anything from an instance method. So, we can even access static variables/methods defined in the same class as the instance method.

## method overloading 

change the method signature 

```java

returnType methodName(type param1){}
returnType methodName(type param1, type param2){}
returnType methodName(type param2, type param1){}


```

only changing the returnType, static or nonstatic won't work 


### varargs ~ variable length arguments 
last parameter can take variable # arguments 
syntax is three dots following parameter types 

```java

ReturnType methodName(type param1, type...param2)

//1 array 
methodName(arg1, new type[]{elements});
//2 command separate 
methodName(arg1, 1,2,3,4);

```

```java
public class Hello{
    public static void main(String []args){
     methodName(100, 1,2,3,4);
    }

    public static int methodName(int first, int...items){
       
        for(int element : items){
            System.out.println(element);
        }
        return first;
    }
}

```

#### varargs restrictios. it must be the last parameter, methodName(type...args)


why should we use varargs? it provides simpler & flexible invocation 
printf(String format, Object...args); 

#### varargs & overlaoded methods 
invlaid overload are : 
methodName(type arg1, type...arg2)
methodName(type arg1, type [] arg2)
varargs method will be matched last 




## object reference types 

### referece types 
Class allocate space for reference variables 
new allocates space for new object 
= assigns object to the space 

```java
ClassType objectName = new ClassType();


```


#### objects live on heaps , bit depth ~ jvm specific, default null 

without a new it will cause NullPointerException 


### passing data 
1. pass by value 
2. pass by reference 


data_type variable = value; the variable is logical name. memory address, value 
value of argument is passed to parameter
primitive argument ~ value is primitive 
object referecnce argument, value is memory address 

### reinializing object references 


```java
ClassType object1 = new ClassType ();
ClassType object2 = new ClassType ();
ClassType object3 = new ClassType ();
object1 = object2;
object2 = object3;



```
 

## constructors 

the main goal of constructor is to intialize object state 
if no constructor was written, compiler will create a constructor for us. this means when constructor is not provided compiler insets one with no parmaters aka no args constructors 
and if a constructor is provided, there will be no default constructor inserted 

construcots must be first statement and only one per constructor 


```java

Class ClassName{
    type instanceVariable;
    public ClassName(){

    }
    public ClassName(type param1,type param2){
        instanceVariable = param1;

    }
}

```


### constructor overloading 

you cannot provide two constructors with the same signature



```java

Class ClassName{
    type instanceVariable1;
    type instanceVariable2;
    public ClassName(){

    }
        public ClassName(type param1,type param2){
        instanceVariable = param1;

    }
    public ClassName(type param1,type param2){
        instanceVariable1 = param1;
          instanceVariable2 = param2;

    }
}

```

### alternative way 




### `this` constructor invocation statement 
. As before, the compiler determines which constructor to call, based on the number and the type of arguments.
From within a constructor, you can also use the this keyword to call another constructor in the same class. Doing so is called an explicit constructor invocation.This class contains a set of constructors. Each constructor initializes some or all of the rectangle's member variables. The constructors provide a default value for any member variable whose initial value is not provided by an argument. If present, the invocation of another constructor must be the first line in the constructor.


```java


Class ClassName{
    type instanceVariable1;
    type instanceVariable2;
    public ClassName(){
        this(0,0);

    }
        public ClassName(type param1,type param2){
      this(param1,0);

    }
    public ClassName(type param1,type param2){
        instanceVariable1 = param1;
          instanceVariable2 = param2;

    }
}
```

typicallly the conventin seems to be that you would always delegate from the constructor having fewer numbers of constructor parameters 
when this happens, we refer to the primary constructor -- the one with most instance variables 




### `this` keyword in instance variables 

The most common reason for using the this keyword is because a field is shadowed by a method or constructor parameter.

sometimes we have to come up with names that are different from the instance variable names which is a bit challenging, but in realtiy we can use the same names as the instance variable names 





```java


Class ClassName{
    type instanceVariable1;
    type instanceVariable2;
    public ClassName(){
        this(0,0);

    }
        public ClassName(type param1,type param2){
      this(param1,0);

    }
    public ClassName(type instanceVariable1,type  instanceVariable2){
        this.instanceVariable1 = param1;
          this.instanceVariable2 = param2;

    }
}
```



## Packages 
why use packags? because packages have meaningful organization and name scoping, it also enhances and restrict parts of your class to be inaccessible, outside of its package that is only classes with that package should access those parts  
packages -> java.lang-> java.util-> java.io 
APIs improve performance over time and gain new functionality 

important packages 
1. java.lang ~ fundamental classes 
2. java.util ~ data structure 
3. java.io ~ reading & writing 
4. java.net ~ networking 
5. java.sql ~ database 

## Java API 
java API is a library of well tested classes, java 8 has 4240 clsses all developed. 


### accessing class 
some packages ~ direct acces 
different packages using 
1. import 
2. fully qualified class name 
```java

import java.util.ArrayList;

java.util.ArrayList list = new java.util.ArrayList();

```

there is no side effect in using imports, it does not make class bigger nor affect runtime performance. it saves from typing fully qualified name ~ compiler does this  

#### import single versus multiple classes 

1. import single class - explicit import or single type import 
2. import multiple classes - separate explicit import  ~ * import 


import package.name.* 
that imports all classes in a package 
this import package.name.* can break code 


explicit import has better clarity and seems to be preferred 


ifwe have two packagse import with * and explict import 
it always execute the explict import 
```java
import com.foo.*;
import com.hello.ClassName;

public class Something {
       ClassName object = new ClassName();
}

```

#### fully qualified class name 
alternatve to import 
```java

import java.util.ArrayList;

java.util.ArrayList list = new java.util.ArrayList();

```
required if using java.util.packageName 

java lang is imported by default 



### matching directory structure 
basics: -> basic

com.package.ClassName 
-> com 
      -> package 
                -> ClassName 


package name is part of class name 


```shell
javac -classpath `pathname/*.java`

```
remember, classpath is used by both java compiler as well as java interpreter 

to execute the package assuming class path has been set correctly, using 

```java
import java.com.packagename.ClassName

```



### package naming 

same name in java will always let JVM always picking on its own package first 
so all packagse are suppoed to work.classname confilicts they missed and not be helpful 


if developers are not using proper naming, it will cause problems so always use organization's reverse internet domain name 
```java
edu.stanford.math.addition
```

also components naming conventions includes: 
1. lowercase alphabets, rarely digits 
2. short ~ generally less than 8 characters 
3. meaningful abbreviations util for utilities 
4. acronyms 
5. single word 
6. never start with java or javax 



### Access Level 
provide restriction on accessing classes/interfaces and their members 

inside package
inside&outside packages ~ public 


```java
access_modifier class  ClassName{

}

```

#### accessibility for class members 
inside class ~ private 
```java
private data_type variable = value;
```
inside package only 
```java
data_type variable = value;

```
privage means it is private to class not among objects of classes 



inside package only + any subclass ~ protected 
```java
protected data_type variable = value;

```


inside & outside package ~ public 
```java
public data_type variable = value;

```


## information hiding and  encapsulation 

 mechanism for restricting access to some of the object's components. Your above example is the case of Information Hiding if you make age private.
 in public classes, use accessor methods, not public fields 

 we use setter/mutator and getter/accessor
  ```java
public class ClassName{
    priavte int variable;
    public void setVariable(variable){
        self.variable = variable;
    }
    public data_type getVariable(variable){
        return this.variable;
    }
}

```


```java
public class ClassName{
    priavte int variable;
    public void setVariable(variable){
        if(xxx.equals("something"))
        self.variable = variable;
        else{
            throw new IllegalArgumentException("this is invalid");
        }
    }
    public data_type getVariable(variable){
        return this.variable;
    }
}

```

### minimizig the acess of classes and members 


 

if all data are declared as public then they are tightly coupled 


```java
public class ClassName{
    public int variable;
}

```

Encapsulation is an OOP concept where object state(class fields) and it's behaviour(methods) is wrapped together. Java provides encapsulation using class.

#### tight coupling 

it cannot enforce invariant or range, 
cannot change data representation 

#### loosely coupled system
develop, test, use and optimize in isolation which is useful in multiple projects and decreases risks 

#### rule of thumbs 
design minimal public API of your class and make all other fields private. only make a member default if really need to 

if only one class uses it, make it private nested 

## Static initializer 

initialization needs multiple lines 
1. populating a data structure 
2. initialization with error handling 

multiple initializes execute in order 

```

static ClassName object = initlizeMethod();

priate static ClassName initializeMethod(){
    try{
        return method();
    }catch(Exception e){
        ....
    }
    return null;
}

```

Uff! what is static initializer?

The static initializer is a static {} block of code inside java class, and run only one time before the constructor or main method is called.

OK! Tell me more...

is a block of code static { ... } inside any java class. and executed by virtual machine when class is called.
No return statements are supported.
No arguments are supported.
No this or super are supported.
Hmm where can I use it?

Can be used anywhere you feel ok :) that simple. But I see most of the time it is used when doing database connection, API init, Logging and etc.

Don't just bark! where is example?


```java
package com.example.learnjava;

import java.util.ArrayList;

public class Fruit {

    static {
        System.out.println("Inside Static Initializer.");

        // fruits array
        ArrayList<String> fruits = new ArrayList<>();
        fruits.add("Apple");
        fruits.add("Orange");
        fruits.add("Pear");

        // print fruits
        for (String fruit : fruits) {
            System.out.println(fruit);
        }
        System.out.println("End Static Initializer.\n");
    }

    public static void main(String[] args) {
        System.out.println("Inside Main Method.");
    }
}

```
Output???

Inside Static Initializer.

Apple

Orange

Pear

End Static Initializer.

Inside Main Method.

Hope this helps!



## instance initializer 

we all know that constructors initialize states, but why bother with instance initializer, it can also reference static members 


First of all, there are two types of initialization blocks:

instance initialization blocks, and
static initialization blocks.
This code should illustrate the use of them and in which order they are executed:

public class Test {

    static int staticVariable;
    int nonStaticVariable;        

    // Static initialization block:
    // Runs once (when the class is initialized)
    static {
        System.out.println("Static initalization.");
        staticVariable = 5;
    }

    // Instance initialization block:
    // Runs each time you instantiate an object
    {
        System.out.println("Instance initialization.");
        nonStaticVariable = 7;
    }

    public Test() {
        System.out.println("Constructor.");
    }

    public static void main(String[] args) {
        new Test();
        new Test();
    }
}
Prints:

Static initalization.
Instance initialization.
Constructor.
Instance initialization.
Constructor.
Instance itialization blocks are useful if you want to have some code run regardless of which constructor is used or if you want to do some instance initialization for anonymous classes.


