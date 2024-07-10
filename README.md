# Android13RPI4
build and make Android 13 image and sd card for Raspberry pi 4


# Raspberry Android Kernel Compilation

## Completed Files from Others
- [KonstaKANG AOSP14](https://konstakang.com/devices/rpi4/AOSP14/)
- `D:\powenko-win\20240707-RPI_Android\01_OtherVersions\AOSP14-20240704-KonstaKANG-rpi4`

This is an AOSP (Android 14) built for Raspberry Pi 4 Model B, Pi 400, and Compute Module 4. Running this version requires a Pi 4 model with at least 2GB of RAM.

**Important!** The Raspberry Pi hardware-specific implementation in this version is based on the original code released in my Raspberry Vanilla project, but this version still provides various additional features and enhancements. This image contains parts licensed under a non-commercial license (Creative Commons Attribution-NonCommercial-ShareAlike 4.0 International). You are free to use this version for personal/educational/etc. purposes. This version is not allowed for commercial use! You can contact me via email to discuss creating a customized Android version for commercial purposes.

## Using Raspberry Pi for Burning

## Screen After Boot

## Installing Google Play Market
- [Google Play Market Installation Tutorial](https://www.youtube.com/watch?v=DcIq7uS1fpQ)

## Relevant Resources
- [device_arpi_rpi4 GitHub](https://github.com/android-rpi/device_arpi_rpi4)
- [local_manifests GitHub](https://github.com/android-rpi/local_manifests/blob/arpi-14/default.xml)

## Using VM
- [Ubuntu Focal Releases](https://releases.ubuntu.com/focal/)
- Download 64-bit PC (AMD64) desktop image

## 1.1 AOSP14 — Download & Build
- [AOSP14 Download & Build Tutorial](https://medium.com/@213maheta/aosp14-download-build-0bcd99a99f84)

### Install Required Packages
\`\`\`sh
$ sudo apt-get update
$ sudo apt-get install openjdk-8-jdk android-tools-adb bc bison build-essential curl flex g++-multilib gcc-multilib gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-gtk3-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc yasm zip zlib1g-dev git-core python3.8 libncurses5 -y
$ sudo apt install python-is-python3
$ sudo apt install python3-pip
$ sudo pip3 install meson mako jinja2 ply pyyaml dataclasses
$ sudo apt install meson
\`\`\`

### Download and Set Path for Git Repo
\`\`\`sh
$ sudo apt-get update
$ mkdir ~/bin
$ PATH=~/bin:$PATH
$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo
$ chmod a+x ~/bin/repo
\`\`\`

### Initialize AOSP-git Repo
\`\`\`sh
$ cd ~/Desktop
$ mkdir aosp14
$ cd aosp14
$ sudo ln -s /usr/bin/python3 /usr/bin/python
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
$ repo init -u https://android.googlesource.com/platform/manifest -b android-14.0.0_r52
$ repo sync -j6
\`\`\`

### Build AOSP
\`\`\`sh
$ source build/envsetup.sh
$ lunch sdk_car_x86_64-userdebug
$ make -j16
\`\`\`

## 1.1.1 Error & Solution
### Error 1: \`/usr/bin/env: ‘python’: No such file or directory\`
**Solution:**
\`\`\`sh
$ sudo ln -s /usr/bin/python3 /usr/bin/python
\`\`\`

### Error 2: \`Git *** Please tell me who you are.\`
**Solution:**
\`\`\`sh
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
\`\`\`

### Expand VirtualBox Disk Space
\`\`\`sh
VBoxManage modifymedium disk "D:\VirtualBox VMs\ubuntu18Android14\ubuntu18Android14.vdi" --resize 256000
\`\`\`

### Build AOSP for Raspberry Pi
\`\`\`sh
$ source build/envsetup.sh
$ lunch sdk_car_x86_64-userdebug
$ make -j16 0
\`\`\`

## Good Tutorial Videos
- [YouTube Tutorial Video](https://www.youtube.com/watch?v=MvNb_RP9QFE)

## Technical Documentation Installation
- [Technical Documentation](https://github.com/phuthodien/android_embedded/blob/main/unit1_build_aosp_for_pi/Build_Android_Kernel_images/BuildImage.md)

### REPO INIT
\`\`\`sh
$ repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r61
\`\`\`

### IMPLEMENT REPO
\`\`\`sh
$ curl --create-dirs -L -o .repo/local_manifests/manifest_brcm_rpi4.xml -O -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-13.0/manifest_brcm_rpi4.xml
\`\`\`

### INSTALL SOURCE
\`\`\`sh
$ sudo apt-get update
$ repo sync
\`\`\`

### COMPILE
\`\`\`sh
$ . build/envsetup.sh
$ lunch aosp_rpi4-userdebug
$ make bootimage systemimage vendorimage -j\$(nproc)
\`\`\`

### MAKE FLASH IMAGES
\`\`\`sh
./rpi4-mkimg.s
\`\`\`

### MAKE KERNEL
#### CREATE FOLDER KERNEL
\`\`\`sh
$ cd ..
$ mkdir -p kernel/
$ cd kernel/
\`\`\`

#### INITIALIZATION REPO KERNEL
\`\`\`sh
$ repo init -u https://android.googlesource.com/kernel/manifest -b common-android13-5.15-lts
$ curl --create-dirs -L -o .repo/local_manifests/manifest_brcm_rpi4.xml -O -L https://raw.githubusercontent.com/raspberry-vanilla/android_kernel_manifest/android-13.0/manifest_brcm_rpi4.xml
\`\`\`

#### INSTALL SOURCE KERNEL
\`\`\`sh
$ repo sync
\`\`\`
