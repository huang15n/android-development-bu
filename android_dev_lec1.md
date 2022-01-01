


#  Basic Concept and Model View Controller 


this section is full of new concepts and moving parts required to build an Android app. 


There are two apps we will create. A quiz app tests the user's knowledge of geography when user presses True or False 






## Concept Basics 


### Activity, Views, Layout, Widgets and View Hierachy 

- An **activity** is an isntance of Activity, a class in the Android SDK. An activity is responsibel for managing user interaction with a screen of information 
you write subclasses of Activity to impelment the functionality that you app requires. A simple application may need only one subclass; a complex app can have many. In our case, activity_main.xml is linekd to MainActivity.java


- a layout defines a set of UI objects and the object's positions on the screen. a layout is made up of defintions written in XML. each defintion is used to create an obejct that appears onscreen, like a button or some text 


in the project tool window, click the discoure arrow next to app, Android studio automatically opens the file activity_main.xml and MainActivity.kt/MainActivity.java in the main view. called the editor tool window or just the edtior 


currently, activity_main.xml holds the default activity layout template. the template changes frequently, 


the default activity layout defines two views: a CosntraintLayout and a TextViews 


**Views** are the bulding blocks you use to compose a UI. everything you see on the screen is a view. views that the user can see or interact with are called **widgets** 

the Android SDK includes many widgets that you can configure to get the appearnce and behaviour you want. every **widget** is an instance of the **View** class or one of its subclasses 

**ViewGroup** is a kind of View that contains and arranges other views. a ViewGroup does not display content itself. Rather it **orchestrates** where other views' content is displayed. ViewGroups are often referred to as **layouts** 




in our case, we need 1 vertical LinearLayout 2 a text view 3 a horizontal linearlyout 4 two Buttons 


every **widget** has a corresponding XML element, and the name of the element is the type of the widget. each element has a set of **XML attributes**. each **attribute** is an instruction about how the widget should be configured 
your **wiget** exits in a hierachy of **View** objects called the view hierachy. in our case, the root element is LinearLayout, when a view is contained by a **ViewGroup** that view is said to be a child of the ViewGroup. 


```xml

<?xml version="1.0" encoding="utf-8"?>
<LinearLayout android:layout_height="match_parent"
    android:layout_width="match_parent"
    android:orientation="vertical"
    android:gravity="center"


    xmlns:android="http://schemas.android.com/apk/res/android">

    <TextView
        android:layout_width="wrap_content"
        android:layout_height="wrap_content"
        android:padding="24sp"
        android:text="@string/question_text"/>


    <LinearLayout android:layout_height="wrap_content"
        android:layout_width="wrap_content"
        android:orientation="horizontal">

        <Button android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/true_button" />


        <Button android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:text="@string/false_button" />
    </LinearLayout>


</LinearLayout>
```

### Widget Attribute 

#### android:layout_width and android:layout_height 
**android:layout_width** and **android:layout_height** attribtues are required for almost every type of widget. they are typically to set either match_parent or wrap_content 


- match_parent view will be as big as its parent
- wrap_content view will be as big as its contents require


#### android:orientation
**android:orientation** attribute on the Layout widgets determines whether their children will apepar vertically or horizontally. The order in which children are defined determins the order in which they apepar onscreen. 


#### android:text
the Button and TextView have android:text, this attribute tells the widget what text to display 

notice that the values of these attribtues are not literal strings. they are references to string resources, as denoted by the @string/ syntax 



#### string resources 
a **string resource** is a string that lives in a separate XML file caleld a string file. you can give a widget a hardcoded string, but it is usually not a good idea. placing strings into a separate file and then reference them is better because it makes localization 


open **res/values/string.xml**.the template has already added one string resources. add others ones 

```xml 
<resources>
    <string name="question_text">Hello</string>
    <string name = "true_button">True</string>
    <string name = "false_button">False</string>
</resources>

```



### XML to View Objects 

how do XML elements in activity_main.xml become view objects? it starts in the MainActivity classes. 

when a project is created, a subclass of Activity named MainActivity.java/kt was created for you. the class file for MainActivity.java/kt is in the app/java directory of the project, the java directory is where the java/kotlin code for your project lives 

a quick aside about directory name: this directory is called java because android originally supported only java code. Because you configured it to use Kotlink and Kotlin is fully **interoperable** with java, the java directory is where Kotlink lvies as welll. you could create a kotlin directory and place your kotlin fiels there, but you would have to tell android that the new folder includes source files so they would be included in your project. in most cases, separating your source fiels based on their language provides no benefits, so most project just plave their kotlin files in the java directory 

```java
package com.windsor.hello;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;

public class MainActivity extends AppCompatActivity {

    @Override
    protected void onCreate(Bundle savedInstanceState) {
        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
    }
}

```

```kotlin

package com.windsor.hellokt

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle

class MainActivity : AppCompatActivity() {
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
```


if you are not seeing all of the import statements, click the + symbol to the left of the first import statement to reveal the others 



**AppCompatActivity** is subclass of Android's **Activity** class that provides compatibility support for older version of android 

**onCreate(Bundle?)** or **onCreate(Bundle savedInstanceState)** is called when an instance of the activity subclass is created. when an activity is created, it needs a UI to mange. to give the activity its UI, you can **Activity.setContentView(layoutResID: Int).** or **public void setContentView(int layoutResID)**

this function **inflates** a lyaout and puts it onscreen, when a layout is infalted, each widget in the layout file is instantiated defined by its attributes. you specify which layout to inflate by passing in the layout's resource ID 


## Resource and resource IDs 
**layout** is a **resource**. a **resource** is a piece of your app that is not code -- things like image, files, audio and xml files 

resources for your project live in a subdirectory of the app **/res** directory. in the project tool widnow, you can see the activity_main.xml lvies in **res/layout/**. you string files, which contains string resources lives in **res/values**

the access a resource in code, you use its resource ID, the resource ID for your layout is R.layout.activity_main 


in android studio , this project tool window hides the true directory structure of your android proejct so that you can focus on the files and folders that you need most often. After making making a change to your resources, you may not see the file instantly updated. 



the R.java file can be large, this is where the R.layout.activity_main comes from -- it is an integer constant named activity_main where the layout inner class of R 

Android geenrates a resource ID for the entire layout and for each string, but it did not generate resource IDs for the invididual widgets in the activity_)main.xml. not every widget needs a resource ID. 


add ID to your buttons :

```xml
        <Button android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/true_button"
            android:text="@string/true_button" />


        <Button android:layout_width="wrap_content"
            android:layout_height="wrap_content"
            android:id="@+id/false_button"
            android:text="@string/false_button" />

```


### wiring up widgets 


you are ready to wire up your button widgets, this is a two step process 
1. get refernces to the inflated View objects 
2. set listeners on those objects to respond to user actions 


in java, add two variables, you will fix the error just in a second, do not use code completion, type in yourself. 

in an acitiy, you can get a reference to an infalted widget by calling the following Activity method: 

 java:
***public View findViewById(int id)***

kotlin:
*** Activity.findViewById(Int)***

 



```java

package com.windsor.hello;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.widget.Button;

public class MainActivity extends AppCompatActivity {
    private Button mTrueButton;
    private Button mFalseButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mTrueButton = findViewById(R.id.true_button);
        mFalseButton = findViewById(R.id.false_button);
    }
}

```


```kotlin

package com.windsor.hellokt

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.widget.Button

class MainActivity : AppCompatActivity() {
    private lateinit var trueButton: Button
    private lateinit var falseButton: Button
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
    }
}
```

you may need to get rid of those pesky errors when mouse over the red error indicator: Unresolved references: you could type import statement at the top or you can just do it the easy way and let Android Studio do it for you. *press option-return / alt +enter to let the intellij magic under the hood amaze you*. this should get rid of the errors. once your code is error free, it is time to make your app interactive 




in the codes above, you use the resource IDs of your widgets to retrive the infalted obejct and assign them to your view properties, since the view obejcts are not infalted into and available in memory until after **setContentView(...)** is called in **onCreate(...)**, you use lateinit on your property declarations to indicate the compielr that you will provide a non-null View value before you attemp to use the contetnts of the proeprty. then, in **onCreate(..)** you look up and assign the view obejcts the appropriate properties. 


### setting listeners and make toasts 

***Android application are typically event driven***. unlike command line programs or scripts, event-driven apps start and then wait for  an event -- such as pressing a button, events can also be initiated by the OS or another app, but user-initiated events are the most obvious 


when you app is waiting for a specific event, we say that is *listening for* that event. the object that you create to respond to an event is called a listener, and the lsitenr implements a **listener interface** for that event 


the Android SDK comes with lsitener interface for various events, so you do not have to write your own. 
in this case, the event you want to lsiten for is a button being pressed or clicked, so you listener will implement the **View.OnClickListener** interface 


now to make the button **fully armed and operational**. you are going to press of each button trigger a pop message called a toast. 
a ***toast*** is a short message that informs the user of something but does not require any input or action. 


add toast message in the res/values/strings.xml


```xml
<resources>
    <string name="question_text">Hello</string>
    <string name = "true_button">True</string>
    <string name = "false_button">False</string>
    <string name = "correct_toast"> Correct! you rock! </string>
    <string name = "wrong_toast"> Wrong! you suck </string>
</resources>

```






in java, this lsitener is implemented as anonymous inner class, the syntax is tricky, but it helps to remember that everythign within the outermost set of parentheses is passed into setOnClickListener(onClickListener). within the parentheses, you create a new, nameless class and pass its entire implementation. Because your anonymous class implements OnClickListener, it must implement that interface’s sole
method, onClick(View). You have left the implementation of onClick(View) empty for now, and the
compiler is OK with that. A listener interface requires you to implement onClick(View), but it makes
no rules about how to implement it
(If you have a View cannot be resolved to a type error, try using Option+Return (Alt+Enter) to import
the View class.)



use the code completion to help you fill in the lsitener code, code compeltion can save you a lot time, so it is good to become familar with it early 
to choose one of the suggestions, use the up and down arrow keys to select if you want to ignore code completion, you could just keep typing. it will not compelte anything for you if you do not presse the tab key, press the return key, or click onthe pop up widnwo 

From the list of suggestions,  select **makeText(Context context, int resID, int duration)**. Code
completion will add the complete method call for you.

let's open a new landscape and possibility 



in java. in makeText(....), you pass the instance of the AppName as the Context argument. however, you cannot simply pass the variable `this` as you might expect. at this point in the code, you are defiing the anoymous class where this refers to the *View.OnClickListener*

```java
package com.windsor.hello;

import androidx.appcompat.app.AppCompatActivity;

import android.os.Bundle;
import android.view.View;
import android.widget.Button;
import android.widget.Toast;

public class MainActivity extends AppCompatActivity {
    private Button mTrueButton;
    private Button mFalseButton;

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);
        mTrueButton = findViewById(R.id.true_button);
        mFalseButton = findViewById(R.id.false_button);

        mTrueButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(MainActivity.this, R.string.correct_toast, Toast.LENGTH_LONG).show();
            }
        });
        
        
        mFalseButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                Toast.makeText(MainActivity.this, R.string.wrong_toast, Toast.LENGTH_LONG).show();
            }
        });
    }

}

```

in kotlin to create a toast, we call the static function Toast.makeText(Context!,Int,Int) this function creates and configures a Toast object. the Context parameter is typically an isntance of Acitivity and Activity is a subclass of Context. 


the second parameter is the resource ID of the string that toast should dispaly. the Context is needed by the Toast class to be able to find and use the string's resource ID. the third parameter is one of the two Toast constants that specify how long the toast should be visible 

after you have created a toast, you call Toast.show() on it to get it onscreen. because you used code compeltion, you do not have to do anything to import Toast clsas. when you accept a code completion suggestion, the necessary classes are imported atuomatically, let's see it in action 

```kotlin

package com.windsor.hellokt

import androidx.appcompat.app.AppCompatActivity
import android.os.Bundle
import android.view.View
import android.widget.Button
import android.widget.Toast

class MainActivity : AppCompatActivity() {
    private lateinit var trueButton: Button
    private lateinit var falseButton: Button
    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_main)
        trueButton.setOnClickListener(View.OnClickListener {
            Toast.makeText(this,R.string.correct_toast, Toast.LENGTH_LONG).show()
        })
        falseButton.setOnClickListener(View.OnClickListener {
            Toast.makeText(this, R.string.wrong_toast, Toast.LENGTH_LONG).show()
        })
    }
}

```



the app crashes when launching or when you press a button, useful information will appear in the Logcat tool window. if logcat did not open automatically when you ran the app, you can open it by clicking the Logcat button at the bottom of the android window. look for exceptions in the log; they will be an eye-catching red color 



### Android Build process 
by now, you probably have soem burining question about how build process works. You hae already seen that Android Studio builds your project autoamtically as you modify it, rather than on command 

during the build process, the tools take your resources, code, and AndroidManiest.xml file withich contains metadata about the app and turn them into an .apk file. this file is then signed with a debug key, which allows it to run on the emulator. ***to distribute your .apk to the masses***, you have to sign it with a release key. 

ClassLoader.loadClass you can also crete your view clsses programmatically in the activity instead of defining them in XML, but there are benefits to separating your presentation from the logical of the app. the main one is taking advantage of configuration changes built into the SDK 

AndrooidManitest|res/ -> asset -> gen/ R.java | src/ -> compile java -> java bytecode class -> cross compile to dalvik 

asset packing tool aapt -> compile resources 

dalvik + comipled resources -> build and sign apk -> android package apk -> install and run 





### build tools 
the build is integrated into the IDE - it invokes standard android build tool like aapt2, but the build process itself is managed by Android Studio 

you may, for your own reasons , want to perform builds from outside of android studio. the easist way to do this is to use command line build tools. The android build system sues a tool called gradle 


read along but do not be concerned if you are not sure why you might want to do this or if the command below do not seem to work, coverage of the ins and outs of using the command is beyond the scope 


the use Gradle from the command line, navigate to your project's directory and run the following command 


```shell

# ./gradlew tasks 
# gradlew.bat tasks

```

this will show you a list of avaiable tasks you can execute. the one you want is called installDebug make it so with a command liek this 


```shell

# ./gradlew installDebug
# gradlew.bat installDebug

```

this will install your app on whatever device is connect, howevver, it will not run hte app. for that, you will need to pull up the launcher and launch the app by hand 

I cannot encourage you enough to take on these challenges, tackling them cements what you have learned, builds confidence in your skills, and bridgets the gap between prorgamming and on your own. if you get stuck while working on it, take a break, and come back to try again fresh. 


##### main takeaways for prorgamming 
1. Kotlin private lateinit var variable 
2. this keyword in anoymous inner class for java is different from kotlin 



## Android and Model View Controller 
