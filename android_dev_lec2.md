
# Activity Lifecyle and Persisting UI state 


## TODO ADD KOTLIN 


Your app works great until you rotate the device. The dreaded cause -- and very common -- rotation problem. how to leverage the mechanics underlying the rotation problem to display an alternate layout with device is in landscape mode. if the emulator does not rotate after you press one of the rotate buttons, turn auto-rotate on. swipe down from the top of the screen to open Quick Settings. press auto-rotate icon, which is the third icon from the left, the icon will change from grayed out to a teal color to indicate that auto rotate is now on  



every instance of Activity has a lifecyle. During this lifecyle, an activity transitions between four states: nonexistent, resumed, paused, stopped(previously three running, paused, stopped). for each transition, there is an Activity method that notifies the activity of the change in its state 


      Nonexistent 
               
onCreate()       onDestroy()
 _____________________________       entire lifetime, instance in memory    
       Stopped       
onStart()       onStop() 
________________________________  visible life time, vifew partially or fully visibel to user
        Paused 
onResume()      onPause() 
____________________________          foreground lifetime user interacting with this activity 
       Resumed     

               
| State  | in memory | visible to user  | in foreground |
| ------------- | ------------- | ------------- | ------------- |
| nonexistent  | no  | no  | no  |
| stopped  | yes  | no  | no  |
| paused  | yes | yes/partially | no  |
| resumed  | yes  | yes  | yes  |

- nonexistent represents an activity that has not been launched yet or an activity that was just destroyed by the user pressing the back button. for that reason, this state is sometimes referred to as the destroyed sate. there is no instance in memory, and there is no associated view for the user to see or interact with 


- stopped represents an activity that has an instance in memory but whose view is not visible on the screen. this state occurs in passing when the activity is first spinning up and reoccurs anytime the view is fully **occluded** such as when the user launches another full screen activity to the foreground, presses the home button, or uses the overview screen to switch tasks 



- paused represents an activity that is not active in the foreground but whose view is visible or partially visible. an activity would be partially visible, for example, if the user launched a new dialog themed or transparent activity on top of it. an activity could also be fully visible but not in foreground if the user is viewing two activity in multiple window mode also called split-screen mode 


-- resumed represents an activity that is in memory, fully visible, and in the foreground. it is the activity the user is currently interacting with. only one activity across the entire system can be in the resumed state at any given time. that means that if one activity is moving into the resume state, another is likely moving out of the resumed state 




you are **acquianted** with one of these lifecyle callback function -- onCreate(Bundle). the os calls this function after the activity is created but before it is put onscreen 


typically. an activity overrides onCreate(Bundle) to prepare the specifics of its UI 
1. inflating widgets and putting them on screen 
2. getting references to inflated widgets
3. setting listenrs on widgets to handle user interaction
4. connecting to external model data 


it is important to understand that you never call onCreate(Bundle) or any of the other Activity lifecylcel functions yourself. you simply override the callbacks in your activity subclass. then android calls the lifecyle callbacks at the appropraite time in relation to what the user is doing and what is happening across the rest of the system to notify th activity that its state is changing 


### Logging the activity lifecyle 

override lifecyle functions to cavesdrop on MainActivity's lfiecyle. each implementation will simply log a message informing you that the function has been called. 




### making log messages 

android.util.log class sends log messages to a shared system level log. Log has several functions for logging messages. here is the one we use most often: 

```
public static int d(String tag, String msg)

```

the d stands for debug and refers to the level of the log message.

the first string is typically a TAG constant with the class name as its value. this makes it easy to determine the source of a particular message 


```java

    
    private static final String TAG = "MainActivity";



    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Log.d(TAG,"onCreate() ");
    }

```


```kt
    private const val TAG = "MainActivity"



    override fun onCreate(savedInstanceState: Bundle?) {
        Log.d(TAG,"onCreated(Bundle?) is called ")

    }

```


now override five more lifecycle functions in MainActivity by adding the following after onCreate(Bundle). 

```kt


    override fun onStart() {
        super.onStart()
        Log.d(TAG, "onStart() is called")
    }

    override fun onResume() {
        super.onResume()
        Log.d(TAG, "onResume() is called")
    }

    override fun onPause() {
        super.onPause()
        Log.d(TAG, "onPause() is called")
    }

    override fun onStop() {
        super.onStop()
        Log.d(TAG,"onStop() is called")
    }

    override fun onDestroy() {
        super.onDestroy()
        Log.d(TAG,"onDestroy() is called")
    }

```

notice that you call the superclass implementation before you log your messages. These superclass calls are required. calling the superclass implementation should be the first line of each callback function override implementation 

```java

  @Override
    protected void onStart() {

        super.onStart();
        Log.d(TAG,"onStart() is called");

    }

    @Override
    public void onResume(){
        super.onResume();
        Log.d(TAG,"onResume() is called");


    }

    @Override
    public void onPause(){
        super.onPause();
        Log.d(TAG,"onPause() is called");


    }


    @Override
    protected void onStop(){
        super.onStop();
        Log.d(TAG,"onStop() is called");


    }

    @Override
    protected void onDestroy(){
        super.onDestroy();
        Log.d(TAG,"onDestroy() is called");


    }


```


### log levels 

when you use the android.util.log class to send log messages, you control not only the content of a message but also a level that specifics how important the message is. Android support five log levels. each level has a corresponding function in the Log class. sending output to the log is simple as calling the correspdonig log function 


| Log Level  | Function | Used for |    
| ------------- | ------------- | ------------- |  
| ERROR  | Log.e(...)   | errors  |
| WARNING | Log.w(...)  | warnings  |
| INFO | Log.i(...)  | informational messages  |
| DEBUG | Log.d(...)  | debug ouput may be filtered out  |
| VERBOSE | Log.v(...)  | development only   |


### Activity Lifecyle responds to user actions 
onCreate(Bundle?), onStart(), and onResume. when app was launched and the intial instance of MainActivity was created 
2022-01-02 23:24:35.997 6706-6706/com.windsor.hello D/MainActivityEddie: onCreate() 
2022-01-02 23:24:36.509 6706-6706/com.windsor.hello D/MainActivityEddie: onStart() is called
2022-01-02 23:24:36.514 6706-6706/com.windsor.hello D/MainActivityEddie: onResume() is called

as you continue through, you will override the different activity lifecyle functions to do real things for you app. for now, have some fun familiarizing yourself with how the lifecyle behaves in common usage scenarios by interacting with you app and checking out the logs in the Logcat 

in addition, each of the logging function has two signarue: one that takes a TAG string and a message string, and a second that takes those two argumetns plus an isntance of Thrwoable, which makes it easy to log information about a particular exception that you app might throw 

### Temporarily leaving an activity 

< Back button 
o  home 

if the app is running, press home button. the Home screen disdplays, and MainActivity mvoes completely out of view. you activity received calls on onPause() and onStop() 
by presing the Home button, the user is telling Android, go look at something else, but I might come back. I am not really done with this screen yet. android pauses and ultimately stops the activity 



2022-01-02 23:28:40.999 6706-6706/com.windsor.hello D/MainActivityEddie: onPause() is called
2022-01-02 23:28:41.795 6706-6706/com.windsor.hello D/MainActivityEddie: onStop() is called


so after you press the Home button, your instance of MainActivity hangs out in the stopped state in memory, not visible, and not active in the foreground. android does this so it can quickly and easily restart MainActivity where you left off when you come back to it. 
Keep in mind that this is not the whole story about pressing the Home button. Stopped app can be destroyed at the discretion of the OS 

[] recent button, each card in the overview screen represents an app the user has interacted with in the past 
a quick look at logcat shows your activity got calls to onStart() and onResume(). note that onCreate() was not called. this is because MainActity was in the stopped state after the user pressed the Home button. because the activity instance was still in memory, it did not need to be created. instead, the activity only had to  be started. move to the pause/visibel state and then resumed mvoed to the resume/foreground state 

2022-01-02 23:31:18.488 6706-6706/com.windsor.hello D/MainActivityEddie: onStart() is called
2022-01-02 23:31:18.489 6706-6706/com.windsor.hello D/MainActivityEddie: onResume() is called


ealier we said that it is possibel for an activity to hang out in the paused state, either partially visble such as a new activity with either a transparent background or a smaller than screen size is launched on top or fully visible in multi window mode. 

multi window mode is only availbale on Android 7 or higher, select split screen 
to exit multi window mode, swipe the window separtor in the middle of the screen down to the bottom of the screen to dismiss the bottom window 



### Finishing an activity 
press the back button on the device and then check Logcat. your activity received calls to onPause(), onStop(), and onDestroy(). your MainActivity instance is now in nonexistent state 

when you pressed the back button, you as the user of the app finished the activity. in other words. you told android, i am done with this activity. android then destroyed your activity's view and removed all traces of the activity from memory. this is android's way of being frugal with your device's limtied resourcse 

another way the user can finish an activity is to swipe app's card from the overview screen. 


as a developer, you can programmatically finish an activity by calling 

```java
Activity.finish();

```



## Rotate the screen

when you rotate the device(fn+ctrl+f12/ctrl+f12), the instance of MainActivity you wre looking at was destroyed, and a new one was created. rotate the device again to witness another round of destrunction and rebirth 

each time you rotate the device, the current MainActivity instance is completely destroyed. the value that was stored in that instance is wiped from memory. 

before making the fix, take a closer look at why the OS destroys your activity when the use rotate the screen 


### device configuration changes and activity lifecyle 
rotating the device changes the configuration. 
**the device configuration** is a st of characteristics that describe the current state of an individual device. the characteristics that make up the configuration include screen orientation, screen density, screensize, keyboard type, dock mdoe, language and more 

typically, app provide alternative resources to match device configurations. 
when a runtime configuration change occurs, there may be resources that are a better match for the new configuration. so android destorys the activity, looks for resources that are the best fit for the new configuration, and then rebuilds a new isntance of the activity with those resources. 

to set this in action, create an landscape mode, android will create the res/layou-land/folder in your projeect and palce a enw layout file named activity_main.xml in the new folder. swtich the project tool window to the project view to see the files and folders as they actuallly are. as you have seen, configuration qualifers on res subdirectires are how android identifiers which resoruces best mnatch the current device configuration. the land suffix is another example of a configruation qualifier. 


you now have a landscape layout and a default layout. when the device is in landscape orientation. android will find and use layout resource in the res/layout-land directory. otherwise, it will stick with the default res/layout. note that the two layout fiels must have the same filename so that you can be referenced with the same resource ID 


 


 ### UI updates and multi-window mode 
prior to android 7.0 most activities spent very little time in the pasused state. instead, activites passed through the paused state quickly on their way to either the resume state or stopped state. because of this , many developers asumed they only need to update their UI when their ativity was in the resumed state 

it was common pratice to use onReumse() and onPause() tostart or stop any ongoing related to the UI such as animation or data refereshes 


when multiwindow mode was introduce, it broken the assumption that resumed activies were the only fully visible activties.this is ,in turn, broke the intended behaviour of many apps. now, pasued activities can be fully visible for extended periods of tiem when the user is in multiwindow mode. and users will expect those paused activites to behave as it they were resumed 


multi-window mode comes along, but you app stops playback when it is pasued and user are interacting with anotehr app in the second window. users start complaining, because they want to watch their vidoes while they send a text in a separate window 


luckily, the fix is relatively simple: move your playback resuming and pausing to onStart() and onStop(). this goes for any live updating data, like a photo gallery app tha refreshes to show new images as they are pused to a flickr stream 


unfortunately, not everyone got the memo, and many apps still misbeahve in multiwindow mode, to fix this, introduced a spec to support multi-resume for multi-window mode. .it means that the fully visible activity in each of the windows will be in the resumed state when the device in multi-window mode, regarldelss of which window the user last touched 


you can opt in to using multi resume mode for you app . even if you opt in, multi-resume will only work on device whose manufaceturer implemented the multiresume spec. and, as of this writing, no device on the market implement it. however, there are rumours that the spec will become mandatory 


until multi-resume becomes a readily avaible standard across most devices in the marketplace, use your knowledge of the activity lfiecyle to reason about where to place UI update code. you will get a lot of practice doing so throughout the course of this 




# Persisting UI state 

android does a great job of providing alternative resources at the right. howver, reverting back to the initial value : destroying and re-creating activties on rotation can cause headaches 


## Save data across rotation  

## way 1: Including the ViewModel Dependency 
in a moment you are going to add a ViewModel class to yoru project. the ViewModel class comes from android lirbary called lifecyle-extemsopm. pme pf ,amu ;onrar. you must first include the library in the list of dependencies for your project 


project's dependencies live in a file called build.gradle, gradle is the build too. 

with android view enabled, expand gradle scripts and take a look at the content. your project actually comes with two build.gradle files: one for the project as a whole and one for your app module. 


the first line in the dependencies specifies that the project depends on all of the .jar files in its libs directory. the other lines lsit libraries that were automatically included in your project based on the settings you selected when you created it 

add lifecyle-extensions depedency to app/build/gradle file 
its exat placement in the dependencies does not matter, but to keep thigns tidy it is good to put new dependencies under the last exiting implementation dependency 

```
dependencies {

    implementation 'androidx.appcompat:appcompat:1.4.0'
    implementation 'com.google.android.material:material:1.3.0'
    implementation 'androidx.constraintlayout:constraintlayout:2.0.4'
    implementation 'androidx.lifecycle:lifecycle-extensions:2.0.0'
    testImplementation 'junit:junit:4.+'
    androidTestImplementation 'androidx.test.ext:junit:1.1.3'
    androidTestImplementation 'androidx.test.espresso:espresso-core:3.4.0'
    
}

```


when you make any change to  build.gradle, android studio will prompt you to sync the file 



### Adding a ViewModel

a **VuewNidek** is related to one particular screen and is a great place to put logic involved in fomrating the data to display on that screen 

a **ViewModel** holds on to a model object and decoartes the model - adding functionality to display onscreen that you might not want in the model itself 

using a ViewModel aggreates all the data the screen needs in one place, formats the data, and makes it easy to access the end result 


**ViewModel** is part of the androidx.lifecyle package , which contains lifecyle-related APIs including lifecyle-ware component.
**lifecylc-aware** component observe the lifecyle of some other component, such as an activity, and take the state of that lifecycle into account 


google created the androidx.lifecycle pacakge and its contetns to make dealing with the activity lifecyle and other lifecyle a little less painful 

create a new file -> xxViewModel select Class from the kind dropdown. 

```java
package com.windsor.hello;

import android.util.Log;
import android.view.View;

import androidx.lifecycle.ViewModel;




public class MainViewModel extends ViewModel {

    private final static String TAG = "MainViewModel";
    
    {
        Log.d(TAG,"ViewModel Instance Created");
    }

    @Override
    protected void onCleared() {
        super.onCleared();
        Log.d(TAG,"ViewModel instance about to be destroyed")
    }
}


```

the onCleared() method is caleld just before a ViewModel is destroyed, this is a useful place to perform any cleanup, such as unobserving a data source. 
simply log the fact that ViewModel is about to be destroy 


### Accessing ViewModel from Main controller 


```java
MainViewModel provider = new ViewModelProvider(this).get(MainViewModel.class);


```

the ViewModelProviders class provides instance of the ViewModelProvider class, you call to ViewModelProvier.of(this) creates and retrurns a ViewModelProvider associated with the activity 

ViewModelProvider no plural, on the other hand, provides instance of ViewModel to the activity calling provider.get() return an instance of MainViewModel. you will most often see these functions chain togther like so

```java
ViewModelProviders.of(this).get(MainViewModel.class)

```

the ViewModelProvider acts like a registry of ViewModels. whe nthe activity queries from a ViewModel for the first time, ViewModel provider creatse and return a new MainViewModel instance. when the activity queries for MainViewModel after a configruation change, the instance was first created is returned. when the activity is finished such as when the user presses back button, the ViewModel-Activity pair is removed from memory 



### ViewModel lifecyle and ViewModelProvider

activties transition beween four sate, resumed, paused, stoppedand nonexistent. different ways an activity can be destroyed: either by user finishing the activity or by the system destroying it as a result on a configruation change 

when the user finsihes an activity, they expect their UI state to be reset. when the user rotates an activityl they expect their UI sate to be the same before and after rotation 

you can determine which of these two scenarios is happening by checking the activity's isFinishing property. if isFinishing is true, the activity is being destroyed because the user finished the activity if isFinishing is false, the activity is being destroyed by the system because of a configruation change 


but you do not need to track isFinishing and preverse UI state mnually when it is false just to meet your user's expection. instead, you can use a ViewModel to keep an activity's UI state data in memory across configuration changse. A ViewModel's liecyle more closely mirros the user's expection; it surives configuration changes and is destroyed only when its associated activity is finished 


you associate a ViewModel instance with an activity's lifecyle, the ViewModel is then said to be scoped to that activity's lifecyle. this means the ViewModel will remain in memory, regardless of the activity's sate, until the activity is finished 


MainActivity.OnDestroy() is caleld -> Activity.isFinishing -> no_ stays in memory / yes ViewModel is destroyed 


this means that ViewModel stays in memory during a ocnfiguration change, such as rotation. during the configruation, the activity instance is destroyed and recreated but when the ViewModels scoped to the activity stay in meory 

2022-01-04 21:53:59.643 8737-8737/com.windsor.hello D/MainActivityEddie: onStop() is called
2022-01-04 21:53:59.644 8737-8737/com.windsor.hello I/MainActivityEddie: onSaveInstanceState
2022-01-04 21:53:59.645 8737-8737/com.windsor.hello D/MainActivityEddie: onDestroy() is called

the relationship between MainActivity and ViewModel is unidrectional. the activity refernces the ViewModel, but the ViewModel does nto access the activity. your ViewModel should never hold a reference to an activity or a view, otherwise you will introduce a ***memory leak***


a memory leak occurs when one object holds a strong reference to another object that should be destroyed. holding the strong refernce pevents the garbage collector from clearing the obejct from meory. memory leaks due to a configruation change are common bugs.
you ViewModel instance stays in memory across rotation, while your original activity instance gets dstroyed. if the ViewModel held a strong reference to the original activity isntance, two problems would occur: first, the original activity instance would nto be removed from memory, and thus the activity would be leaked. second, the ViewModel would hold a refernce to a stale activity. if the ViewModel tried to update the view of the stale activity, it would trigger an IllegalStateException 


### Add data to your ViewModel 

you can stash the activity's UI state data in the ViewModel instance and it, too will surive rotation
along with all the logic related to them, begin by cutting the properties from MainActiviy 

```java
// copy to xxxViewModel
    private Question [] mQuestionBank = new Question[]{
            new Question(R.string.question_one, true),
            new Question(R.string.question_two, false),
                new Question(R.string.question_three, false),
                new Question(R.string.question_four,true),
                new Question(R.string.question_five,false), };
    private int mCurrentIndex = 0;


```
remove the private access modifier so property value can be accessed by external classes, such as MainAcitity. leave the private access modifier on the array will not interact with that directly. instead, it will call functiosn and computed proeprties you will add to xxViewModel 

delete the initialzation block and onCleared() logging, as you will not use them again  

now add a method to xxViewModel to advance to the next. also, add computed properties to return the text and answer for the current question 


```java

package com.windsor.hello;

import android.util.Log;
import android.view.View;

import androidx.lifecycle.ViewModel;

import com.windsor.hello.Models.Question;


public class MainViewModel extends ViewModel {

    private final static String TAG = "MainViewModel";
    private Question[] mQuestionBank = new Question[]{
            new Question(R.string.question_one, true),
            new Question(R.string.question_two, false),
            new Question(R.string.question_three, false),
            new Question(R.string.question_four,true),
            new Question(R.string.question_five,false), };
     int mCurrentIndex = 0;


     public boolean currentQuestionAnswer(){
         return mQuestionBank[mCurrentIndex].isAnswerTrue();
     }

     public int currentQuestionText(){
         return mQuestionBank[mCurrentIndex].getTextResId();
     }

     public void moveToNext(){
         mCurrentIndex = (mCurrentIndex + 1) % mQuestionBank.length;
     }



}

```

we said that a ViewModel stores all the data and its assoicated screen needs, formats it, and make it easy to access. this allows you to remove presentation logic from the activity, which in turn keeps your activity simpler. and keeping activities s simple as possibel is a good thing: any logic you put in your activity might be unintentionally affected by the activity's lifecle. also, it allows the activity to be responsibel for handlign only what appears on the screen, not the logic behind determing the data to display 


update these methods shortly to call through the new xxViewModel computed properties you added. but you will keep them in MainActivity to help keep your activity code organized 



kotlin 
add a lazily initialized propety to stash the xxViewModel instance associated with the activity 
using by lazy allows you to make the xxViewModel propety a val instead of a var. this is great because you only need and want to grab and store the xxViewModel when the acitivity insance is created -- so xxViewModel should only be assigned a value one time 

more important, using by lazy means the xxViewModel calculation and assignment will not happen until the first time you access xxViewModel. this is good because you cannot safely access a ViewModel until Activity.onCreate if you call ViewModelProvider.of(this).get(xxxViewModel.class) before Activity.onCreate() you app will crash with an IllegalStateException 


finally, update MainActivity to display content from and interact with your newly updated xxViewModel 

```java
// MainActivity.java

package com.windsor.hello;

import androidx.appcompat.app.AppCompatActivity;
import androidx.lifecycle.ViewModelProvider;

import android.os.Bundle;
import android.util.Log;
import android.view.View;
import android.widget.Button;
import android.widget.TextView;
import android.widget.Toast;

import com.windsor.hello.Models.Question;

public class MainActivity extends AppCompatActivity {
    private Button mTrueButton;
    private Button mFalseButton;
    private Button mNextButton;
    private TextView mQuestionText;


    private static final String TAG = "MainActivityEddie";

    private MainViewModel provider;









    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Log.d(TAG,"onCreate() ");


        super.onCreate(savedInstanceState);
        setContentView(R.layout.activity_main);

       provider = new ViewModelProvider(this).get(MainViewModel.class);


        mTrueButton = findViewById(R.id.true_button);
        mFalseButton = findViewById(R.id.false_button);
        mNextButton = findViewById(R.id.next_button);
        mQuestionText = findViewById(R.id.question);

        mQuestionText.setText(provider.currentQuestionText());


        mTrueButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {

                checkAnswer(provider.currentQuestionAnswer(), true);

            }
        });


        mFalseButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                checkAnswer(provider.currentQuestionAnswer(), false);


            }
        });

        mNextButton.setOnClickListener(new View.OnClickListener() {
            @Override
            public void onClick(View view) {
                provider.moveToNext();
                updateQuestion();

            }
        });
    }

    @Override
    protected void onStart() {

        super.onStart();
        Log.d(TAG,"onStart() is called");

    }

    @Override
    public void onResume(){
        super.onResume();
        Log.d(TAG,"onResume() is called");


    }

    @Override
    public void onPause(){
        super.onPause();
        Log.d(TAG,"onPause() is called");


    }


    @Override
    protected void onStop(){
        super.onStop();
        Log.d(TAG,"onStop() is called");


    }

    @Override
    protected void onDestroy(){
        super.onDestroy();
        Log.d(TAG,"onDestroy() is called");


    }




    private void updateQuestion(){

        mQuestionText.setText(provider.currentQuestionText());

    }

    private void checkAnswer(boolean answer, boolean response){
        if(answer == response){
            Toast.makeText(MainActivity.this, R.string.correct_toast, Toast.LENGTH_LONG).show();


        }else{
            Toast.makeText(MainActivity.this, R.string.wrong_toast, Toast.LENGTH_LONG).show();

        }

    }

}

```
do a happy dance to celebrate solving the UI state loss on rotation bug. but do not dance too long. there is another, less-easily-discouverable bug to squash 






## way2: Overriding onSaveInstanceState(Bundle)

one way to do this to override the Activity method: 
```java
protected void onSaveInstanceState(Bundle outstate)

```

this method is normally called by the system before onPause(), onStop(), and OnDestroy()
the default implemtation of onSaveIstanceState() directs all of the activity's views to save their state as data in the Bundle object.

a **Bundle** structure that maps tring keys to values of certain limtied types, you have seen this Bundle and it is passed into onCreate(Bundle)


```java 
@Override 
public void onCreate(Bundle saveInstanceState){

}


```


when you override onCreate, you call onCreate on the activity's superclass and pass in the bundle you jsut received, in the superclass implementation, the saved state of the views is retrieved and used to recreate the activity's view hierachy 




you can override onSaveInstanceState to save additional data to the bundle and then read that data back in onCreate. this is how you are going to save the value.

add a constant that will be the key for key value pair that will be stored in the bunddle 

java: 

```java
    private static final String KEY_INDEX = "index";
    @Override
    public void onSaveInstanceState(Bundle savedInstanceState){
        super.onSaveInstanceState(savedInstanceState);
        Log.i(TAG, "onSaveInstanceState");
        savedInstanceState.putInt(KEY_INDEX, mCurrentIndex);
    }

    @Override
    protected void onCreate(Bundle savedInstanceState) {

        Log.d(TAG,"onCreate() ");
        
        if(savedInstanceState != null){
            mCurrentIndex = savedInstanceState.getInt(KEY_INDEX,0);
        }
    }

```


to fix this bug, the post rotation MainActity instnaces need to know the old value, you need a way to save this data across a runtime configuration changse, like rotation 

You will fix this state loss on rotation bug by storing its UI data in a ViewModel. you will also addrss a less easily discoverable, but equally problematic bug - UI state loss on process death - using android saved instance state mechanism 



the newly minted saveInstanceState method will remember what the value was. note that the types that you can save to and restore from a Bundle are primitive types and classes that implement the **Serializable or Parcelable** interface. it is usually a bad pratice to put obejcts of custom types into a Bundle. however, because the data might be stale when you get it back. it is a better choice to use some other kind of storage ofr the data and put primtiive identifier into the Bundle instead. 
testing the implementation of onSaveInstanceState is a good idea -- espcially if you are saving and restoring objects. rotation is easy to test, tsting low memory situations is harder. you can simulate your activity being destroyed by android to reclaim memory 



Configuration changs are not the only time the OS can destroy an activity even though the user does not intend it to. each app gets its own process more specifcally, a Linux process cotnaining a single thread to execute UI related work on and a piece of emmory to store obejcts in 

an app's process can be dstroyed by the OS if the user naviate away for a while and adnroid needs to reclaim meory, when an app's prcess, all the obejcts stored in that process's memory are dstroyed 

process containing resumed or paused activities get higeher priority than other processes. when the OS needs to free up resources, it will select lower priortiy process first. pratically speaking, a process cotnainign a visible activity will not be relaimed by the OS. if a foreground process does get reclaimed, that means something is horribly wrong with the device and your app is being killed is probably the least of the user's concerns 

but stopped activities are fair game to be killed. if the user press the home button and then goes and watches a video or plays a game, your app's process might be destroyed. 

activites themseleves are not indivudally destroyed in low memory situations, even though the doumentaiton reads liek that is the case. instead, android clears an entire app process from memory, taking any of the app's in memory actitvies with it 

when the OS destroys the app's process, any of the app's activitews and ViewModels is stored in memory will be wpied away. and the OS will not be ncie about the destruction. it will not call any of the activity or ViewModel lifecyle callback functions 

how can you save UI state data and use it to reconstruct the activity so that the user never even knwos the activity was destroyed. one way to do this is to store data in saved instance sate. saved instance sate is data the OS temporily stores outside the activity. 


do not keep activties off when you are done testing, as it will cause a perofmrnace decrease. remember that pressing the back button instead of the home button will always destroy the activity, regardless of whether you have this development setting on . 


### saved instance state and activity records

how does the data you stash in onSaveInstanceState(Bundle) surive the activity's and process's death? when onSaveIstanceState(Bundle) is called, the data is saved to the Bundle object. that Bundel object is then stuffed into your **activity's activity record** by the OS 



when your activity is stashed, an Activity object does not exist, but the activity record object lives on in the OS. the OS can reanimate the activity using the activity record when it needs it 

note that your activity can pass nto the stash state without onDestroy() being called. you can rely on onStop() and onSaveInstanceState(Bundle) being called unless somethign has gone horribly wrongt on the device. typicaly, you override onSaveInstanceState(Bundle) to stash small, transient state that belongs to the current activity in your Bundle. override onStop() to save any permaent data, such as thigns the user is editing, because your activity may be killed at any time after this function returns 

so when does the activity record get snuffed? when the activity finishes, it really gets destroyed, once and for all. at this point, your activity record is discarded, activity records are also discarded on reboot



Nonexistent

|             | 
onCreate    onDestroy 
|         |
Stopped 
|         |
onStart    onStop
|           |
paused visible 
|           |
onResume    onPause
 |           |
 Resumed 




## ViewModel versus SaveInstanceState 
while saved instance state stores an activity record across process death, it also stores an activity record across a configuration chagne. when you first launch the activity, the savedInstanceState bundle is null. when you rotate your device, the OS calls onSaveInstanceState() on your activity. the OS then passes the data you stashd in the bundle to onCreate 

if saveInstanceState protected from both configuration changes and process death, why bother with a ViewModel at all? to be fair, you could have gotten away with savedInstanceState only 

however, most apps do not rely on a small hardcoded data set. most apps these days pull dyanimc data from a database, from the internet, or from a combiantion of both. these optioans are asynchronous, can be slow, and user precious battery and networking resources, and tying these opeation to the activity lifecyle can be very tedious and error prone 


ViewModel really shines when you use it to orchestrate dyanmic data for the activity, ViewModel makes continuing a downlaod operation across a configruation change simple. it also offers an esay way to keep data that was expensive to load in memory across a configuration change. and, as you ahve seen, ViewModel get s cleaned up automatically once user finishes the activiTY

ViewModel does not shine in the proces death scenario since it gets wiped away from memory along with the process everything in it. this is where saveInstanceState takes center stage. but savedInstanceState has its own limtiion. since savedInstanceState is serialized to disk, you should avoid stashing any large or complex object 


the adnroid team is actively working to improve the developer experience using ViewModels, lifecyle-viewmodel-savedstate is a new library thta was just relased to allow ViewModels to save their state across process death. this should alleviate some of the diificulties of using ViewModel alongside saved isntance state from your activity 


so it is a matter of which is better> savvy developers use savedInstanceState and ViewModel **in harmony** 


use savedInstanceState to store the minimal amount of info necessary to recreate the UI state. use ViewModel to cache the rich set of data needed to populate the UI in memory across configuration changes for quick and easy acess. when the activity is recreated after process death, use the saveInstanceSate info to set up the ViewModel as if the ViewModel and activity were never dstroyed 

there is no easy way to determine whether an activity is being recreatd after process death versus a configruation change. why does it matter? a ViewModel stays in memory during a configuration chagne. so if you use the savedIsntanceState data to update the ViewModel after the configruation, you are making your app do uncessary work. if the work causes the user to wait or use their reousrces like battery unecessarily, this reundant work is problmatic 


one way to fix this problem is to make your ViewModel a little smarter. when setting a ViewModel, value might result in more work, first check whether the data is fresh before doing the work to pull in and update the rest of the data 

neither ViewModel nor saveInstance state is a solution for long term storage. if your app needs to store data that should lvie on as long as the app instaleld on the device, regardless of your activity's state, use a persistent storage alternative. shared preferences is fine for very simple and small data. a local databsae is a better option for larger,  more complex data, in addition  to local storage, you could store data on a remote server somehwere 
it makes sense to persist them independent of activity lifecyle state. but accessing database is a relatively slow operation, compared to accessing values in mmeory. so it makes sense to load what you need to display your UI and retain that in memory while the UI is showing using a ViewModel 



### Avoid Half-baked solution 
you squashed state loss bug by correctly accounting for configuration changes and process death. some people try to address the UI state loss on configuration change bug in their app by disabling rotation. if the user cannoit rotate the app, they never lose their UI satte. but sadly this appraoch leaves your app prone to other bugs. while this smooths over the rough edge of rotation, it leaves other lifecycle bugs that users will surely encounter, but that will not neccessarily present themselves during development and testing 

first, there are other configuration changes that can occur at runtime, such as window resizing and night mode changes. you could also capture and ignore or handle those changes. but this is just bad pratice -- it disables a feature of the system, which is to automatically select the right resource based on the runtime configruation changes 

second, handling configuration chagnes or disabling rotation does not solve the process death issue. if you want to lock you app into portrait or landscape mode because it makes sense for your app. you should still prgram defensively against configuration changes and process death. you are equipped to do so with your newfound knowledge ViewModel and savedIstanceState

in short, dealing with UI sate loss by blocking configuration changes is had form. you will recognize it as such if you see it out in the wild 







### programming takeway 

1. kotlin no longer supports private const val VARIABLE = 100, const modifier is not applicable 

2. in kotlin, you may have been wondering about the override keyword. this asks the compiler to ensure that the class actually has the function you want to override. if the parent AppCompatActivity class does not have an onCreate(Bundle?) function, so the compiler will complain. this way you can fix the typo, rather than waiting until you run the app and see strange behaviour to discover 


3. in java, you will have to make sure the access modifier match the parent classes or have more openess -- protected when override the method The access modifier for an overriding method can allow more, but not less, access than the overridden method. 

