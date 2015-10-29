# Docker Project Tango Development Environment

This is an Android Studio development environment created for [Google's Project Tango](https://www.google.com/atap/project-tango/) using Docker.  I built this as a fast way to spin-up a Project Tango development environment for myself, but I am happy to integrate suggestions and improvements.

It was made to run on an Ubuntu 14.04 host, but should work under other versions of Linux and OSX (using XQuartz & Docker-Machine) without too much tweaking.  I haven't used Windows much for Docker, so I can't really say how well it will work.

Note: You must have a Project Tango device to use this Docker Image.  Google has not yet made a Project Tango emulator to use for development.


## Setting Up the Docker Container

1. Make sure you have Git, Docker, and Docker-Compose installed on your machine.
2. Clone this repo: `git clone git@github.com:toddsampson/project-tango-docker.git && cd project-tango-docker`
3. IMPORTANT: If your host computer user and group IDs aren't set to 1000, update the `android-studio/Dockerfile` to the correct values and use the `build` command instead of `image` in the docker-compose.yml.
4. Run `xhost +` to allow the container to communicate with your host system's X server.
5. If you don't have an `AndroidStudioProjects` folder on your host computer, create one.  Then update `/home/toddsampson/AndroidStudioProjects` in docker-compose.yml with the path to your project folder; leaving everything after the ":" unchanged.
6. Plug-in and turn-on your Project Tango device.
7. Run `docker-compose run android-studio` which will setup the Docker Container and launch a Bash terminal.
8. Run `studio.sh` to start Android Studio. Unless you need specific customizations, simply click `Next` a few times to begin installation of the SDK.
9. During the SDK install the Project Tango device should show an `Allow USB debugging` alert.  When it does, check the `Always allow from this computer` box and click `OK.`
10. Wait for the SDK to finish installing and click `Finish` to complete setup.


## Getting Started Using the Container

Once Android Studio has been setup, you can run through the Project Tango examples found in the Docker Container's `/srv` directory.  We will walk through the `/srv/tango-examples-c/hello-tango-jni-example` as a quick getting-started.

1. From the Android Studio launch screen select `Import Project (Eclipse, ADT, Gradle, etc.)`
2. Select the `/srv/tango-examples-c/hello-tango-jni-example` folder and click `OK`
3. You will likely get a number of messages about missing SDKs, built tools and plugins from Gradle.  Each time, click the `Install missing platform/build tools and sync project` or `Fix plugin version and sync project` followed by `Finish.` After Gradle stops showing you these messages, usually three screens, proceed to the next step.
5. Click on the word `Project` printed vertically on the left side of Android Studio.
6. In the file window that appeared when clicking Project, double-click on `Gradle Scripts.`  Then double-click on `local.properties.`
7. In the local.properties file, add `ndk.dir=/home/android/Android/android-ndk-r10e` below the `sdk.dir=...` line and save the file.  This will allow Gradle to know where to find the Android NDK.
8. Press the green play button (Run App) in Android Studio.  Select `Google Project Tango Tablet Development Kit...` under Choose a running device, check `Use same device for future launches` and click `OK.`
9. The app should launch on your Project Tango device.  If you receive a message to enable Motion Tracking, accept it.  If not, press the home button on your Project Tango device and re-run step eight.
10. If all went well you should be able to move your Project Tango device around and see the values being displayed in Android Studio via the Android Debugging Bridge (ADB).  You are now ready to run through the rest of the examples or begin building your own application.


## What's Included

* [Android Studio IDE and SDK Tools](http://developer.android.com/sdk/index.html)
* [Android NDK](http://developer.android.com/tools/sdk/ndk/index.html)
* [Project Tango C API, Java API and Unity SDK](https://developers.google.com/project-tango/)
* [Project Tango code samples and tutorials](https://github.com/googlesamples)
* [Oracle JVM](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-jvm-419420.html)
* Docker-Compose launch script example
* Well-commented Dockerfile that can easily be customized for your project
* UDEV rules to enable Project Tango Device (and other Google Vendor ID products)
* All required Linux libraries & package dependencies
* A few convenience tools I have found helpful
* Non-root Linux user with user and group IDs matched to the host system to allow graphical windows to be forwarded to the host's X server


Cheers,
Todd
