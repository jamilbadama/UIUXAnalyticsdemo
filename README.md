# UI/UX Authoring Tool

This document describes how to get started using the UI/UX Authoring tool Tracking SDK for Android. UI/UX Authoring tool is open source UX engine that gives you valuable insights into your application user, and much more, so you can optimize your strategy and experience of your application user.


# 1. UI/UX Authoring Tool Android Tracking SDK

### 1.1 Getting Started

Integrating UI/UX Authoring tool tracking into your Android app

## 1.2 Include Library

Add this to your apps build.gradle file:

        dependencies {
            repositories{
                      jcenter()
                        }
                     // ...
                     compile 'khu.uclab.mm.sl.uiux.analytics'
                     }

## 1.3 Initialize Tracker

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
                    uiuxanalayticstracker.getInstance(this).newTracker("trackerapiurl", 1);
                } catch (MalformedURLException e){
                    Log.w(Tracker.LOGGER_TAG, "url is malformed", e);
                    return null;
                  }
                 return uiuxanalayticstracker;
                }     
               }

Don't forget to add application name to your AndroidManifest.xml file.

         <application android:name=".YourApplication">
               <!-- activities goes here -->
         </application>

# 2. Tracker Usage

## 2.1 Track Screen Views

To send a screen view set the screen path and titles on the tracker

          public class YourActivity extends Activity {
            @Override
            public void onCreate(Bundle savedInstanceState) {
               super.onCreate(savedInstanceState);
               Tracker tracker = ((YourApplication) getApplication()).getTracker();
               TrackHelper.track().screen("/your_activity").title("Title").with(tracker);
             }
           }

## 2.2 Track events 

To collect data about user's interaction with interactive components of your app, like button presses or the use of a particular item in a game use trackEvent method.

       TrackHelper.track().event("category", 
        "action").name("label").value(1000f).with(tracker);

## 2.3 User ID

Allow to collect the data based on user id

        ((YourApplication) getApplication()).getTracker().setUserId("user@email.com");






# UI/UX Authoring Tool Web Interface

UI/UX Authoring tool is web based UX engine that collects the user app usage behavior data by integrating the SDK in android applications. This is Django package, you must install Django befor using this package.

# 1. Getting Start

To get started with UI/UX Authoring tool analytics, the package must first be installed using pip command.

           pip install ui_ux_authoring_tool

After you install ui_ux_authoring_tool you need to add it to the list of installed applications in the settings.py file of your project

         INSTALLED_APPS = [
            ...
            'ui_ux_authoring_tool';
            ...
         ]

After adding the 'ui_ux_authoring_tool' in your project setting, then run the following commands

        $ python manage.py makemigrations
        $ python manage.py migrate  
