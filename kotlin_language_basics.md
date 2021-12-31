

# Kotlin Language Basics 

we are gonna improve that iteratively and apply more concepts, we use Kotlin REPL, REPL refers to read evaluate print loop 

Tools -> Kotlin -> Kotlin REPL 

or you can set up IntelliJ 
create a new project -> name it -> create a kt file under src 


```kt
val PI = 3.1415

fun main(args: Array<String>){
    println("hello world")
}

```




## Variables and Data Types 


read-only local variables are defined as keyword `val`. 

```kotlin 
val a: Int = 1; // immediate assigment 
val b = 1; // Int is inferred 
val c: Int; // Type required when no initializer is provided 
c = 3; // deferred assignment  error: val cannot be reassigned




```


variables that can be reassigned use the `var` keyword 

```kotlin
var x = 10;  // 'Int' type is inferred 
x += 1;

```
the main takeaway is if you can make a var to val, you have to redesign your code to make immutable, only make var when it is necessary just in terms of your use case and doamin. 




Bascially any type that you have in java, you have the same type in Kotlin as well. you just need to write uppercase in the beginning 
You should try to avoid use Float and instead use Double because of the machine precision and the troubles that you can run into with float to really compare them securely 
Type safety in Kotlin in Kotlin is a given just like in java 





## Null safety 

in Kotlin, every type is not nullable, meaning you cannot assign Null to it 
you can be sure that you never have a null in there, you also cannot have null pointer exception unless you are interfacing with java code which can of course throw null pointer exceptions 


```java
String str = null;
```

```kotlin
val str : String = null // error

```

### ?
you can use question mark is basically the data type the nullable data type. now notice that this holds for every data type in Kotlin 


```kotlin
val i : Int? = null
val str: String? = null

```
having nulls in your code is that maybe at some point in your code, where you are not sure anymoer that an object is null, kotlin won't give a null pointer exception, the compiler has already seen that is invalid 


### !!
if you use !!, you tell the compiler that you are sure this is not null, and it is your fault if it is indeed null 

it basically looks like you are screaming at the compiler, and this is intentional , this is unsafe call operator 

```kotlin
val str: String? = "hello"
 str!!.length
res5: kotlin.Int = 5

```


## variable?.method or variable?.property -- safety call operator

basically this is like if else, if the object here is null. then any call you do here is just gonna return null, if the object is not null, then it is just gonna execute the method 



```kotlin
val str: String? = null
 str?.length
res3: kotlin.Int? = null

val str: String? = "hello"
 str?.length
res4: kotlin.Int? = 5

```


## ?: operator else if operator 
it is just a shortcut for checking whether the argument here at beginning is null and if it is null, assigining the value back and just having this conditional code 


```kotlin
val str: String? = null
 val lengthOfString = str?.length ?: 0
 println(lengthOfString)
5

val str: String? = null
 val lengthOfString = str?.length ?: 0
 println(lengthOfString)
0
```


so all in all, in theory you could use kotlin code without any nulls at all, but in many cases, you are gonna be interoperating with java code and in those cases, you always have to specify at which points you want to assume a nullable value and at which points you do not want to assume a nullable value 
every type in kotlin is not nullable by default 



## if expression 


```kotlin

if(condition){
    statements
}else if(condition){

}else{

}

```



## when expression 
it is similar to swtich statement in java 

```kotlin
val case = xxx
when(case){
    value1 -> statement1
    in start..end -> statement2
    in start..end -> statement3
    else -> statements default 

}


/*


val number: Int? = 100
 when(number){
     in 0..20->println("it is 0 < x < 20")
     else -> println("it is greater than 20")
 }
*/

```


```kotlin
when{
    conditional statement -> statements
    conditional statement -> statements 
    else -> statements 

}


/*

val number : Int?= 100
 when{
     number?:0 > 100 -> println("number is greater than 100")
     else -> println("number is less than 100")
 }
*/

```



```koltin
val variable = when{
    conditional statement -> statements
    conditional statement -> statements 
    else -> statements 

}

```



## collections 


kotlin collection API builts on top of java API 


in kotlin the main disction is mutable collections and immutable collections 

### intArrayOf()  doubleArrayOf()
```kotlin

val arr = arrayOf(1,2,3,4)
arr.joinToString()
val arr = intArrayOf(1,2,3,4)
val arr = doubleArrayOf()


```

### listOf()


```kotlin 
val listValue = listOf(1,2,3,4)
 listValue[1] = 100
error: unresolved reference. None of the following candidates is applicable because of receiver type mismatch: 
public inline operator fun kotlin.text.StringBuilder /* = java.lang.StringBuilder */.set(index: Int, value: Char): Unit defined in kotlin.text
listValue[1] = 100
^
error: no set method providing array access

```


### mutableListOf()

you do not have to declare the mutableXxxOf as var in order to change the elements in side the collection 
```kotlin
val arr = mutableListOf(1,2,3,4,5)
 arr[1] = 200

```


note the element inside the for in loop cannot be reassigned when iterating through the list

```kt
   for (i in mutableIntArray){
        i = 10
        println(i)

    }

```


### setOf()

```kotlin
val set = setOf(1,1,1,1,2,2,2,3,3,3)
 set
error: a 'val'-property cannot have a setter
set

```

### mutableSetOf()


```kt
val mutable = mutableSetOf(1,2,3,4)
 mutable
res27: kotlin.collections.MutableSet<kotlin.Int> = [1, 2, 3, 4]

  val mutableSetArray = mutableSetOf<Int>(1,2,3,1,2,1,1,1)

    for (i in mutableSetArray){
        println(i)




    }
```
you cannot visit a set by its index


```kt

    val mutableSetArray = mutableSetOf<Int>(1,2,3,1,2,1,1,1)

    for (i in 0..mutableSetArray.size - 1){
        mutableSetArray[i] = 10

        


    }
```


### mapOf(Pair(key, value))

```kt
val map = mapOf(Pair(1,'Java'),Pair(2,'Kotlin'))
error: too many characters in a character literal ''Java''
val map = mapOf(Pair(1,'Java'),Pair(2,'Kotlin'))
                       ^
error: too many characters in a character literal ''Kotlin''
val map = mapOf(Pair(1,'Java'),Pair(2,'Kotlin'))
                                      ^

val map = mapOf(Pair(1,"Java"),Pair(2,"Kotlin"))


```

you cannnot perform this:


```kt
   val mapArray = mapOf<Int, String>(Pair(1,"Eddie"))
    mapArray[2] = "Jack"

```


### mutableMapOf(key to value)
it is actually declared as an infix function, it is expressive syntax using the infix function notation 

```kt
val mutableMap = mutableMapOf(1 to "Java", 2 to "JavaScript")

   val mapArray = mutableMapOf<Int, String>(Pair(1,"Eddie"))
    mapArray[2] = "Jack"

 val mutableMap = mutableMapOf<Int,String>(Pair(1,"Eddie"), Pair(2,"Jack"))

  for ((key,value) in mutableMap){
      println("$key $value")
  }


```

### toList function 
you can easily create copies using the toList function 
this will create a shallow copy and those objects will not be copied recursively 

```kt
// shallow copy 
val list = set.toList()


```

you should always prefer immutable collections, unless you really  do need to change the colletion later on 



## for loops and range start..end both inclusive

```kt
for (i in start..end){
    statements
}

/* this does not exist
for(int i = 0 ; i < 199; i ++){

}

*/


for(c in "string"){
    println("$c")
}

```

it is more like for in loop in java


to iterate through a list 
```kt

val listValue = listOf(1,2,3,4)
for(i in listValue){
    println("$id")
}

```

note in .. are all inclusive 
```kt




fun main(args : Array<String>){
    val intArr = intArrayOf(1,2,3,4)
    var mutableIntArray = mutableListOf<Int>(1,2,3,4,5)

    for (i in intArr){
        println(i)
    }

//    for (i in mutableIntArray){
//        i = 10
//        println(i)
//
//    }
    for (i in 0..mutableIntArray.size - 1){
        mutableIntArray[i] = 10
        println(mutableIntArray[i])

    }


}
```

### downTo function 


```kt
for(i in end downTo start){
    
}

for(i in 10 downTo 1){
     println("$i")
 }

```

### step number


```kt
for(i in end downTo start step number){
    
}

for(i in 10 downTo 1 step 2){
     println("$i")
 }

```


## while loop and do while loop 
it is used when user wants to check certain conditions 

```kt
while(conditional){

}

var value = 0
 while(value < 100){
     println("$value")
     value ++
 }



```

do while loop will continue to check until the condition is true 

```

do {

}while(conditional)


```



## functions 

```kt

fun functionName(argument:Type):ReturnType{

}

fun add(argument1:Int, argument2:Int): Int{
     return argument1 + argument2
 }
 add(1,2)
res36: kotlin.Int = 3

```



### vararg keywords and any method 


```kt
fun functionName(varargs argumentName: Int): ReturnType{
    return argumentName.any {singleArgument -> singleArgument > 10}
}


fun functionName(vararg args: Int) : Boolean{
     return args.any { each_one -> each_one > 1 }
 }
 functionName(1,2,3,4,5)
res37: kotlin.Boolean = true

```



### named arguments & default 


you can also use this to change the order of your arguments by using these explicit names 

```

fun functionName(argumentName: Type, argumentName2:Type = value) 

functionName(argumentName2=value1,argumentName1=value2)

fun functionName(argumentName: Type, argumentName2:Type = value) = statements


```



```kt





fun main(args : Array<String>){

    val result = name()
    println(result)

}


fun name(arg1: Int = 100, arg2: Int = 200) = arg1 + arg2

fun main(args : Array<String>){

val together = concat(listOf("Java","Kotlin","JS"))
    println(together)


}


fun concat(texts:List<String>, separator:String = ",") = texts.joinToString(separator)
```




## exception handling 


checked exception exists in java but not in kotlin based on language design 


all kotlin exceptions are unchecked exceptions 

any exceptions that extends exception does not extend runtime exceptions is called checked exceptions 

checked exceptions need to be declared in a method 


for example, you have to say it in the function signature for an exception in java, you can either do try catch or propogate this exception to another method 
in larger software, exceptions are then propagated along many levels which first of all decreases tracebility but also means higher level of the architecture have to know about many of the exceptions. hence they inherit more problems than they solve problems 

runtime exceptions are unchecked exceptions so we do not hav to add a throws clause 
that is a quick excursion to java 


```java
class Main{
    public static void main(String []args) throws IOException{
        canThrowException();

    }

    static void canThrowException() throws IOException {
        throw new IOException();
    }
}

```


in kotlin, the try catch block is actually an expression 



```kt
import java.io.IOException


fun main(args : Array<String>){

    val input = try {
      getExternalInput()
    }catch (e: IOException){
        e.printStackTrace()
    }finally {
        println("this executes every time")
    }
    println("launched it!")

}


fun getExternalInput() : String{
    throw IOException("you cannot find a file")
}



```















































































