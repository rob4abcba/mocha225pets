
MOCHA225 (ABND) [Oct 28th at 5:56 PM]
I can’t figure out why I’m not getting a compilation error on the pet app
I add sanity checks in Pet Provider and get 23 errors
package com.example.android.pets.data;
import android.content.ContentProvider;
import android.content.ContentUris;
import android.content.ContentValues;
Click to expand inline 175 lines


13 replies
Jorge E. Covarrubias (ABND) [7 days ago]
@MOCHA225 (ABND) at line 146 you have an open {  and need to close it after the throw new IllegalArgument...  so in line 149

Jorge E. Covarrubias (ABND) [7 days ago]
@MOCHA225 (ABND) also at line 138 the } bracket shouldn't be there. You can delete that

Jorge E. Covarrubias (ABND) [7 days ago]
the latter reason might would have thrown of your formatting creating a little bit of confusion.

MOCHA225 (ABND) [7 days ago]
That got me down to 14 errors.  And values became red

Jorge E. Covarrubias (ABND) [7 days ago]
@MOCHA225 (ABND) What are the errors? do you have this up on github? That was from a quick visual scan

MOCHA225 (ABND) [7 days ago]
I’ll put on github.  Fixed all the errors but app stops and wants to be restarted.

MOCHA225 (ABND) [7 days ago]
here is my github link https://github.com/mocha225/mocha225pets.git
GitHub
mocha225/mocha225pets
Contribute to mocha225/mocha225pets development by creating an account on GitHub.
 

Jorge E. Covarrubias (ABND) [7 days ago]
i'm coming. was helping someone else. :grin:

Jorge E. Covarrubias (ABND) [7 days ago]
@MOCHA225 (ABND) Here we go.
First clean up the empty space in your if statements in the PetProvider when doing the sanity checks. then at line 168, you need an open bracket { for your if statement and close it at line 170.
Hit CTRL + ALT + L to reformat your code and make it easier to read. You should notice the it will remove some indentation after line172.

Jorge E. Covarrubias (ABND) [7 days ago]
Now that that is set, I was getting an error in the catalogActivity that the cursor was null. "Attempt to invoke interface method 'void android.database.Cursor.close()' on a null object reference"

So this was telling me that it was empty. Why is it empty? I took a look at the cursor declaration in line 75 and saw that it points to PetEntry.CONTENT_URI located in the PetContract.

I noticed nn the PetContract, your String
public static final String CONTENT_AUTHORITY = ".com.example.android.pets"; shouldn't have that . before the com.

it should read
public static final String CONTENT_AUTHORITY = "com.example.android.pets";

**

https://github.com/rob4abcba/mocha225pets

**





**

FAILURE: Build failed with an exception.



* What went wrong:

Could not open cp_settings remapped class cache for 9khs0qj4gyiyra4guh5oezmza (C:\Users\rob_t\.gradle\caches\4.4\scripts-remapped\settings_8dvrwb9v19ok742olr82mzssq\9khs0qj4gyiyra4guh5oezmza\cp_settings638c4bcc3be846fd35262b91d5a74869).

> Could not open cp_settings generic class cache for settings file 'C:\Users\rob_t\Udacity\Android\mocha225pets\settings.gradle' (C:\Users\rob_t\.gradle\caches\4.4\scripts\9khs0qj4gyiyra4guh5oezmza\cp_settings\cp_settings638c4bcc3be846fd35262b91d5a74869).

   > java.io.FileNotFoundException: C:\Users\rob_t\.gradle\caches\4.4\scripts\9khs0qj4gyiyra4guh5oezmza\cp_settings\cp_settings638c4bcc3be846fd35262b91d5a74869\cache.properties (The system cannot find the file specified)



* Try:

Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.



* Get more help at https://help.gradle.org



CONFIGURE FAILED in 10s

C:\Users\rob_t\.gradle\caches\4.4\scripts\9khs0qj4gyiyra4guh5oezmza\cp_settings\cp_settings638c4bcc3be846fd35262b91d5a74869\cache.properties (The system cannot find the file specified)



**

11/5/2018

8:19 PM Gradle sync started



8:19 PM Gradle sync failed: C:\Users\rob_t\.gradle\caches\4.4\scripts\9khs0qj4gyiyra4guh5oezmza\cp_settings\cp_settings638c4bcc3be846fd35262b91d5a74869\cache.properties (The system cannot find the file specified)

    Consult IDE log for more details (Help | Show Log) (25 s 606 ms)

**



**

Google: cache.properties (The system cannot find the file specified)

**

I just started using Android Studio 1.3 sdk 24 and it has worked fine until today. I get this error message about cache.properties and I delete that cache file but now I am getting this error message:

Error:C:\Users\user1.gradle\caches\2.4\scripts\asLocalRepo15_dhjxrnvsgiyg1ow3dfj4myl7\InitScript\initscript\cache.properties (The system cannot find the file specified)

I try file/invalidate caches/restart.. and rebuild project but am still getting this error message. How do I fix it?

android android-studio

shareimprove this question

edited Jul 15 '16 at 14:45






WMios

6,54393357

asked Aug 15 '15 at 12:59






max

2,14462445

Check if disabling Instant Run in the Preferences of Android Studio makes a difference. In was the solution for the issue in my setup. – JJD Nov 30 '17 at 11:30 

add a comment


16 Answers
activeoldestvotes


up vote
130
down vote
accepted

You don't have to delete all .gradle folders and no need to reinstall Android Studio.

I have the latest version of Android Studio and I faced that problem, the only thing that worked for me is to:

Navigate to C:\Users\user\.gradle\caches\2.x\

Copy the folder scripts , scripts-remapped and paste it somewhere safe just in case anything went wrong you will place it back

Delete this folder scripts and scripts-remapped from the directory C:\Users\user\.gradle\caches\2.x\

Sync Project with Gradle Files and you are done.

enter image description here

When you sync your project, Android Studio will generate new cache files.

You also need to delete buildOutputCleanup.lock from projectLocation/.gradle/buildOutputCleanup in case the above 4 steps do not work out.

It worked for me I hope it will work for you.

shareimprove this answer

edited Oct 25 at 7:42






Community♦

11

answered Sep 5 '15 at 14:05






Salam El-Banna

2,2241925

2

This is the correct answer. No need of reinstall anything. Thanks. – SajithK Sep 22 '15 at 9:33

1

same problem as mine, but \caches\2.2.1\ worked for me, thanks – dens14345 Dec 12 '15 at 1:54 

1

Thank you so much, This worked for me :) – unitedartinc Jan 1 '16 at 6:10

1

Thanks alot, after removing script-remapped, it worked for me too – Naveed Ahmad Dec 1 '16 at 14:49

1

Its really great solution!! thank you – Learning Always Dec 22 '16 at 5:54

show 8 more comments



Pear Therapeutics

We have 6 open jobs ♥

Imagine yourself at Pear Therapeutics

Learn more


up vote
11
down vote

Reinstall Android Studio again is not an option!
To fix the problem:

cache.properties (The system cannot find the file specified)

go to :

 C:\Users\[User]\.gradle\caches\
Delete folders \2.4 and \2.8

introducir la descripción de la imagen aquí

Restart Android Studio!.

shareimprove this answer

answered Apr 3 '16 at 3:23






Jorgesys

90.7k15234206

2

If deleting 2.4 and 2.8 doesn't work for you, make sure you take note of the folder number in the error message. It might be something else other than 2.4 or 2.8. Mine was 2.14.1 – ojonugwa ochalifu Sep 8 '16 at 20:01

Hey it works for me! =) – Jorgesys Jan 19 '17 at 15:06

add a comment


up vote
8
down vote

You don't have to reinstall Android Studio or no need to delete all .gradle folder.

I am reinstalled the latest version of Android Studio and still I faced that problem. It caused my to rename the "Android Projects" folder on my desktop in my case.

The only thing that you have to do:

1-Navigate to C:\Users\user_name.gradle\caches\2.4 or (2.8 if error in it otherwise)

2-Copy the folder "2.4" or "2.8" and paste it somewhere safe just in case anything went wrong you will place it back

3-Delete this error folder from the directory C:\Users\user.gradle\caches\2.4\ (or \2.8)

4-Close the Android studio & restart it.

During restart it sync your project & Android Studio will generate new cache files.

It worked for me I hope it will work for you... :)

shareimprove this answer

edited Jan 16 '17 at 6:30






Omi

1,8981826

answered Jan 12 '16 at 19:33






user5780741

8911

add a comment


up vote
6
down vote

I have the same problem, I just delete .gradle from C:\Users\user\.gradle\caches\2.4\ and from my application too.

Of course close Android Studio and start Android Studio again.

shareimprove this answer

edited Jul 15 '16 at 14:58






WMios

6,54393357

answered Sep 28 '15 at 5:55






destinydz

6113

Deleting the .gradle directory from the project folder was enough to solve the issue for me – Trent Feb 22 '17 at 1:40 

This worked for me. The accepted answer, above, did not work for me... I had already deleted from the user\.gradle location. That was not enough. I had to delete from your suggested: (project location)\.gradle. – Dale Feb 25 '17 at 2:05 

add a comment


up vote
4
down vote

No need to reinstall anything.

Just delete the 2.4 and 2.8 folder located at C:\Users\user\.gradle\cachesdirectory and reopen android studio. It will generate new cash files so now the build should be successful.

shareimprove this answer

answered Mar 11 '16 at 7:01






Sabeeh

60369

this..worked..sabeesh..thanks – John Jul 11 '16 at 5:13

add a comment


up vote
3
down vote

Easy solution. Go ahead and create an empty cache.properties file under the path specified in the error log. The error should then disappear.

shareimprove this answer

edited Jul 15 '16 at 14:59






WMios

6,54393357

answered Jan 27 '16 at 22:02






Manoj Shrestha

1,35211731

1

Remarkably simple solution :) – zenzelezz Jan 30 at 11:29

add a comment


up vote
3
down vote

As said in the above examples i have tried resolving with extra steps:

Navigate to the respective folder C:\Users\user.gradle\caches\2.14.1\
Copy both the folders "scripts" and "scripts-remapped" into a safe place.
Now, DELETE BOTH THE FOLDERS "scripts" and "scripts-remapped" in the location C:\Users\user.gradle\caches\2.14.1\
Finally, try to sync the gradle.
Android Studio will ask to Upgrade the Gradle plugin. So click on Upgrade the gradle.
(If not try to Restart the Android Studio IDE completely.)

Finally, it is done for me...!!!

shareimprove this answer

answered Oct 31 '16 at 14:58






Prakash P

642

add a comment


up vote
2
down vote

I found the solution to my question, but I do not know whether it is the optimal solution:

I deleted all .gradle folders in user library and reinstalled android and then it worked.

shareimprove this answer

edited Jul 15 '16 at 14:47






WMios

6,54393357

answered Aug 16 '15 at 13:16






max

2,14462445

add a comment


Deleting the "scripts" folder and rebuilding the project will solve this problem.

shareimprove this answer

edited Apr 27 '16 at 8:29






0X0nosugar

6,48631742

answered Apr 27 '16 at 5:24






Kaisar Hossain

111

@Kaisar Hossein - I hope I've understood what you wanted to say. Please note that the Community prefers posts without expressions like "thanks", "hope this helps" etc. If I misunderstood you can always edit your own posts as often as you like :) – 0X0nosugar Apr 27 '16 at 8:35



I don't know why a great developer as Google can't manage this issue by them selves it is very easy to delete the cached folder and regenerate it programmatically. ** RL: DO THIS ** Any way just navigate to C:\Users\user.gradle\caches\ and open the latest version folder, then delete the scripts folder. Go to android studio and sync project. (RL: File > Sync Project with Gradle Files)

**



**

I was working on a project, and then I got a prompt to update Android Studio. After I did that, I started getting this error when trying to run my app Error

It says

The project may need to be synced with Gradle files

How do I solve this?

android android-studio

shareimprove this question

edited Jun 8 '16 at 6:57






twlkyao

5,26441834

asked Nov 12 '13 at 15:11



ojonugwa ochalifu

14.8k2177103

add a comment


5 Answers
activeoldestvotes


up vote
116
down vote
accepted

Clicking the button 'Sync Project With Gradle Files' should do the trick:

Tools -> Android -> Sync Project with Gradle Files

If that fails, try running 'Rebuild project':

Build -> Rebuild Project

EDIT

Starting with Android Studio 3.1, you should go to:

File -> Sync Project with Gradle Files

shareimprove this answer

edited Apr 20 at 13:44



Mateus Gondim

2,35931942

answered Nov 12 '13 at 15:16




Jonathon Fry

2,01931827

Try running './gradlew clean packageDebug' from the project root. – Jonathon Fry Nov 12 '13 at 15:29

1

Perfect answer ...!!! – Najib Puthawala May 26 '15 at 9:32

Updated to android stuido 2.0 and button is now disabled and solution above does not help – Vlado PandžićApr 18 '16 at 9:45

awesome answer... – Sudipta Som Apr 26 '16 at 11:07

2

Unfortunately this option does not exist in Android Studio 2.2. – Igor Ganapolsky Jun 14 '16 at 21:08

show 6 more comments



up vote
4
down vote

Old Answer

When trying to run the application, instead of selecting the directory highlighted here in blueenter image description here

I selected the subdirectory instead

enter image description here

and clicked "run".All the issues with Gradle are automatically resolved and the missing apk directory is automatically created.

New Solution

The Sync project with gradle files button disappeared from Android Studio for a while.Its back and you can find it here:

enter image description here

hit the button and wait for the task to complete

shareimprove this answer

edited Aug 18 '17 at 6:26

answered Nov 12 '13 at 15:44






ojonugwa ochalifu

14.8k2177103

add a comment



up vote
1
down vote

I've had this problem after installing the genymotion (another android amulator) plugin. A closer inspection reveled that gradle needs SDK tools version 19.1.0 in order to run (I had 19.0.3 previously).

To fix it, I had to edit build.gradle and under android I changed to: buildToolsVersion 19.1.0

Then I had to rebuild again, and the error was gone.

**

Build Sync Pane

**

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/gradle/3.1.4/gradle-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/gradle-core/3.1.4/gradle-core-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/builder/3.1.4/builder-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/lint/lint-gradle-api/26.1.4/lint-gradle-api-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/gradle-api/3.1.4/gradle-api-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/databinding/compilerCommon/3.1.4/compilerCommon-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/builder-model/3.1.4/builder-model-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/sdklib/26.1.4/sdklib-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/sdk-common/26.1.4/sdk-common-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/builder-test-api/3.1.4/builder-test-api-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/analytics-library/protos/26.1.4/protos-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/manifest-merger/26.1.4/manifest-merger-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/ddms/ddmlib/26.1.4/ddmlib-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/analytics-library/shared/26.1.4/shared-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/analytics-library/tracker/26.1.4/tracker-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/apksig/3.1.4/apksig-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/common/26.1.4/common-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/databinding/baseLibrary/3.1.4/baseLibrary-3.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/annotations/26.1.4/annotations-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/layoutlib/layoutlib-api/26.1.4/layoutlib-api-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/dvlib/26.1.4/dvlib-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/repository/26.1.4/repository-26.1.4.pom

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/gradle-api/3.1.4/gradle-api-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/gradle/3.1.4/gradle-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/gradle-core/3.1.4/gradle-core-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/builder/3.1.4/builder-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/manifest-merger/26.1.4/manifest-merger-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/databinding/compilerCommon/3.1.4/compilerCommon-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/sdk-common/26.1.4/sdk-common-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/sdklib/26.1.4/sdklib-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/repository/26.1.4/repository-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/analytics-library/tracker/26.1.4/tracker-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/builder-test-api/3.1.4/builder-test-api-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/ddms/ddmlib/26.1.4/ddmlib-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/analytics-library/shared/26.1.4/shared-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/dvlib/26.1.4/dvlib-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/layoutlib/layoutlib-api/26.1.4/layoutlib-api-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/common/26.1.4/common-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/analytics-library/protos/26.1.4/protos-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/builder-model/3.1.4/builder-model-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/build/apksig/3.1.4/apksig-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/databinding/baseLibrary/3.1.4/baseLibrary-3.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/annotations/26.1.4/annotations-26.1.4.jar

Download https://dl.google.com/dl/android/maven2/com/android/tools/lint/lint-gradle-api/26.1.4/lint-gradle-api-26.1.4.jar



FAILURE: Build failed with an exception.



* What went wrong:

A problem occurred configuring project ':app'.

> Failed to find target with hash string 'android-24' in: C:\Users\rob_t\AppData\Local\Android\Sdk



* Try:

Run with --stacktrace option to get the stack trace. Run with --info or --debug option to get more log output. Run with --scan to get full insights.



* Get more help at https://help.gradle.org



CONFIGURE FAILED in 31s

Failed to find target with hash string 'android-24' in: C:\Users\rob_t\AppData\Local\Android\Sdk

Install missing platform(s) and sync project



**

Event Log

**

8:53 PM Gradle sync started



8:54 PM Gradle sync failed: Failed to find target with hash string 'android-24' in: C:\Users\rob_t\AppData\Local\Android\Sdk

    Consult IDE log for more details (Help | Show Log) (32 s 38 ms)



**

RL: The hyperlink to Install missing platform(s) is in the LHS Build Sync side not the RHS Event Log.

**





Packages to install:

- Android SDK Platform 24 (platforms;android-24)



Preparing "Install Android SDK Platform 24 (revision: 2)".

Downloading https://dl.google.com/android/repository/platform-24_r02.zip

**

To take advantage of the latest features, improvements, and security fixes, we strongly recommend that you update the Android Gradle plugin to version 3.2.1 and Gradle to version 4.6. Release notes  Android plugin 3.2.0 and higher now support building the Android App Bundle—a new upload format that defers APK generation and signing to compatible app stores, such as Google Play. With app bundles, you no longer have to build, sign, and manage multiple APKs, and users get smaller, more optimized downloads. Learn more

**





I clicked Update.

**

RL: What happened before with 4.4 is happening now with 4.6.



Here 4.4 is shaded:




Here 4.6 is shaded




**

** RL: DO THIS ** Any way just navigate to C:\Users\user.gradle\caches\ and open the latest version folder, then delete the scripts folder. Go to android studio and sync project. (RL: File > Sync Project with Gradle Files)


Finally after this round it passed and I got the Play button became GREEN.  

Click the GREEN Play button.


Chose my edited virtual device.  This didn't show anything on the device image.  Just black screen.


Try again. Click the GREEN Play button again.

Choose Pixel API 19 this time.  Now I do see stuff on the phone screen.  Not just black screen.


**

From Event Log:


11/5/2018

8:19 PM Gradle sync started


8:19 PM Gradle sync failed: C:\Users\rob_t\.gradle\caches\4.4\scripts\9khs0qj4gyiyra4guh5oezmza\cp_settings\cp_settings638c4bcc3be846fd35262b91d5a74869\cache.properties (The system cannot find the file specified)

    Consult IDE log for more details (Help | Show Log) (25 s 606 ms)


8:53 PM Gradle sync started


8:54 PM Gradle sync failed: Failed to find target with hash string 'android-24' in: C:\Users\rob_t\AppData\Local\Android\Sdk

    Consult IDE log for more details (Help | Show Log) (32 s 38 ms)


11:01 PM Gradle sync started


11:01 PM Project setup started


11:01 PM Gradle sync finished in 57 s 490 ms


11:02 PM Gradle sync started


11:02 PM Gradle sync failed: C:\Users\rob_t\.gradle\caches\4.6\scripts\9khs0qj4gyiyra4guh5oezmza\cp_settings\cp_settingsdf5583fde4f7f1f2f3f5ea117e2cdff1\cache.properties (The system cannot find the file specified)

     Consult IDE log for more details (Help | Show Log) (27 s 900 ms)


11:17 PM Gradle sync started


11:17 PM Project setup started


11:17 PM Gradle sync finished in 29 s 711 ms


11:17 PM Executing tasks: [:app:generateDebugSources]


11:17 PM Gradle build finished in 6 s 158 ms


11:20 PM * daemon not running; starting now at tcp:5037


11:20 PM * daemon started successfully


11:20 PM Executing tasks: [:app:assembleDebug]


11:20 PM Gradle build finished in 5 s 66 ms


11:22 PM Emulator: Process finished with exit code 0


11:22 PM Instant Run is not supported on devices with API levels 20 or lower.

     (Don't show again)


11:22 PM Executing tasks: [:app:assembleDebug]


11:22 PM Gradle build finished in 2 s 314 ms


11:23 PM Emulator: FramebufferData::restore: warning: a texture is deleted without unbinding FBO


11:23 PM Emulator: FramebufferData::restore: warning: a texture is deleted without unbinding FBO



11:23 PM Emulator: FramebufferData::restore: warning: a texture is deleted without unbinding FBO

**

The bottom status line has that same last warning line but is clickable.  Click "Emulator: FramebufferData::restore: warning: a texture is deleted without unbinding FBO"



**

Now the LHS Build (not Sync) side says:  

Could not find com.android.tools.build:aapt2:3.2.1-4818971.

Searched in the following locations:

    file:/C:/Users/rob_t/AppData/Local/Android/Sdk/extras/m2repository/com/android/tools/build/aapt2/3.2.1-4818971/aapt2-3.2.1-4818971.pom

    file:/C:/Users/rob_t/AppData/Local/Android/Sdk/extras/m2repository/com/android/tools/build/aapt2/3.2.1-4818971/aapt2-3.2.1-4818971-windows.jar

    file:/C:/Users/rob_t/AppData/Local/Android/Sdk/extras/google/m2repository/com/android/tools/build/aapt2/3.2.1-4818971/aapt2-3.2.1-4818971.pom

    file:/C:/Users/rob_t/AppData/Local/Android/Sdk/extras/google/m2repository/com/android/tools/build/aapt2/3.2.1-4818971/aapt2-3.2.1-4818971-windows.jar

    file:/C:/Users/rob_t/AppData/Local/Android/Sdk/extras/android/m2repository/com/android/tools/build/aapt2/3.2.1-4818971/aapt2-3.2.1-4818971.pom

    file:/C:/Users/rob_t/AppData/Local/Android/Sdk/extras/android/m2repository/com/android/tools/build/aapt2/3.2.1-4818971/aapt2-3.2.1-4818971-windows.jar

    https://jcenter.bintray.com/com/android/tools/build/aapt2/3.2.1-4818971/aapt2-3.2.1-4818971.pom

    https://jcenter.bintray.com/com/android/tools/build/aapt2/3.2.1-4818971/aapt2-3.2.1-4818971-windows.jar

Required by:

    project :app

** 

The bottom 2 lines above are clickable.  Click them both but got 404 page not exist.



Google: Emulator: FramebufferData::restore: warning: a texture is deleted without unbinding FBO



Got:



Do I need to unbind a texture after drawing a textured primitive?
By Extrakun, August 14, 2008 in Graphics and GPU Programming 



Hi, I am drawing two primitives; one is bind to a texture, the other is not. However, somehow, the second primitive takes on the texture of the first.



i, I am drawing two primitives; one is bind to a texture, the other is not. However, somehow, the second primitive takes on the texture of the first.




">I've recorded an animation of what is happening and put it on youtube. As you can see, whenever the textured quad changes the uv coordinate (the numbers are actually from one piece of texture), so does the colour of the cat. Both are enclosed within their own glBegin and glEnd... The code is as such (using Tao.OpenGL)

// For the textured quad
 public void Draw(Texture drawable, float gameTime, float x, float y, float UVStartX, float UVStartY,
                float UVWidth, float UVHeight)
        {
            Gl.glPushMatrix();
            Gl.glTranslatef(x, y, 0.0f);

            // TODO: Calculate world height and world width
            float worldHeight = 1.0f;
            float worldWidth = 1.0f;

            // Bind the texture
            Gl.glBindTexture(Gl.GL_TEXTURE_2D, drawable.TextureID);

            // Begin drawing the quad
            Gl.glBegin(Gl.GL_TRIANGLES);

            // First triangle, first point
            Gl.glTexCoord2f(UVStartX, UVStartY);
            Gl.glVertex3f(0.0f, 0.0f, 0.0f);

            // First triangle, second point
            Gl.glTexCoord2f(UVStartX, UVStartY + UVHeight);
            Gl.glVertex3f(0.0f, worldHeight, 0.0f);

            // First triangle, third point
            //Gl.glTexCoord2f(UVStartX + UVHeight, UVStartY);
            Gl.glTexCoord2f(UVStartX + UVWidth, UVStartY);
            Gl.glVertex3f(worldWidth, 0.0f, 0.0f);

            // Second triangle, first point
            Gl.glTexCoord2f(UVStartX + UVWidth, UVStartY);
            Gl.glVertex3f(worldWidth, 0.0f, 0.0f);

            // Second triangle, second point
            Gl.glTexCoord2f(UVStartX, UVStartY + UVHeight);
            Gl.glVertex3f(0.0f, worldHeight, 0.0f);

            // Second triangle, third point
            Gl.glTexCoord2f(UVStartX + UVWidth, UVStartY + UVHeight);
            Gl.glVertex3f(worldWidth, worldHeight, 0.0f);           
            Gl.glEnd();            

            Gl.glPopMatrix();


**

And the code which draws the 'cat' is actually all triangle primitives

public void Draw(float timeElapsed)
        {
            // Store previous settings
            Gl.glPushMatrix();

            // Translate to location            
            Gl.glTranslatef(posX_, posY_, 0f);            

            // Animation consists of frame; now we just want to first frame
            CacFrame toRender = animation_.Frames[currentFrame_];

            // NOTE: A frame consist of multiple strokes; a stroke consist of multiple vertices and triangles
            // Begin to draw triangles
            Gl.glBegin(Gl.GL_TRIANGLES);

            foreach (CacStroke s in toRender.Strokes)
            {
                for (int strokeIndex = 0; strokeIndex < s.Vertices.Count; strokeIndex++)
                {
                    // Get the triangles that form the stroke
                    List<IndexedTriangle> triangles = s.Triangles;

                    // Get the vertices that form the stroke
                    List<DiffuseVertex> vertices = s.Vertices;

                    // Draw all the triangles
                    foreach (IndexedTriangle eachTriangle in triangles)
                    {
                        for (int i = 0; i < 3; i++)
                        {
                            // extract the diffuse vertex
                            DiffuseVertex currentVertex = vertices[eachTriangle.index];

                            Gl.glColor4f(currentVertex.R, currentVertex.G, currentVertex.B, currentVertex.A);
                            Gl.glVertex3f(currentVertex.X, currentVertex.Y, currentVertex.Z);
                        }
                    }
                }
            }

            Gl.glEnd();

            // Restore OpenGL setting
            Gl.glPopMatrix();


I call Gl.glEnd() after drawing each of the primitive. Do I need to 'unbind' the texture so that the cat will not change colour? (It's supposed to be white).

**

OpenGL is a state machine, that is, if you set something, it stays that way until you unset it.



In the case above, you are binding a texture to one object, but it is continuing to stay bound, even though the model you are drawing is untextured. Therefore it is taking the previous state (the bound texture) and using that on the model.



There are two ways to get around this.



Either gall glBindTexture with the 2nd arguement being NULL, this will unbind any bound texture. Or simply call glDisable(GL_TEXTURE2D), which will disable all texturing, however you will need to remember to call glEnable(GL_TEXTURE2D) before drawing the object with the texture.



Hope this helps.

**

Quote:

Original post by AndyEsser

There are two ways to get around this.



Either gall glBindTexture with the 2nd arguement being NULL, this will unbind any bound texture. Or simply call glDisable(GL_TEXTURE2D), which will disable all texturing, however you will need to remember to call glEnable(GL_TEXTURE2D) before drawing the object with the texture.



Hope this helps.





Binding texture ID zero will bind texture ID zero. Texture ID zero is the default texture and is a perfectly valid texture object to use for texturing (you can upload an image to it and use it). That is a very bad way to "disable" texturing, becuase texturing is still enabled and in use.



If you want to disable texturing, then my advice is to... disable texturing.



edit: Just a minor adjustmet on 0 being a texture object. It's not, actually. It is the way to disable texture objects and fall back to old style texture management, but for the purpose of explaining, it behaves as a default object that cannot be deleted.

**

Thanks for the answer! 



I tried disabling texture before the drawing the primitives which I only want to have the diffuse colors and it works; I just have to remember re-enabling the texturing before the drawing the quad.



On a separate note, will multiple glEnable(GL_TEXTURE_2D) cause lost in performance? I am thinking of moving the texture enabling and disabling into the Draw() method of the sprite itself.

**

Dont think It wont make any difference. 



Of course you can always test it out by doing a loop of 1000 enable texture calls each frame and see how long it takes :)

**



**


Jorge E. Covarrubias (ABND) [7 days ago]
Since it couldn't locate the authority at .com.example.android.pets, the cursor is empty and that is why we were getting that error. After fixing that, the app was able to run on my emulator.


MOCHA225 (ABND) [7 days ago]
that you.  I’m getting ready for bed and will have to work on this tomorrow.  Have a good night.  Thanks.



MOCHA225 (ABND) [6 days ago]
Jorge you are the best!  It still amazes me how such little things make such havoc.  Have a great night.
