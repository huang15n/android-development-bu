# android-development-kotlin


android is an operating system consists of an operating system Linux and a framework. Android incorporated and get together with a number of other companies to create the open handset alliance. That could be further from the truth 







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



