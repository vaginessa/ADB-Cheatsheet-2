# ADB-Cheatsheet-2


Commands for android-tools

### Start ADB server:

    adb start-server 

### Stop ADB server:

    adb stop-server

### Kill ADB server: 

    adb kill-server

### Setup ADB server via Wi-Fi

    adb tcpip <port>
    
### Connect to ADB server: 

    adb connect <device_ip>

### Restarts the adbd daemon listening on USB

    adb usb
    
### Reboot - Default, system reboot

    adb reboot

### Reboot - Recovery Mode

    reboot recovery

### Reboot - Bootloader Mode

    reboot bootloader

### List Connected Devices: 

    adb devices

### Get Status:

    adb get-state  
  
### Print Serial Number:

    adb get-serialno 
    
### Backup Device:

    adb backup -all
    
### Restore Device:

    adb restore /path/to/backupflile.adb

### Enter ADB shell:

    adb shell

### Enter ADB shell if there is multiple devices connected:

    adb -s <id_from_adb_devices> shell 

### To print device serial no: 

    adb get-serialno

### Create a bugreport: 

    adb bugreport

### Install an app:

    adb install <apk_file>

### Install an app and keep all it's data from a previous setup: 

    adb install -r <apk_file>

### Uninstall an app: 

    adb uninstall <apk_file>
   
### Set date: 

    date MMDDYYYY.XX;am broadcast -a android.intent.action.TIME_SET

### Push a file (Transfer a file FROM pc > device)

    push mypicture.png /storage/on/device

### Push a folder (Transfer a folder FROM pc > device)

    push myfolder /storage/on/device

### Pull a file (Transfer a file FROM device > pc)

    adb pull /storage/on/device/mypicture.png /path/on/pc

### Pull a folder (Transfer a folder FROM device > pc)

    adb pull /storage/on/device /path/on/pc

### Pull all files inside a folder to a path (Transfer all files in a folder FROM device > pc)

    adb pull /storage/on/device/ /path/on/pc # Notice the trial slash
    
# ADB package manager (please use cmd, it's alot faster then old pm) 

### CMD

### List uid owner of a app

    cmd package list packages -U                                           

### List packages a.k.a: pm list packages

    cmd package list packages -l                                          

### List disabled packages
    cmd package list packages -d
    
### Filter to only show enabled packages     
    cmd package list packages -e                                       

### Filter to only show third party packages    

    cmd package list packages -3                                                 

### Set the default home activity (aka launcher)

    cmd package set-home-activity [--user USER_ID] TARGET-COMPONENT        
    
### Prints all features of the system

    cmd package list features 
    
###  Print briefs

    cmd package resolve-activity --brief  com.facebook.katana        
    priority=0 preferredOrder=0 match=0x108000 specificIndex=-1 isDefault=false
    com.facebook.katana/.LoginActivity

### PM 

### List all packages installed on device 

    pm list packages

### List enabled packages

    pm list packages -e
    
### List disabled packages

    pm list packages -d

### List third party packages installed by user

    pm list packages -3

### List users

    pm list users

### List permission groups

    pm list permission-groups

### List features
 
    pm list features

### Uninstall any installed package:

    pm uninstall --user 0 com.package.name

### Uninstall multiple apps:

    for packages in com.package1 com.package2; do 
        adb shell pm uninstall --user 0 "${packages}"
    done 

### Clear application data:

    pm clear PACKAGE_NAME

### List permission groups: 

    pm list permission-groups 

### List instrumentation:

    pm list instrumentation

### Grant permission to an app (Example Only For Grant): 

    pm grant com.application android.permission.READ_LOGS
    
    
### Revoke permission to an app (Example Only For Revoke): 

    pm revoke com.application android.permission.READ_LOGS

### Reset all permissions for an app:

    pm reset-permissions -p your.app.package
    
# LOGCAT

### Default options: 

* V — Verbose (lowest priority)
* D — Debug
* I — Info (default priority)
* W — Warning
* E — Error
* F — Fatal
* S — Silent (highest priority, on which nothing is ever printed)

### Use -v time for print timestamps, and threadtime for dates:

    adb logcat -v time ...
    adb logcat -v threadtime ....

### For get output colorized with logcat:

    adb logcat ... -v color

### Displays current log buffer sizes:

    adb logcat -g   

### Sets the buffer size (K or M):

    adb logcat -G 16M   

### Clear the log buffer:

    adb logcat -c

### Enables ALL log messages (verbose mode)

    adb logcat *:V  

### Dump everything to a file:

    adb logcat -f <filename>    Dumps to specified file

### Display PID with the log info 

    adb logcat -v process

### Display the raw log message, with no other metadata fields

    adb logcat -v raw

### Display the date, invocation time, priority/tag, and PID of the process issuing the message

    adb logcat -v time

#### Display the priority, tag, and the PID and TID of the thread issuing the message

    adb logcat -v thread

### Display the date, invocation time, priority, tag, and the PID and TID of the thread issuing the message

    adb logcat -v threadtime

### Display all metadata fields and separate messages with blank lines

    adb logcat -v long
    
### Log multiple options (-b ... -b ....): 

    adb logcat -b main -b radio -b events

# DUMPSYS

### List all active services:

    dumpsys -l 
    
    oln older devices
    
    dumpsys -l |sed 's/^  /      /g'
    Currently running services:
      AAS
      AODManagerService
      CCM
      CocktailBarService
      CodecSolution
      CustomFrequencyManagerService
      DeviceRootKeyService
      DirEncryptService
      DisplaySolution
      DockObserver
      EngineeringModeService
      HqmManagerService
      ImsBase
      OcfKeyService
      ReactiveService
      SEAMService
      SamsungKeyProvisioningManagerService
      SatsService
      SecExternalDisplayService
      ...................

### Examples:

### Show bluetooth macaddr, bluetooth name and such things:

    dumpsys bluetooth_manager

### List all settngs and if they are true or false:

Settings are sorted for root and user:

     GLOBAL SETTINGS (user 0)
     SECURE SETTINGS (user 0)
     SYSTEM SETTINGS (user 0)
     SECURE SETTINGS (user 95)
     SYSTEM SETTINGS (user 95)


    dumpsys settings
    _id:225 name:lock_screen_show_notifications pkg:com.android.settings value:1 default:1 defaultSystemSet:true
    _id:6 name:volume_bluetooth_sco pkg:android value:7 default:7 defaultSystemSet:true
    _id:192 name:ringtone_set pkg:com.google.android.gsf value:1
    _id:159 name:lock_screen_allow_rotation pkg:android value:0 default:0 defaultSystemSet:true
    _id:2997 name:Flashlight_brightness_level pkg:com.android.systemui value:1001 default:1001 defaultSystemSet:true
    _id:67 name:SEM_VIBRATION_NOTIFICATION_INTENSITY pkg:android value:5 default:5 defaultSystemSet:true
    _id:175 name:call_popup pkg:android value:0 default:0 defaultSystemSet:true
    _id:59 name:install_non_market_apps pkg:android value:1 default:1 defaultSystemSet:true
    .....

### Display Contacts On Sim Card:

    dumpsys simphonebook

### Show hardware info as thermal stuff for cpu, gpu and battery

     dumpsys hardware_properties
    ****** Dump of HardwarePropertiesManagerService ******
    CPU temperatures: [38.0, 38.0]
    CPU throttling temperatures: [55.0, 76.0]
    CPU shutdown temperatures: [115.0, 115.0]
   
### Show all application you have an account on: 

    dumpsys account|grep -i com.*$ -o|cut -d' ' -f1|cut -d} -f1|grep -v com$
    com.microsoft.workaccount
    com.skype.raider
    com.samsung.android.mobileservice
    com.facebook.messenger
    com.google.android.gm.exchange
    .......
    
### Show all notifications listener and so on:

    dumpsys notification
    
### List email addresses registerd on different stuff on device:

    dumpsys | grep -E -o "\b[A-Za-z0-9._%+-]+@[A-Za-z0-9.-]+\.[A-Za-z]{2,6}\b"
    
### Print version of a specifik package

    dumpsys package com.lge.signboard | grep versionName
    versionName=6.00.170603-0
    
### Check state for screen and figoure how device was unlcked last time:

    dumpsys  user
    ...
    State: RUNNING_UNLOCKED
    ...
    Last logged in fingerprint
    .....
    agree Knox Privacy Policy: false
    
### And for example, you can dump data for all of the running services: 
### Dump all data for battery: 

    adb shell dumpsys battery

### Dump stats for your battery:

    adb shell dumpsys batterystats 

### Erase old stats for battery:
 
    dumpsys batterystats --reset 

### Sort Applications By Ram Usage:

     dumpsys meminfo

    Applications Memory Usage (in Kilobytes):
    Uptime: 29602806 Realtime: 57806941

    Total PSS by process:
    265,435K: com.android.systemui (pid 4190)
    264,671K: system (pid 3838)
    171,192K: surfaceflinger (pid 3360)
    152,523K: android.hardware.graphics.composer@2.1-service (pid 3338)
    128,781K: com.sec.android.app.launcher (pid 5597 / activities)
     92,656K: se.kronansapotek.kronan (pid 26729 / activities)
     84,563K: logd (pid 3203)
     80,944K: com.google.android.talk (pid 32314 / activities)
     79,754K: com.google.android.googlequicksearchbox:search 
     
# DUMPSTATE

### Dump info about your sim provider and kernel bootloader ID etc.

    dumpstate -v

    ========================================================
    == dumpstate: 2019-08-30 19:31:05
    ========================================================

    Build: PPR1.180610.011.G950FXXS5DSF1
    Build fingerprint: 'samsung/dreamltexx/dreamlte:9/PPR1.180610.011/G950FXXS5DSF1:user/release-keys'
    Bootloader: G950FXXS5DSF1
    Radio: G950FXXS5DSF1
    Network: Comviq
    Linux version 4.4.111-16019454 (dpi@21DHA724) (gcc version 4.9.x 20150123 (prerelease) (GCC) ) #1 SMP PREEMPT Mon Jun 3     20:16:50 KST 2019
    Kernel: Command line: (unknown)
    up 0 weeks, 0 days, 16 hours, 21 minutes
    Uptime: Bugreport format version: 2.0
    Dumpstate info: id=0 pid=26940 dry_run=0 args=dumpstate -v extra_options=

     
# AM

### Factory Reset:

    am broadcast -a android.intent.action.MASTER_CLEAR

### Open Special Menu

    am start -a android.intent.action.VIEW \

### Open settings:

     am start -n com.android.settings/com.android.settings.Settings

### Open activity to new APN

     am start -a android.intent.action.INSERT  content://telephony/carriers  --ei simId 

### Open hiden menu (require root)

    su -c "am broadcast -a android.provider.Telephony.SECRET_CODE -d android_secret_code://IOTHIDDENMENU"

### Start prefered webbrowser:

    am start -a android.intent.action.VIEW -d <url> (com.android.browser | com.android.chrome | com.sec.android.sbrowser) 

### Print Activities:
    
    am start -a com.android.settings/.wifi.CaptivePortalWebViewActivity

### Open Camera ( take photo with key event 66)

    am start -a android.media.action.IMAGE_CAPTURE

## Open Video Camera

    am start -a android.media.action.VIDEO_CAMERA

#### Open a picture and then set wallpaper by:

    am start -a android.intent.action.SET_WALLPAPER

### Open a url with your default browser

    am start -a android.intent.action.VIEW -d https://github.com/wuseman

### Open google maps with coordinates

    am start -a android.intent.action.VIEW -d "geo:46.457398,-119.407305"

### Enabling Night Mode (If Supported)
    
    am start --ez show_night_mode true com.android.systemui/.tuner.TunerActivity

# IMEI:

### Print IMEI (Method 1)

    service call iphonesubinfo 1| cut -d "'" -f2| grep -Eo '[0-9]'| xargs| sed 's/\ //g'  
    
## Print IMEI 1 & 2 (Method 2)

#### Imei 1:
    
    service call iphonesubinfo 3 i32 1 | grep -oE '[0-9a-f]{8} ' | while read hex; do echo -ne "\u${hex:4:4}\u${hex:0:4}"; done; echo          

#### Imei 2: 
       
    service call iphonesubinfo 3 i32 2 | grep -oE '[0-9a-f]{8} ' | while read hex; do echo -ne "\u${hex:4:4}\u${hex:0:4}"; done; echo       
    
### List how many times we booted device:

    settings list global|grep "boot_count="|cut -d= -f2|head -n 1|xargs echo "Booted:"|sed 's/$/ times/g'
    
### Send SMS:

    am broadcast -a com.whereismywifeserver.intent.TEST --es sms_body "test from adb"

### Simulate waking your app using the following commands:

    am set-inactive <packageName> 
    am set-inactive <packageName> false
    
### Start facebook application inbox by using URI

    am start -a android.intent.action.VIEW -d facebook://facebook.com/inbox
  
### Open a vcard file from sdcard (will open contacts app :) )

    am start -a android.intent.action.VIEW -d file:///sdcard/me.vcard -t text/x-vcard  

### Open an application to get content (in this case to get a jpeg picture)

    am start -a android.intent.action.GET_CONTENT -t image/jpeg

### There is several ways to send a SMS via AM, here is one example:

    aam broadcast -a com.whereismywifeserver.intent.TEST --es sms_body "test from adb"

### Trick device that setup already has been done:

     content insert --uri content://settings/secure --bind name:s:user_setup_complete --bind value:s:1
     am start -n com.google.android.gsf.login/
     am start -n com.google.android.gsf.login.LoginActivity

# GETPROP

There is to much to describe here, get info by type getprop, but you can for example grep various stuff by:

    getprop | grep "model\|version.sdk\|manufacturer\|hardware\|platform\|revision\|serialno\|product.name\|brand"

# MiSC

### Try vibrator
 
    echo 200 > /sys/class/timed_output/vibrator/enable

### Open settings for a specifik app

    am start -a android.settings.APPLICATION_DETAILS_SETTINGS package:<com.package.example>

### Adopting USB-Drive
 
    sm set-force-adoptable true

### Auto rotation on

    content insert –uri content://settings/system –bind name:s:accelerometer_rotation –bind value:i:1

### Auto rotation off:
    
    content insert –uri content://settings/system –bind name:s:accelerometer_rotation –bind value:i:0

### Rotate to landscape

     content insert —uri content://settings/system –bind name:s:user_rotation –bind value:i:1

### Rotate portrait

     content insert –uri content://settings/system –bind name:s:user_rotation –bind value:i:0

### Genereate hash from keystore  -Typically used in Facebook

    keytool -exportcert -alias your_alias -keystore debug.keystore | openssl sha1 -binary | openssl base64 

# Typically used in Google Maps

    keytool -list -v -keystore ~/.android/debug.keystore -alias your_alia           

### Print Screen Size

    wm size

### Set Screen Size

    wm size WxH 
    
### Set Overscan:

    wm overscan 0,0,0,200

### Tips & Tricks

### See current used app:

    dumpsys window windows | grep -E 'mCurrentFocus|mFocusedApp'|grep '/'|awk -F'u0' '{print $2}'|awk '{print $1}'

### Print how many notifications you have: 

    dumpsys notification | grep NotificationRecord | wc -l 

### Simulate a swipe down for notifications:

    input swipe 0 0 0 300 
    
### Swipe and unlock screen:

    input swipe 300 1000 300 500 
    
### Test any app by pressing 10000 times at once, this will start your application and perform 10000 random events.# 

    monkey -p com.example.myapp -v 10000 

### Print all application in use in a for loop 

    pm list packages | sed -e "s/package://" | while read x; do cmd package resolve-activity --brief $x | tail -n 1 | grep -v "No activity found";done 
    com.google.android.youtube/.app.honeycomb.Shell$HomeActivity
    com.google.android.googlequicksearchbox/.SearchActivity
    com.google.android.apps.docs.editors.docs/com.google.android.apps.docs.app.NewMainProxyActivity
    com.android.documentsui/.LauncherActivity
    com.google.android.apps.docs.editors.sheets/com.google.android.apps.docs.app.NewMainProxyActivity
    com.google.android.apps.docs.editors.slides/com.google.android.apps.docs.app.NewMainProxyActivity
    com.android.vending/.AssetBrowserActivity
    .....
    
### Open Projectmenu (Huawei only)

    am start com.huawei.android.projectmenu/com.huawei.android.projectmenu.ProjectMenuActivity

### Auto answer any call after 2 seconds:

    setprop persist.sys.tel.autoanswer.ms 2000

### Turn off auto answer:
 
    setprop persist.sys.tel.autoanswer.ms 0

### Unplug AC:

    dumpsys battery unplug

### Print uptime for your device by days + time

    TZ=UTC date -d@$(cut -d\  -f1 /proc/uptime) +'%j %T' | awk '{print $1-1"d",$2}'

### Add a contact

## Example 1:

    am start -a android.intent.action.INSERT -t vnd.android.cursor.dir/contact -e name "$(dialog --stdout --inputbox 'wuseman' 0 0)" -e postal "$(dialog --stdout --inputbox 'Postal Address' 0 0)" -e phone "$(dialog --stdout --inputbox 'Phone Number' 0 0)" -e email "$(dialog --stdout --inputbox 'Email' 0 0)"
    
## Example 2: 

    am start -a android.intent.action.INSERT -t vnd.android.cursor.dir/contact -e name 'wuseman' -e phone <phone_number>

# GETPROP

### Is OEM unlocking enable or not

      getprop sys.oem_unlock_allowed 
      
 ### Is sys boot completed:
 
      getprop sys.boot_completed

# Fastboot

### Print device info

    
    fastboot getvar all
    
    (bootloader) version:0.5
    (bootloader) variant:MTP eMMC
    (bootloader) secure:yes
    (bootloader) version-baseband:
    (bootloader) version-bootloader:
    (bootloader) display-panel:
    (bootloader) off-mode-charge:0
    (bootloader) charger-screen-enabled:0
    (bootloader) max-download-size: 0x20000000
    (bootloader) partition-type:cache:ext4
    (bootloader) partition-size:cache:       0x20000000
    (bootloader) partition-type:userdata:ext4
    (bootloader) partition-size:userdata:    0x5ba000000
    (bootloader) partition-type:system:ext4
    (bootloader) partition-size:system:      0x15d800000
    (bootloader) dm_count:0
    (bootloader) lock_count:1
    (bootloader) unlock_count:2
    (bootloader) serialno:LGH87011067135
    (bootloader) kernel:lk
    (bootloader) product:MSM8996
    (bootloader) unlocked:yes

### Fastboot commands

    fastboot erase config
    fastboot reboot
    fastboot oem get-psid                               #_Print_Serial_and_IMEI
    fastboot getvar rescue_version                      #_Print_rescue_mode
    fastboot getvar rescue_phoneinfo                    #_Print_phone_model
    fsatboot getvar_vendorcountry                       #_Print_vendorcountry
    fastboot getvar rescue_ugs_port                     #_Print_rescue_ugs_port
    fastboot getvar rescue_enter_recovery               #_Enter_recovery
    fastboot getvar max-download-size                   #_Print_max_download_size
    fastboot getvar error_print                         #_Print_amount_of_errors
    fastboot getvar partition-type                      #_Print_partition_type
    fastboot oem get_key_version                        #_Print_version_key
    fastboot oem battery_present_check                  #_Print_battery_millivolt
    fastboot continue                                   #_Fastboot_continue
    fastboot oem get_hwnff_ver                          #_Get_hwnff_version
    fastboot oem reboot_boot_dump                       # UNKNOWN
    fastboot getvar rescue_version                      # Print rescue version
    fastboot getvar rescue_phoneinfo                    # Print rescue model
    fastboot getvar devicemodel                         # Print device model
    fastboot getvar rescue_ugs_port                     # Print rescue port
    fastboot getvar error_print                         # Error Print
    fastboot getvar rescue_enter_recovery               # Enter recover
    fastboot getvar rescue_get_hwid                     # (bootloader) xxxxxxxxxxxx / xxxxxxxxxxxx (bootloader) 
    fastboot getvar inject_bootfail_memory_address      # NO DESCRIPTION - FOUND WHEN I CRACKED THE BOOTLOADER
    fastboot getvar rescue_get_updatetoken              # NO DESCRIPTION - FOUND WHEN I CRACKED THE BOOTLOADER
    fastboot getvar max-download-size                   # NO DESCRIPTION - FOUND WHEN I CRACKED THE BOOTLOADER
    fastboot oem check-rootinfo                         # NO DESCRIPTION - FOUND WHEN I CRACKED THE BOOTLOADER
    fastboot oem get-bootinfo                           # NO DESCRIPTION - FOUND WHEN I CRACKED THE BOOTLOADER
    fastboot oem get-product-model                      # NO DESCRIPTION - FOUND WHEN I CRACKED THE BOOTLOADER
    fastboot oem get-build-number                       # NO DESCRIPTION - FOUND WHEN I CRACKED THE BOOTLOADER
    fastboot oem unlock
    fastboot oem check-image                            
    fastboot oem relock
    fastboot oem frp-unlock
    fastboot oem get_key_version
    fastboot oem battery_present_check
    fastboot oem unlock_func
    fastboot oem get_hwnff_ver
    fastboot getvar error_print
    fastboot oem oeminforead
    fastboot oem get_bootFail_ver_func
    fastboot oem func
    fastboot oem get_bootFail_info_func
    fastboot oem relock_func
    fastboot oem reboot_boot_dump_func
    fastboot oem hwdog certify begin
    fastboot oem get-product-model
    fastboot oem get-build-number
    fastboot oem get_hwnff_ver_func
    fastboot flashing unlock

### Print USB Mode (Charging only, MTP ... )

    cat /sys/devices/soc0/hw_platform
    
# Good Pages:
 
    https://wiki.gentoo.org/wiki/Android/adb
    http://tjtech.me/analyze-oem-unlocking-under-android.html

# adb-cheatsheet
