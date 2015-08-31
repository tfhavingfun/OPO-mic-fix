# OPO-mic-fix
The mic on my Oneplus One isn't really working when I'm on a call. People always complain that they can't hear me well, even when I'm talking really close to the microphone. So here is the fix I found that fixes the issue for me. To do that, we need to change some settings inside the `build.prop` file which is located in directory `/system`. "How do I edit the file?", you ask. Well, there are two ways:

* You can edit it on the device itself using a file manager (eg, ES File Explorer)
* Or you can eit the file on your computer

I won't go into option one here, cuz I think it's more  convenient to just do it on a computer.

**Please note that your device has to be rooted to edit the `build.prop` file.**

1. We need to use adb:
  - Windows users can get this [adb/fastboot installer](http://forum.xda-developers.com/showthread.php?t=2588979). It automatically places a fastboot/adb folder on your C drive (C:\adb).
  - Linux users can search for the relevant android-tools package in your package manager.
1. Make sure your have enabled USB debugging on your phone and connect your phone to your computer.
1. Check if your device is reocgnized:
  - On Windows:
  
        cd C:\adb
        adb devices
  - On Linux: `adb devices`

1. Restart ADB as root:

        adb root
1. Remount `/system` as `rw` (read-write)

        adb remount
1. Download my `build.prop` from [here](https://github.com/tfhavingfun/OPO-mic-fix/releases).
1. Push the modified version of `build.prop` (my version) to your device.

        adb push build.prop /system/build.prop
1. Check the file permission:

        adb shell
        ls -l /system/build.prop

if it's not 644, then you need to fix the permission:
        chmod 644 /system/build.prop

**Watch for typos before you press Enter, otherwise you could fuck up your system.**

1. Reboot your device:

        adb reboot
