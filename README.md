#  UI/UX Authoring Tool

<!-- make your own badges from here: http://shields.io/ -->
[![Version](https://img.shields.io/badge/MM__SL__UI/UX-V2.5-ff69b4.svg)](http://www.miningminds.re.kr/english/)
![License](https://img.shields.io/badge/Apache%20License%20-Version%202.0-yellowgreen.svg)

--------------------------
<!-- Update the list and the main body. -->

This document describes how to get started using the UI/UX Authoring tool Tracking SDK for Android. UI/UX Authoring tool is open source UX engine that gives you valuable insights into your application user, and much more, so you can optimize your strategy and experience of your application user.


- [1. Introduction and core concepts](#1-introduction)
    - [1.1 Device](#11-device)
    - [1.2 Context](#12-context)
    - [1.1 Recognizer](#13-recognizer)
	
- [2. Getting started](#2-getting-started)
    - [2.1 Requirements](#21-requirements)
    - [2.2 Installation](#22-installation)
    - [2.3 Usage](#23-usage)
	
- [3. Features](#3-features)
    - [3.1 Plug and play recognizers](#31-plug-and-play-recognizers)
    - [3.2 External Configuration File](#32-external-configuration-file)
   
- [4. Author](#4-authors)

- [5. For more details](#5-for-more-details)

- [6. License](#6-license)

<!-- Main Body of the Document -->

## 1. UI/UX Authoring Tool Android Tracking SDK

### 1.1 Getting Started

Integrating UI/UX Authoring tool tracking into your Android app

### 1.2 Include Library
Import the uiuxanalytics library into your Android app, then add this to your app build.gradle file: check the UIUXAnalyticsdemo as sample

        dependencies {
                    compile fileTree(dir: 'libs', include: ['*.jar'])
                    //.....
                    compile project(':uiuxanalytics')
                     }

### 1.3 Initialize Tracker

Developers could manage the tracker lifecycle by themselves. To ensure that the matrics are not overcounted, it is highly recommended that the tracker be created and managed in the Application class. 

       import java.net.MalformedURLException;
       public class YourApplication extends Application {
           private Tracker uiuxanalayticstracker;
           public synchronized Tracker getTracker(){
               if (uiuxanalayticstracker != null) {
                    return uiuxanalayticstracker;
               }
                try {
                    uiuxanalayticstracker = 
                    uiuxanalayticstracker.getInstance(this).newTracker("http://...../api/analytics/actionlog/", appID);
                } catch (MalformedURLException e){
                    Log.w(Tracker.LOGGER_TAG, "url is malformed", e);
                    return null;
                  }
                 return uiuxanalayticstracker;
                }     
               }

Note:use the app ID Created by UI/UX Authroing Tool Web Interface 
Don't forget to add application name to your AndroidManifest.xml file.

         <application android:name=".YourApplication">
               <!-- activities goes here -->
         </application>

### 1.4 Tracker Usage

#### 1.4.1 Track Screen Views

To send a screen view set the screen path and titles on the tracker

          public class YourActivity extends Activity {
            @Override
            public void onCreate(Bundle savedInstanceState) {
               super.onCreate(savedInstanceState);
               Tracker tracker = ((YourApplication) getApplication()).getTracker();
               TrackHelper.track().screen("/your_activity").title("Title").with(tracker);
             }
           }

#### 1.4.2 Track events 

To collect data about user's interaction with interactive components of your app, like button presses or the use of a particular item in a application use trackEvent method.

       TrackHelper.track().event("category", 
        "action").name("label").value(1000f).with(tracker);

#### 1.4.3 Track exceptions and errors 
To collect the exceptions and errors occrurred in the application use a 

        TrackHelper.track().exception(new Exception("OnPurposeException")).description("Crash button").fatal(false).with(getTracker());

#### 1.4.4 User ID

Allow to collect the data based on user id

        ((YourApplication) getApplication()).getTracker().setUserId("user@email.com");



## 2. UI/UX Authoring Tool Web Interface

UI/UX Authoring tool is web based UX engine that collects the user app usage behavior data by integrating the SDK in android applications. This is Django package, you must install Django befor using this package.

### 2.1. Installation
To get started with UI/UX Authoring tool analytics, the package must first be dowloaded from the repo then access the dowloaded folder via command line then run the follow command

       pip install -r requirements.txt

### 2.2 Dependencies
* Django
* Django REST framework 



After adding the 'ui_ux_authoring_tool' in your project setting, then run the following commands

        $ python manage.py makemigrations
        $ python manage.py migrate  
