# General information/ FAQ/ Disclaimers:

## Why?
I had an old Galaxy SIII mini lying around in my drawer and didn't want to throw it away, since it's in good condition.
Even though this device is now over 10 years old, and we have phones more powerful than a dozen of SIII minis today in 2024, it is still useful.
... At least more useful than on a landfill! 😄
I wanted to breathe a second life into this antiquity.

### You can use old Android phones for example as:
* Raspberry Pi alternative
* As Nextcloud server
* For Octoprint
* As remote shutter for digital cameras
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

---

# Procedure
## Step 0: Precautions
- Back up any personal data. Old phones are a gem in retrieving old memories! :)
- Get a micro-SD-card + USB-reader for it.
- Charge the phone fully. The process will take longer than you think, the battery is aged and that will drain lots of juice.
My battery was in good condition, and still I had only 40% battery left when finishing.

## Step 1: Flashing TWRP
[TWRP](https://twrp.me/) replaces the pre-installed recovery mode from Samsung with this custom one. It allows you to install other distros (+ much more!), including LineageOS.
### Install [Heimdall](https://github.com/Benjamin-Dobell/Heimdall)
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
* Now, start Heimdall via `heimdall-frontend`. Don't use `sudo`. Many other guides say you should, but it will result in an error message.

  WIP, to be continued.
