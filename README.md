# SamsungDebloater
A debloater script for Samsung phones made by someone who hates it just as much as you do if not more. If you were like me and searched around for ages trying to find one complete list of packages to remove then I aim to provide that :D. With that said, everyone has different phones and carriers so if this doesn't uninstall all bloatware from your device and you find packages it left behind you can make a commit to this repo, just ensure that basic functions of the device (WiFi, mobile data, biometrics, receiving and sending both sms and phone calls, work profiles, navbar gestures) still work after removing the packages.

*tested on a Snapdragon Samsung Galaxy Note 20 Ultra 5G VZW*

# **⚠⚠⚠⚠⚠⚠⚠ WARNING ⚠⚠⚠⚠⚠⚠⚠**
# ***WHILE THE SCRIPT WORKS DOCUMENTATION IS NOT YET COMPLETE, BE WARNED THAT YOU'RE BETTER OFF WAITING A FEW DAYS FOR ME TO FINISH IT. PROCEED AT YOUR OWN RISK***
# **⚠⚠⚠⚠⚠⚠⚠ WARNING ⚠⚠⚠⚠⚠⚠⚠**

# Before you start
- READ THE ENTIRE README FIRST BEFORE DOING ANYTHING
- **If this breaks your device, you lose data, or anything else I am in no way responsible for anything and I have zero obligation to help you**
- This script will break any apps that rely on the Galaxy Store
- You will probaby get random background ANRs (for those of you that don't know, ANR's are those popups that say "**A**pp **N**ot **R**esponding")
- If you choose to nuke google services and you don't have MicroG or something similar a **lot** of apps will stop working
- Deleting knox packages isn't a good idea but I leave the option in there for anyone who is an advanced enough user to know what they're doing. If you don't know what you're signing up for then don't delete them.
- This script is deisgned to be run on a fresh factory reset before internet has been connected and without a SIM card installed (you can insert your SIM afterwards and connect to the internet afterwards.
- Chances are your device isn't the same model, same revision, same region, same carrier, and same software update version as mine. I obviously can't find, remove, and test packages that aren't on my devices and I can't ensure stability on Samsung's million and one different models.

# Understanding the script and what it does to your device
You should never run scripts without understanding them and looking at them, so here's a quick explanation:

ADB stands for Android Debug Bridge, it is a tool for developers that gives access to a variety of helpful tools without the need to root a device.

The command I prefer to use for removing packages uses the following syntax `pm uninstall --user 0 package.name.here`, the command needs to be run within an ADB shell.

Breaking down the command, pm stands for Package Manager so `pm uninstall` uses the package manager to uninstall someting, `--user 0` is telling your device to uninstall the app from the user with ID 0 on the device (0 is the default user, if you have multiple swap this for a 1, 2, etc.), `package.name.here` is the package you want to uninstall. 

Putting all of this together if you wanted to remove the Google Play Store for example, the command would be `pm uninstall --user 0 com.android.vending`.

# Getting the ready

## Backups
Finally we get into the meat of things. First, __**BACK UP YOUR PHONE!**__ I seriously can't stress how important this is- using ADB to remove system apps can easily break things and although I haven't had it happen to me personally I have heard of it soft-bricking devices and I don't doubt it, you can basically anything.

## Download Alternatives
Now that we have that out of the way, if you don't intend on using the Google Play Store go ahead and download an alternative to your PC, I personally recommend [Aurora Store](https://gitlab.com/AuroraOSS/AuroraStore/-/releases). If you also want to remove all Google Services and Frameworks then get an alternative to those, I recommend [MicroG](https://microg.org) but as far as I'm aware MicroG requires rooting/an unlocked bootloader so keep that in mind. Remember this script does remove the Galaxy Store and will break any apps that depend on it, I'm not aware of any alternatives and I'm not interested in using one anyways the [Aurora Store](https://gitlab.com/AuroraOSS/AuroraStore/-/releases) and [F-Droid](https://f-droid.org) are more than enough apps for me.

## Installing ADB
You've got your backup and your Google-subsitutes ready, next we need to install ADB. There are already dozens of tutorials online but I'll go over it quickly here. Download the [Android SDK Platform-Tools](https://developer.android.com/studio/releases/platform-tools), unzip it, the adb file is what you'll be using to interact with your device, feel free to set this up to be run from anywhere or you can just use ./adb to interact with it.

## A note about 2FA and Password Managers
It's pretty easy to forget about 2FA apps as a lot of them don't sync data. If you're using an app that doesn't automatically sync your data I strongly recommend either moving to one temporarily (ex. [Authy](https://authy.com), keep in mind you may have security concerns with this as Authy has ways of recovering accounts) or ensuring you have backup codes for all of your apps that use 2FA so you don't get locked out of anything.

The same principle goes for Password Managers, if yours doesn't sync data then you should find an alternative ([bitwarden](https://bitwarden.com) is a free and open source one that syncs data for free) or ensure you have a backup and know the password to unlock it.

## Preparing the phone itself
First off you'll want to remove your SIM card(s) and any expandable storage (MicroSD cards), this minimalizes chances of Android reinstalling garbage while we remove it or before we can fully remove it (some stuff comes in multiple packages that like to reinstall each other). This is a great time to double check that you have a proper backup done and if you don't *please go back and make one.*

# Debloating
Now that you've read through all the information above we can begin (if you haven't yet go do it or be warned you may need to factory reset and start over).

## **(RECOMMENDED)** Factory resetting the device
Yes I know factory resetting your phone can be annoying but stopping junk from being installed in the first place is what I've found to be the best and safest method- this also is the only real way I can concretely test stuff and avoid app incompatibilites. 

Now that you're ready with your SIM card removed and expandable storage out, go ahead and open the settings app, at the bottom hit the "About" section then click "Reset" and "Facotry reset my device". 

**DO NOT** reinsert your SIM card(s) or connect to WiFi. When the device reboots go through the setup process by hitting skip on everything you can. You can get around connecting to the internet in the setup process by skipping the "Insert your SIM card" page, hitting "Continue with WiFI", then hitting skip again on the WiFi page. Go ahead and opt out of all of the tracking and telemetry stuff, there's really no benefit to leaving any of it on anyways but if you want to be warned it might fight the script.

## Getting ready
Woooh! you've probably already gone farther than 90% of people who had the idea of debloating their phone. Next we want to transfer over your alternative apps for stuff like the Play Store if you're using alternatives. To do this plug your phone into your PC, open up the notification shade and change your USB mode to transfer files on your phone, then on your PC drag the apk files into the Download folder on your phone, back to the phone open the My Files app and install the apps by clicking on the APKs, it'll ask for permission you can go ahead and grant it- the My Files app gets removed with the other Samsung junk later.

On to the script! In it's current state it's honestly barely even a script, eventually I'll make a bash version that prompts the user about different things but for now we're doing stuff the old fashioned way. Open up debloat.txt and comment out packages you don't want to remove by adding a `#` at the start of the line. This isn't super difficult and you can go back and re-run the script later with less packages commented out if you change your down the road and want to remove something you previously commented out. You can also uncomment some of the stuff that's commented out by default but please read the comments I added each of these- typically stuff commented out by default breaks stuff in some way and I keep the default script setup in a way that I can use on all defaults, I tend to lean much more towards the get rid of everything side than you probably do.
