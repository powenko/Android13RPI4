# ADB ENABLE FOR RPI4

### INSTALL ADB AND FASTBOOT

$ sudo apt update 
$ cd ~/Desktop/aosp13/
$ wget https://dl.google.com/android/repository/platform-tools-latest-linux.zip
$ sudo apt-get install unzip
$ unzip platform-tools-latest-linux.zip  
$ cd platform-tools
 


### CHECK VERSION

./adb version

### Enable

1.After booting Android, select "Setting"

2.Select "About Table"

3.Click on "Build Number" 7-8 times until it shows "you are now developer"

4.In System there will be a section "Developer options"

5.Click "Developer options"

6.Find and enable "USB debugging".

7.Reboot rpi4


### Enable wireless debugging

4.In System there will be a section "Developer options"

5.Click "Developer options"

6.Find and enable " wireless debugging".

7.pair " wireless debugging".
 


### START SERVER

$ sudo ./adb start-server

### pair

$ ./adb pair 192.168.1.110:39593

### connect

$ ./adb connect 
```

### ESTART SERVER IF ERROR
```
sudo ./adb kill-server
sudo ./adb start-server
```
### ADB CMD
```
./adb devices
./adb shell




adb shell : to connect to rpi4 to see its folders

adb devices : see connected devices.


tutorial video can see in here (https://youtu.be/2wxMM8uz8-4)
