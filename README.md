# Docker Project Tango Development Environment

This is an Android Studio docker development environment created for [Google's Project Tango](https://www.google.com/atap/project-tango/).  I built this as a fast way to spin-up a Project Tango development environment for myself, but I am happy to integrate suggestions and improvements.

It was made to run on an Ubuntu 14.04 host, but should work under other versions of Linux and OSX (using XQuartz & Docker-Machine) without too much tweaking.  I haven't used Windows much for Docker, so I can't really say how well it will work.


## Using container

1. Make sure you have Git, Docker, and Docker-Compose installed on your machine.
2. Clone this repo: `git clone git@github.com:toddsampson/project-tango-docker.git && cd project-tango-docker`
3. IMPORTANT: If your host computer user and group IDs aren't set to 1000, update the `android-studio/Dockerfile` to the correct values and use use the `build` command instead of `image` in the docker-compose.yml.
4. Run `xhost +` to allow the container to communicate with your host system's X server
5. Run `docker-compose run android-studio`
6. Once the container starts, run `studio.sh` to start Android Studio and run through setup

## TODO: Walk through tutorial example in depth as a getting started


## Notes

* You must have a Project Tango device.  There is not Project Tango emulator that can be used for development.
* Example projects are found in the `/srv` directory
* The ndk.dir path for [Project Tango tutorials](https://developers.google.com/project-tango/apis/c/) and your own projects should be set to `ndk.dir=/home/android/Android/android-ndk-r10e` in `local.properties` for the project.
sudo chown android:android -R /home/android/Android/android-ndk-r10e



## What's Included

* [Android Studio IDE and SDK Tools](http://developer.android.com/sdk/index.html)
* [Android NDK](http://developer.android.com/tools/sdk/ndk/index.html)
* [Project Tango C API, Java API and Unity SDK](https://developers.google.com/project-tango/)
* [Project Tango code samples and tutorials](https://github.com/googlesamples)
* [Oracle JVM](http://www.oracle.com/technetwork/java/javasebusiness/downloads/java-archive-downloads-jvm-419420.html)
* Docker-Compose launch script example
* Well-commented Dockerfile that can easily be customized for your project
* UDEV rules to enable Project Tango Device (and other Google Vendor ID products)
* All required Linux library & package dependencies
* A few convenience tools I have found helpful
* Non-root Linux user with user and group IDs matched to the host system to allow graphical windows to be forwarded to the host's X server


Cheers,
Todd
