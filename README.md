# OPO-mic-fix
The main microphone on my Oneplus One isn't really working well for my phone call. People on the other side always complain that they can't hear me well, even when I'm talking really close to the microphone. So I did some search and found a solution that make the mic work a lot better than it was. At least now I don't hear people complaining about my phone call volume anymore. If you're suffering from this mic issue as well, continue reading: To fix the problem, we need to edit some settings inside the `build.prop` file which is located in directory `/system`. "How do I edit the file?", you may ask. Well, there are two ways:

* You can edit it on the device itself using a file manager (eg, ES File Explorer)
* Or you can eit the file on your computer

I won't go into details here about option one, cuz I think it's more safe and convenient to just do it on a computer.

**Please note that your device has to be rooted to edit the `build.prop` file.**

1. The first thing we'll need to do is setting up ADB on your computer:
  - Windows users can get this [adb/fastboot installer](http://forum.xda-developers.com/showthread.php?t=2588979). It automatically places a fastboot/adb folder on your C drive (C:\adb).
  - Linux users can search for the relevant `android-tools` package in your package manager. (eg, `android-tools` on Arch Linux and `android-tools-adb android-tools-fastboot` on Debian.)
1. Make sure your have enabled USB debugging on your phone and connect your phone to your computer.
1. Check if your device is recognized:
  - On Windows:
  
          cd C:\adb
          adb devices
  - On Linux: `adb devices`
1. Restart ADB as root:

        adb root
1. Remount `/system` as `rw` (read-write)

        adb remount
1. Download my already modified `build.prop` from [here](https://github.com/tfhavingfun/OPO-mic-fix/releases).
1. Push the modified version of `build.prop` (my version) to your device.

        adb push build.prop /system/build.prop
1. Check the file permission:

        adb shell
        ls -l /system/build.prop
   if it's not 644, then you need to fix the permission (**Watch for typos before you press Enter, otherwise you could fuck up your system**):

        chmod 644 /system/build.prop
1. Reboot your device:

        adb reboot
##FAQ:
###1. What exactly have you changed in the `build.prop` file?
          ## Commented the next line out to fix the mic issue
          #ro.qc.sdk.audio.fluencetype=fluence
          ## Added the next two lines to fix the mic issue
          persist.audio.fluence.voicerec=false
          persist.audio.fluence.speaker=false
      Nothing else.
