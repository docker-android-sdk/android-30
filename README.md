# Docker for Android SDK 30

Docker for Android SDK 30 with preinstalled build tools and emulator image

> Edit from [mindrunner/docker-android-sdk](https://github.com/mindrunner/docker-android-sdk)

**Installed Packages**
```bash
# sdkmanager --list
  Path                                        | Version | Description                                | Location
  -------                                     | ------- | -------                                    | -------
  build-tools;30.0.2                          | 30.0.2  | Android SDK Build-Tools 30.0.2             | build-tools/30.0.2/
  cmdline-tools;latest                        | 2.1     | Android SDK Command-line Tools (latest)    | cmdline-tools/latest/
  emulator                                    | 30.1.5  | Android Emulator                           | emulator/
  patcher;v4                                  | 1       | SDK Patch Applier v4                       | patcher/v4/
  platform-tools                              | 30.0.4  | Android SDK Platform-Tools                 | platform-tools/
  platforms;android-30                        | 3       | Android SDK Platform 30                    | platforms/android-30/
  system-images;android-30;google_apis;x86_64 | 8       | Google APIs Intel x86 Atom_64 System Image | system-images/android-30/google_apis/x86_64/
```

**Usage**

- Interactive way
  ```bash
  $ docker run -it --rm --device /dev/kvm androidsdk/android-30:latest bash
  # check installed packages
  $ sdkmanager --list
  # create and run emulator
  $ avdmanager create avd -n first_avd --abi google_apis/x86_64 -k "system-images;android-30;google_apis;x86_64"
  $ emulator -avd first_avd -no-window -no-audio &
  $ adb devices
  # You can also run other Android platform tools, which are all added to the PATH environment variable
  ```

  To connect the emulator using `adb` on the docker host machine, start the container with `--network host` as well.
  You could also use [`scrcpy`](https://github.com/Genymobile/scrcpy) to do a screencast of the emulator.

- Non-interactive way
  ```bash
  # check installed packages
  $ docker run -it --rm androidsdk/android-30:latest sdkmanager --list
  # list existing emulators
  $ docker run -it --rm androidsdk/android-30:latest avdmanager list avd
  # You can also run other Android platform tools, which are all added to the PATH environment variable
  ```