# android-development-kotlin


## Preface 

I have taken care in writing and make no expressed or implied warranty of any kind and assume no responsibility for errors or omissions. no liability is assumed for incidental or consequential damages in connection with or arising out of the use of the information contained herein. many of designations used by me are claimed as dedications. 
I feel a bit sheepish having names on the cover. The truth is that wihtout an army of collaborators, this could never have hapen. we owe devgelopers all a debt of gratitude. keeping programming through all app development for loving and supporting me through reminding me of what is important along the way. To whatever I personaly have fait in, android is shepherded into existence by a community of collaborators, risk takesrs and other supporters, without whom the burden of comprehending and writing all this material will be overwhelming. We should have the guesto to bring our work to the world, for single-handely writing sections by rubber duck we have ever met. As android studio evolves, developers, who may times saved us from going down rabit holes. they kept our writing focused on what readers really care about and spared all from cunsing, boring and irreleant detours. 
This repo talks through some tough conceptual decisions. Android developer, copyeditors and proofreader's attention to detail is unparalleled and greatly appreciated. They wrote by cutting up their work into little pieces, throwing them in the air, and publishing the rearrangement. Some confusion and simpleminded excitement may have caused us to resort to such techniques. The developer community always sanding away the remaining rough edges of versions. There is a feedback loop and they respond to it with their suggestions and corrections. if we could give ourselves additional brains to do with as we pleased, we would not, we would just put the new brains in a big pile, and share them with our colleagues. Their opinons or corrections as it was shaping up. it is curiosity we have worked to satisfy, confusions we have worked to clarify


## Learning Android 
Android is really blowing up in every generation and it works continously to get the analogy to the general public. It is really a rough day. It is dragging people up at the last minute. It is still holding up. We collectively lvoe it legitimately 

 
Android is an operating system consists of an operating system Linux and a framework. Android incorporated and get together with a number of other companies to create the open handset alliance. That could be further from the truth 
You face a steep learning curve, is like moving to a foreign city. There are so many things divided, things you already knew turn out to be dead wrong in this context. 


Android has a culture, the culture speaks Java and Kotlin or a bit of both, it is blowing up in the notification, but only knowing kotlin or Java is not enough. Getting your head around android requires learning many new ideas and techinques and have trememdously strong releationship with its ecosystem. What resonate with me is it helps to have a guid through unfamiliar territory. It is a career-long longevity to thrillers and we are connected with this. You will face them head on, and do your best to explain why things are the way they are

this approach allows you to put you have learned into pratice in a working app right away rather than learning a lot of theory and then having to figure out how to apply it later. 



## Java and Kotlin
you need to be familiar with Kotlin or Java, including classes, objects, interface, listeners, packages, inner classe, object expressions, generic classes, annoymopus inner class(java only)

if these ideas do not ring a bell, you will be in weeds. there are many introductory sections available in my repo. 
If you are comfortable with object oriented programming concepts, but your Kotlin or java is a little shaky or rusty, you will probably be ok. some brief explanation/remainder about specifcis is all you need. but keep a reference handy in case you need more support as you go through this. Take a listen, every adverted change and another sweeping chaneg is the inclusion of android jetpack component libraries. we incorporate the focus on how modern android app are developed. this is a big depature 


Kotlin has become widely adopted and it is most developer's preferred language for android development. The tide has continued to turn toward kotlin in a very big weay, android framework team has started adding @nullable anotations to legacy platform code. 

The android framework was orignially written in java, this means most of the android classes you interact with are java. luckily, kotlin is interoperable with java, so you should not run into any issues. 


we have chosen to display API listings in Kotlin, even if they are implemented behind the scnes in java. You can see the java api listing by browsing for the class you are interesed 


whether you prefer java or kotlin, this teaches you how to write android. the knowledge and experience you gain in developing apps for the android platform will translate to either language. I have supplied you with a quick cross reference between Kotlin and java to solify your knowledge
[kotlin_java_cross_reference.md] 

## Goal 
the goal is to get you over the initial hump to where you can get the most out of the reference and recipe books available. it is meant to be wrked through from the beginning, things are built on each other, and skipping around is unproductive 





























## install Android Studio SDK
moving forward presuming you are on Mac or Windows at this point 

https://developer.android.com/studio


virtual machines 
the cloud is built on virtualization, modern hardware allows VMs to run on PCs, can run different OS on single computer, which uses host's hardware 
virtualization technology has taken off, you need a new web server to meet demand. by running a powerful pc that hosts virtual servers, you can start a new server up from an imaeg quickly 





## configure android SDK 
let's get hang of android studio 
SDK manager -> Android version 
1. Android SDK Platform 29 
2. Sources sfor Android 29 
3. Google APIs Intel x86

install google play intel Atom system image

the window is resizable. the preview version is basically there for testing for experienced developers. untick the boxes of components and click on Apply button, some components may not be avaialble straightaway 


Settings -> Editor -> Auto Import -> add umambiguous import on the fly / optimize imports on the fly 

Appearnce -> show method separators

Code folding -> uncheck imports / one line methods / file headers / generic constructors and method parameters 




## Android Studio Templates 
the templates that google include with it -- espacially as they somtimes change them when they release a new version, this is up to date and coming out every few months, there will be times when it looks a bit different to how it appears 

they are provided to save you having to ype in some of the basic code that projects needs 




you work through a couple of templates, what you really use is a basic activity -- Empty Activity 



create a project -> application name -> componay domain -> project location 

you need to untick the kotlin support box this cause android studio to generate kotlink code if ticked rather than java code 


run -> create Virtual Device -> select Device -> select system image 


install HAXM :The HAXM stands for Hardware Accelerated Execution Manager. It is a cross-platform hardware-assisted virtualization engine (hypervisor), The Android Emulator use HAXM in intel platforms to speedup & improve performance
#### go to BIOS and turn on the Intel Virtualization 

Intel HAXM installation failed! : https://github.com/intel/haxm/releases




## gradle 
gradle is an open source build automation system, it basically pulls together all the bits of the project to create the app file that can be installed on an android device. if you use an external library, then you tell gradle about them and it sorts everything out, you can get the job done 



