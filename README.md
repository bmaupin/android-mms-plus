# android-sms-plus
Stock Android SMS app with one additional feature: automatically enable/disable mobile data when sending/receiving MMS messages

Installation
---

Requirements:
- Android 4.4 KitKat (no clue if it will work on any other release)
- Rooted

Steps:

1. Download Mms.apk from [releases](https://github.com/bmaupin/android-sms-plus/releases)
2. Overwrite stock Mms.apk on your device. This can be done using a file manager app with root privileges, or using the command line:
   1. Push Mms.apk to your device

            adb push Mms.apk /sdcard/

   3. Connect to your device and become root

            adb shell
            su

   4. Get the system drive for your device  

            mount | grep system
            
   5. Remount the system partition as read-write using the mount point you got from the previous step. Ex:

            mount -o rw,remount /dev/block/mmcblk0p9 /system
            
   6. Remove the existing Mms.apk

            mkdir /sdcard/mms-backup
            mv /system/app/Mms.apk /sdcard/mms-backup/
            mv /system/app/Mms.odex /sdcard/mms-backup/
            mv /system/priv-app/Mms.apk /sdcard/mms-backup/
            mv /system/priv-app/Mms.odex /sdcard/mms-backup/
            
   7. Copy the new Mms.apk and set permissions

            cp /sdcard/Mms.apk /system/priv-app
            chmod 644 /system/priv-app/Mms.apk

   6. Remount the system partition as read-only using the mount point you got earlier. Ex:
  
            mount -o ro,remount /dev/block/mmcblk0p9 /system

3. Reboot


Building
---

See: [Building](https://github.com/bmaupin/android-sms-plus/wiki/Building)
