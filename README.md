# General information/ FAQ/ Disclaimers:

## Why?
I had an old Galaxy S III mini lying around in my drawer and didn't want to throw it away, since it's in good condition.  
Even though this device is now over 10 years old, and we have phones more powerful than a dozen of SIII minis today in 2024, it is still useful.  
... At least more useful than on a landfill! 😄

I wanted to breathe a second life into this antiquity.
While I tried to do this, I noticed, most guides are super scattered on many forums and outdated, and they provided conflicting packages.  
With this repo and guide, you can replicate my process quickly and don't have to do the same annoying work as I do.  

### You can use old Android phones for example as:
* Raspberry Pi alternative
* As Nextcloud server (see [here](https://github.com/jancborchardt/nextcloud-scripts/blob/master/nextcloud-on-android.md)
* For Octoprint [Octo4a, see here](https://github.com/feelfreelinux/octo4a)
* As remote shutter for digital cameras [This for example](https://f-droid.org/de/packages/com.thibaudperso.sonycamera/)
* Surveillance device at home
* ... and much more!

## Security + risks
### Using the stock OS on the phone is bad. Why?
* It never recieved any significant updates in this last decade, and therefore, there might be many (many!) potential security issues that never got fixed.
* The missing maintenence isn't the only issue. The stock OS is also bloated as hell, which increases the attack surface by a lot!
### Now, after installing the new ROM, I'm totally secure and can use it as my daily driver... right???
NO! The "new" OS is still old. Not over a decade old, but old. The last update was 2017, so even that was ~6 years ago.
The custom install should mainly be there to debloat the system and remove many proprietary system apps. The newer Android version is only the cherry on top.
Don't use this phone as daily driver with personal data on it.

### Risks
The procedure of flashing the custom Android distribution is risky. You might brick your device if not careful.
While the loss wouldn't be big, I am not responsible for any damage for anyone following this guide.
This guide only applies to the Samsung Galaxy SIII mini (GT-I8190).

---

# Procedure
## Step 0: Precautions
- Back up any personal data. Old phones are a gem in retrieving old memories! :)
- Get a micro-SD-card + USB-reader for it.
- Charge the phone fully. The process will take longer than you think, the battery is aged and that will drain lots of juice.
My battery was in good condition, and still I had only 40% battery left when finishing.

## Step 1: Flashing TWRP
[TWRP](https://twrp.me/) replaces the pre-installed recovery mode from Samsung with this custom one. It allows you to install other distros (+ much more!), including LineageOS.
  ### Install [Heimdall](https://github.com/Benjamin-Dobell/Heimdall):
  Heimdall is a FOSS-alternative to Odin, a firmware tool developed by Samsung, which is closed source and Windows only.
  Using this alternative gives you the good conscience that there won't be any weird hidden things, and it will be installable on Linux/ MacOS too.
  #### Installation on Linux:
  * Since I use Fedora Silverblue (image based system), I need to work in containers. Therefore, I used my Arch-container in Distrobox.
  If you use a traditional (mutable) distro, like Mint or Fedora Workstation, you can choose to install it on your host directly.
  If you use Mac or Windows, read the documentation of Heimdall in the link above.
  * Install the packages: You'll need both ´heimdall´ and ´android-tools´. They might have a different name on your distro, but basically, you want Heimdall and ADB. If there's an error with "qt5 missing"-blablabla, install that too.
  ### Flash
  * Enable USB-debugging. You can find it under developer options and it allows you to modify the phone via your PC.
  * Connect your device and check the connection via ´adb devices´ in your terminal. The phone should be listed with its' ID.
  * Plug in your phone and type ´adb reboot download´. This will put the phone into the download-mode.
    If the phone is off, you can also press `POWER + HOME + VOL-UP´ instead.
  If there's a warning message, accept it ![PXL_20240118_132235138](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/ce53826b-60aa-4018-ba5f-46f124a15115)
  ![PXL_20240118_132402265](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/a11c1488-36c4-41c6-a2e8-54082af59d29)
  * Now, start Heimdall via `heimdall-frontend`. Don't use `sudo`. Many other guides say you should, but it will result in an error message.
  * Now, go into the "Utilities" tab and click "Detect".
  ![Screenshot_20240118_151119](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/5bf32fae-3ab9-42c0-8403-d6481c4abc56)
  * Prepare the PIT by clicking "Save as..." and downloading it.
  * Next, *disconnect* the phone by pulling the cable. 
  Sounds weird, but if you don't, there will be error messages. 
  Thanks to [Pemill](https://github.com/pemill), see comment [here](https://github.com/Benjamin-Dobell/Heimdall/issues/364#issuecomment-277053119).
  * Prepare the flashing while the device isn't connected.
  For that, switch to the "Flash"-tab and
    * Select the .pit from before.
    * Click "Add" for adding a new layout. Defaults to MBR, which we don't want.
    * On the dropdown, select "Kernel2", which is the bootloader
    * And then, select the recovery file. This is the TWRP.img
    ![Screenshot_20240118_154427](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/0977f492-24ef-4d1c-b871-1a79b09b77f1)
    * Finally, you can start flashing. This will take about 30 seconds.

  If you go into the recovery menu next time, either by ´adb reboot recovery´ or ´POWER BUTTON + HOME + VOL-UP´, you will boot into the new recovery mode!
![PXL_20240119_075050279](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/f94e6e28-98d8-4de8-a2e5-6bb17b0caaea)


## Step 2: Flashing LineageOS
  ### Get the files
  Some of them are attached to this repo, some of them are too big for upload.
    Links:
        - LOS: [here](https://files.usp-forum.de/GalaxyS3MiniI8190/lineage20170609.zip)
        - OpenGApps Pico: [here](https://master.dl.sourceforge.net/project/opengapps/arm/20220215/open_gapps-arm-7.1-pico-20220215.zip?viasf=1)  
        
  Download and copy them to the SD-card. These are the ones I used, and they work.  
  Just copy the lineage.zip and GApps-pico.zip with the SD-adapter plugged in your PC.  

### Boot into recovery (TWRP)
  Do this either by `adb reboot recovery` (if the phone is on) or `POWER BUTTON + HOME + VOL-UP` if off.

### Install LineageOS and the GApps
  Tap "Install" and select the copied Lineage-ROM and GApps-Zip.
  Confirm and wait.
  Don't worry, the phone is old and wants to take its' time! :)
  That will take about ~10 minutes
  ![PXL_20240119_075050279](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/7070cb0e-2668-4c16-b2aa-b8990a72f693)
  ![PXL_20240119_075157143](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/cf442a90-fea1-467e-a5f9-446a66256ea0)
  ![PXL_20240119_075207791 MP](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/af9dba88-d2b9-49a7-9c35-dbf0f2f354e9)
  ![PXL_20240119_075912093](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/a947e8a7-2320-4b0f-8387-4e5caf6925dd)

### Wipe cache
  Every guide I watched said I should, so just do it.
  It will probably prevent some errors, idk...
  ![PXL_20240119_075105325](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/d6354f00-da09-4ee7-92b1-51df2b75958a)

### Reboot
  Almost done!
  ![PXL_20240119_075942777](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/3ef97054-849c-4caa-8f65-d9c7fad1f5f1)
  The LineageOS-logo should now appear.
  ![PXL_20240119_080007340](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/c99ec4b9-986a-4aa0-aa6e-2017621d745e)
  This will take *a long time*, so don't worry.
  Your device probably isn't bricked. The first boot will just take ~10 - 15 minutes. 
  (If it takes significantly longer, you're fucked. Sorry.)

  By now, it should be booted completely.
  ![PXL_20240119_080927618 MP](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/c535ede4-148d-4077-ac8e-d7579a0435ae)
**Aaaaand, you're done!**
  Now, just set up the phone the first time, just like you would another device.
![PXL_20240119_081613396](https://github.com/gluckgluckwasserbauch/galaxy-s3mini-secondlife/assets/99470494/f2b145fd-3980-48ac-b36b-8fb8f2a82711)

---

# I hope this guide did help you!

---

## Credits/ sources/ further ressources:
- https://xdaforums.com/t/rom-7-1-2-lineageos-14-1-for-gt-i8190-gt-i9070-2017-06-09.3520752/
- https://www.usp-forum.de/threads/samsung-galaxy-s3-mini-i8190-cyanogenmod-12-1-android-5-1-1-by-novafusion.122657/
- https://www.usp-forum.de/threads/samsung-galaxy-s3-mini-i8190-lineage-14-1-android-7-1-2-installieren.136119/
- https://opengapps.org/
- https://xdaforums.com/t/recovery-golden-twrp-3-x.2748327/
- http://andi34.github.io/recoveries_golden.html
- https://eu.dl.twrp.me/golden/twrp-2.6.3.0-golden.tar.html (outdated, didn't work!)

