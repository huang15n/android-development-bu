
# Activity Lifecyle and Persisting UI state 


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

android does a great job of providing alternative resources at the right. howver, destroying and re-creating activties on rotation can cause headaches 















### programming takeway 

1. kotlin no longer supports private const val VARIABLE = 100, const modifier is not applicable 

2. in kotlin, you may have been wondering about the override keyword. this asks the compiler to ensure that the class actually has the function you want to override. if the parent AppCompatActivity class does not have an onCreate(Bundle?) function, so the compiler will complain. this way you can fix the typo, rather than waiting until you run the app and see strange behaviour to discover 


3. in java, you will have to make sure the access modifier match the parent classes or have more openess -- protected when override the method The access modifier for an overriding method can allow more, but not less, access than the overridden method. 

