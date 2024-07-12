# Android13 RPI 4
build and make Android 13 image and sd card for Raspberry pi 4


## Completed Android image 
- [KonstaKANG AOSP14](https://konstakang.com/devices/rpi4/AOSP14/)
- `D:\powenko-win\20240707-RPI_Android\01_OtherVersions\AOSP14-20240704-KonstaKANG-rpi4`

This is an AOSP (Android 14) built for Raspberry Pi 4 Model B, Pi 400, and Compute Module 4. Running this version requires a Pi 4 model with at least 2GB of RAM.


# Raspberry Android Kernel Compilation by source code. 
### Ubuntu 20.04 LTS
- [Ubuntu Focal Releases](https://releases.ubuntu.com/focal/)
- Download 64-bit PC (AMD64) desktop image
- harddisk space needs 500 GB

youtube tutoirial (https://youtu.be/ORjOy6SqeC4)
### Install Required Packages
$ sudo apt-get update

$ sudo apt-get install openjdk-8-jdk android-tools-adb bc bison build-essential curl flex g++-multilib gcc-multilib gnupg gperf imagemagick lib32ncurses5-dev lib32readline-dev lib32z1-dev liblz4-tool libncurses5-dev libsdl1.2-dev libssl-dev libwxgtk3.0-gtk3-dev libxml2 libxml2-utils lzop pngcrush rsync schedtool squashfs-tools xsltproc yasm zip zlib1g-dev git-core python3.8 libncurses5 -y

$ sudo apt install python-is-python3

$ sudo apt install python3-pip

$ sudo pip3 install meson mako jinja2 ply pyyaml dataclasses

$ sudo apt install meson

### Download and Set Path for Git Repo
$ sudo apt-get update

$ mkdir ~/bin

$ PATH=~/bin:$PATH

$ curl https://storage.googleapis.com/git-repo-downloads/repo > ~/bin/repo

$ chmod a+x ~/bin/repo









### Initialize AOSP-git Repo
$ cd ~/Desktop

$ mkdir aosp14/source

$ cd aosp14/source

$ sudo ln -s /usr/bin/python3 /usr/bin/python

$ git config --global user.email "you@example.com"

$ git config --global user.name "Your Name" 


### REPO INIT
$ repo init -u https://android.googlesource.com/platform/manifest -b android-13.0.0_r61


### IMPLEMENT REPO
$ curl --create-dirs -L -o .repo/local_manifests/manifest_brcm_rpi4.xml -O -L https://raw.githubusercontent.com/raspberry-vanilla/android_local_manifest/android-13.0/manifest_brcm_rpi4.xml


### INSTALL SOURCE

$ sudo apt-get update
$ repo sync


### COMPILE

$ . build/envsetup.sh

$ lunch aosp_rpi4-userdebug

$ make bootimage systemimage vendorimage -j\$(nproc)

tutorial video(https://youtu.be/JRchgMafhZ4)
### MAKE FLASH IMAGES
./rpi4-mkimg.sh

### MAKE KERNEL
#### CREATE FOLDER KERNEL
$ cd ..

$ mkdir -p kernel/

$ cd kernel/

#### INITIALIZATION REPO KERNEL

$ repo init -u https://android.googlesource.com/kernel/manifest -b common-android13-5.15-lts

$ curl --create-dirs -L -o .repo/local_manifests/manifest_brcm_rpi4.xml -O -L https://raw.githubusercontent.com/raspberry-vanilla/android_kernel_manifest/android-13.0/manifest_brcm_rpi4.xml

INSTALL SOURCE KERNEL
$ repo sync

youtube tutiral (https://youtu.be/JQDu78zBm9A)
#### BUILD IMAGE KERNEL
$ BUILD_CONFIG=common/build.config.rpi4 build/build.sh



####Install app IMAGER for flash image rpi4
$ cd ..

$ snap install rpi-imager

####Change file ownership
$ sudo chown user:root source/out/target/product/rpi4/RaspberryVanillaAOSP13..…

1. please change RaspberryVanillaAOSP13..… to really file name
2. user:root change to your account name, for example powenko , it will change to powenko:root



####FLASH raspberry pi  micro sd card
1.click "choose os"
2.click "use custom"
3.choose imager in folder aosp/source/out/target/product/rpi4/RaspberryVanillaAOSP13-20230706-rpi4.img
4.choose ramidisk storage 
5.write flash image



##  Error & Solution
### Error 1: \`/usr/bin/env: ‘python’: No such file or directory\`
**Solution:**
$ sudo ln -s /usr/bin/python3 /usr/bin/python

### Error 2: \`Git *** Please tell me who you are.\`
**Solution:**
$ git config --global user.email "you@example.com"
$ git config --global user.name "Your Name"
