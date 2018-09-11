# Flutter Playground

A top-level repo containing some exemplar flutter projects.

---

## Tool chain installation

Hmmmm... well this was a little bit of an ordeal. The web is is your best 
bet, but, here are some notes for a VSCode setup for linux (skip any you already may have done):

1. __Install Java (EE)__

2. __Install Dart SDK__
    1. Install via __apt__:
        ```bash
        #!/bin/bash

        function install() {
            # Add repository
            sudo apt-get update
            sudo apt-get install apt-transport-https
            sudo sh -c 'curl https://dl-ssl.google.com/linux/linux_signing_key.pub | apt-key add -'
            sudo sh -c 'curl https://storage.googleapis.com/download.dartlang.org/linux/debian/dart_stable.list > /etc/apt/sources.list.d/dart_stable.list'
            # Install stable
            sudo apt-get update
            sudo apt-get install dart
            # Install dev
            # sudo sh -c 'curl https://storage.googleapis.com/download.dartlang.org/linux/debian/dart_unstable.list > /etc/apt/sources.list.d/dart_unstable.list'
            # sudo apt-get update
            # sudo apt-get install dart
        } && install
        ```

3. __Install Flutter SDK__
    1. Install via __curl__:
        ```bash
        #!/bin/bash

        # https://flutter.io/setup-linux/
        # https://flutter.io/sdk-archive/#linux

        # https://storage.googleapis.com/flutter_infra/releases/beta/linux/flutter_linux_v0.7.3-beta.tar.xz

        function install() {
            local version="v0.7.3-beta"
            local binary="flutter_linux_${version}.tar.xz"
            local url="https://storage.googleapis.com/flutter_infra/releases/beta/linux/${binary}"

            if [ ! -f "${binary}" ]; then
                curl -O "${url}"
            fi

            tar xvf "${binary}"
            local install_dir="${TEMOS_BIN}"
            mv flutter "${install_dir}"

            sudo apt-get install lib32stdc++6

            # Remember to add 'flutter/bin' to path!
            PATH=${PATH}:"${TEMOS_BIN}/flutter/bin"
            flutter doctor

            rm -Rf "${binary}"
        } && install

4. __Install Android Studio__
    1. Manually download, unzip, and move to desired home: https://developer.android.com/studio/#downloads
        1. android-studio-ide-173.4907809-linux.zip
        2. sdk-tools-linux-4333796.zip - Optional?
    2. Unzip and move to desired ```bin``` directory.
    3. Update __.bashrc__ to add binaries to your path and smooth over some kinks:
        ```
        ANDROID_STUDIO_HOME="${TEMOS_BIN}/android-studio"
        if [ -d "${ANDROID_STUDIO_HOME}" ]; then
            export "${ANDROID_STUDIO_HOME}"
            export PATH=${PATH}:"${ANDROID_STUDIO_HOME}/bin"
            alias sdkmanager="JAVA_OPTS='-XX:+IgnoreUnrecognizedVMOptions --add-modules java.se.ee' sdkmanager"
            alias android-studio="${ANDROID_STUDIO_HOME}/bin/studio.sh &"
        fi
        ```
    4. Install Android Studio Dart Plugin (from IDE plugin manager).
    5. Install Android Studio Flutter Plugin (from IDE plugin manager).

7. __Create an emulator device__
    1. Install _qemu-kwm__: ```sudo apt install qemu-kvm```
    2. Ensure your user has acces to '/dev/kvm': ```sudo adduser $USER kvm```
    3. Open 'android-studio', navigate to 'Tools/AVDManager'.
    4. Create one or more virtual devices. I chose the 'Google Pixel 2 XL'.

7. __Install VSCode__.
    1. Install.
    2. Install VSCode __Dart Plugin__ (from IDE plugin manager).
    3. Install VSCode __Flutter Plugin__ (from IDE plugin manager).

8. __Test__
    1. Run ```flutter doctor --android-licenses```.
    2. Create flutter project ```flutter create flutter_demo```
    3. Open project folder in VSCode.
    4. [Optional] Set up emulator: ```<ctrl+shift+p> Setup Device```.
    5. [Optional] Run emulator: ```<ctrl+shift+p> Flutter Launch Emulator```.
    6. Run! ```flutter run```

---

## Project Commands

### Create new project

```
flutter create <project name>

```

---

## Auxillary Commands

### Run project

```
flutter run
```

### Update License

```
flutter doctor --android-licenses
```
