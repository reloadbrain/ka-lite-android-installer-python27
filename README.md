ka-lite-android-python27
================

The objective of this project is to create an APK for Ka-lite and make it runs on the embeded Python-for-Android interpreter. Therefore, user can use this app as a LAN server to serve open-scoure educational contents, or consume the content within the app's webview, without the access to the Internet.

More details about Ka-lite can be found here:

Wiki: https://github.com/learningequality/ka-lite/wiki

More details about how to use android-python27 can be found here:

Wiki: http://code.google.com/p/android-python27/w/list

----
*Overview:* 

  * To use this project in Eclipse, just go to `File->Import` and select the `apk` folder. 

  * Because we use webview for rendering the user interface, and the webview is not chromium based until Android 4.4, we embeded a chromium based webview runtime, Crosswalk, into this project. You will need to download crosswalk-webview-10.39.235.15-arm(https://download.01.org/crosswalk/releases/crosswalk/android/stable/10.39.235.15/) and follow this link(https://crosswalk-project.org/documentation/embedding_crosswalk.html) to embed Crosswalk. It's recommended that you then run `Project->clean` to generate the `R.java`. If your target device is Android 4.4 only, you can skip this part and modify the code in `ScriptActivity.java` to use the default webview instead.

  * Becasue Ka_Lite is a pure Python project, we can zip the whole Ka-Lite project (https://github.com/learningequality/ka-lite) into the `ka_lite.zip` file under `res/raw` folder. This repo already contains the lastest Ka_Lite 0.16 zip file uder the `raw` folder. Ka_Lite 0.16 is still in development, which offers huge performance improvement, but also has some known issues, such as cannot downloading videos right now. We will update the zip file again as soon as Ka_Lite 0.16 merged into master. This repo only serves as a demo to show the posibility of running Ka_Lite on Android.

  * The Python interpreter, including all binaries and modules, should be zipped into an archive and also placed inside the `res/raw` directory. The template already has a zip archive containing the Python interpreter in this directory, so you don't need to change this if your APK runs fine. You can add modules that are needed for your scripts or remove them just by editing the files in this zip archive, or you can use your own Python build by replacing this zip archive with one containing your Python build (see the last bullet point below in this section about naming).

  * If you change the name of the main Python script (`kalitectl.py`) or the name of the zip archive containing your Python scripts, then in `src/GlobalConstants.java` change the values for: `Python_MAIN_SCRIPT_NAME` and `PYTHON_PROJECT_ZIP_NAME` respectively.

  * If you change the name of the zip archive containing the Python interpreter and the Python extras, then in `src/GlobalConstants.java` change the values for: `PYTHON_NICE_NAME`, `PYTHON_ZIP_NAME`, and `PYTHON_EXTRAS_ZIP_NAME` respectively.

*python-build*: 

  * Currently the `apk` project template above contains Python version 2.7.2 already built and included inside the `apk/res/raw` directory, so there's no need to build Python yourself. 

  * If you wish to build other Python version however, you'll find the source code in `python-build` (see README). This will build Python and create the `python_27.zip` and `python_extras_27.zip` archives to replace the ones located inside the `apk/res/raw` directory.

----
*How to run the app:* 
	
  * This APK only works for Android 4.1 to 4.4. Due to the hard requirement of PIE(Position Independent Execution) on Lollipop, the Python build for this repo cannot be run on Android 5.0 and above. We have figured out a way to run python on Lollipop without root privilege and will publish it after Ka-Lite 0.16 is released.

  * Once the APK is successfully genereated, it will take about 5 mins to install on your android device. After installation, it will ask you to locate the content folder, which you can extract from the Ka-Lite develop repo(https://github.com/learningequality/ka-lite/tree/develop). Just select the `content` and `data` folders from the root directory and put them into a folder and name it whatever you wish. Put this folder into your Android device or SD card so that you can select it from the app. If the app does not see the `content` and `data` folders, it will refuse to start the server.

----

Based on:

- https://code.google.com/p/android-python27/

- https://github.com/nonameentername

- https://code.google.com/p/python-for-android/

- https://code.google.com/p/android-scripting/

- https://crosswalk-project.org/

- https://seattle.cs.washington.edu/browser/seattle/trunk/dist/android/SeattleOnAndroid
