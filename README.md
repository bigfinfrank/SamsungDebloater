# **⚠⚠⚠⚠⚠⚠⚠ WARNING ⚠⚠⚠⚠⚠⚠⚠**
# ***After going through all the trouble of working on my own script, I found someone else's AIO script that accomplishes more. This really removes any point in me maintaining this script so instead I'll link the one that I found here, it seems to be much more well-maintained as well. It's hosted on [GitLab](https://gitlab.com/W1nst0n/universal-android-debloater) but I found [this mirror on GitHub](https://github.com/0x192/Universal-Android-Debloater).***
# **⚠⚠⚠⚠⚠⚠⚠ WARNING ⚠⚠⚠⚠⚠⚠⚠**


# Samsung Debloater
A debloater script for Samsung phones made by someone who hates the bloat just as much as you do if not more. If you were like me and searched around for ages trying to find one complete list of packages to remove then I aim to provide that :D. With that said, everyone has different phones and carriers so if this doesn't uninstall all bloatware from your device and you find packages it left behind you can make a commit to this repo, just ensure that basic functions of the device (WiFi, mobile data, biometrics, receiving and sending both sms and phone calls, work profiles, navbar gestures, etc.) still work after removing the packages.

*Tested on a Snapdragon Samsung Galaxy Note 20 Ultra 5G VZW bought in the US intially tested on System Update 7 then tested with each update through System Update 10.*

*Version 1.3.4 of the script was additionally tested on a Samsung Galaxy A11 personally by me. I don't know specifications beyond the device model as it was a friend's device not mine.*

*If you're willing to factory reset your device and follow all of the instructions in the README carefully, feel free to make a [PR](https://github.com/bigfinfrank/SamsungDebloater/pulls) adding the same type of info I put for my Note 20 Ultra.*

# Before you start
- SERIOUSLY READ THE ENTIRE README FIRST BEFORE DOING ANYTHING
- **If this breaks your device, you lose data, or anything else I am in no way responsible for anything and I have zero obligation to help you**
- This script will break any apps that rely on the Galaxy Store
- You will probably get random background ANRs (for those of you that don't know, ANR's are those popups that say "**A**pp **N**ot **R**esponding")
- If you choose to nuke google services and you don't have MicroG or something similar a **lot** of apps will stop working (You can check out [Plexus](https://plexus.techlore.tech), a crowdsourced resource to check app compatibility for de-googled devices)
- Deleting knox packages isn't a good idea but I leave the option in there for anyone who is an advanced enough user to know what they're doing. If you don't know what you're signing up for then don't delete them, I haven't even tried to out of fear that it'll brick my Note 20 Ultra 512GB [which isn't exactly cheap](https://www.google.com/search?q=galaxy+note+20+ultra+512gb+launch+price).
- This script is designed to be run on a fresh factory reset before the internet has been connected and without a SIM card installed (you can insert your SIM and connect to the internet afterwards).
- Chances are your device isn't the same model, same revision, same region, same carrier, and same software update version as mine. I obviously can't find/remove/test packages that aren't on my devices and I can't ensure stability on Samsung's [million and one](https://en.wikipedia.org/wiki/Samsung_Galaxy#Release_history) different models.

# Understanding the script and what it does to your device
You should never run scripts without understanding them and looking at them, so here's a quick explanation:

ADB stands for Android Debug Bridge, it is a tool for developers that gives access to a variety of helpful tools without the need to root a device.

The command I prefer to use for removing packages uses the following syntax `pm uninstall --user 0 package.name.here`, the command needs to be run within an ADB shell.

Breaking down the command, pm stands for Package Manager so `pm uninstall` uses the package manager to uninstall something, `--user 0` is telling your device to uninstall the app from the user with ID 0 on the device (0 is the default user, if for whatever uncommon reason you have multiple then swap the 0 for a 1, 2, etc.), `package.name.here` is the package you want to uninstall. 

Putting all of this together if you wanted to remove the Google Play Store for example, the command would be `pm uninstall --user 0 com.android.vending`, do note how the package name can differ from the app's name.

# Getting ready

## Backups
Finally we get into the meat of things. First, __**BACKUP YOUR PHONE!**__ I seriously can't stress how important this is- using ADB to remove system apps can easily break things and although I haven't had it happen to me personally I have heard of it soft-bricking devices and I don't doubt it, you can basically anything.

## Download Alternatives
Now that we have that out of the way, if you don't intend on using the Google Play Store go ahead and download an alternative to your PC, I personally recommend [Aurora Store](https://gitlab.com/AuroraOSS/AuroraStore/-/releases). If you also want to remove all Google Services and Frameworks then get an alternative to those, I recommend [MicroG](https://microg.org) but as far as I'm aware MicroG requires rooting/an unlocked bootloader so keep that in mind. Remember this script does remove the Galaxy Store and will break any apps that depend on it, I'm not aware of any alternatives and I'm not interested in using one anyways the [Aurora Store](https://gitlab.com/AuroraOSS/AuroraStore/-/releases) and [F-Droid](https://f-droid.org) are more than enough apps for me.

## Installing ADB
You've got your backup and your Google-substitutes ready, next we need to install ADB. There are already dozens of tutorials online but I'll go over it quickly here. Download the [Android SDK Platform-Tools](https://developer.android.com/studio/releases/platform-tools), unzip it, the adb file is what you'll be using to interact with your device, feel free to set this up to be run from anywhere or you can just use ./adb.exe to interact with it.

## A note about 2FA and Password Managers
It's pretty easy to forget about 2FA apps as a lot of them don't sync data automatically. If you're using an app that doesn't automatically sync your data I strongly recommend either moving to one temporarily (ex. [Authy](https://authy.com), keep in mind you may have security concerns with this as Authy has ways of recovering accounts which is questionable in my opinion) or ensuring you have backup codes for all of your apps that use 2FA so you don't get locked out of anything.

The same principle goes for Password Managers, if yours doesn't sync data then you should find an alternative ([bitwarden](https://bitwarden.com) is a free and open source one that syncs your data for free) or ensure you have a backup and know the password to unlock it.

## Preparing the phone itself
First off you'll want to remove your SIM card(s) and any expandable storage (MicroSD cards), this minimizes chances of Android reinstalling garbage while we remove it or before we can fully remove it (some stuff comes in multiple packages that like to reinstall each other). This is a great time to double check that you have a proper backup done and if you don't *please go back and make one.*

# Debloating
Now that you've read through all the information above we can begin (if you haven't yet go do it or be warned you may need to factory reset and start over, or worse not even be able to factory reset your device).

## **(RECOMMENDED)** Factory resetting the device
Yes I know factory resetting your phone can be annoying but stopping junk from being installed in the first place is what I've found to be the best and safest method- this also is the only real way I can concretely test stuff in a reproducible way.

Now that you're ready with your SIM card removed and expandable storage out, go ahead and open the settings app, at the bottom hit the "About" section then click "Reset" and "Factory reset my device". 

**DO NOT** reinsert your SIM card(s) or connect to WiFi. When the device reboots go through the setup process by hitting skip on everything you can. You can get around connecting to the internet in the setup process by skipping the "Insert your SIM card" page, hitting "Continue with WiFI", then hitting skip again on the WiFi page. Go ahead and opt out of all of the tracking and telemetry stuff, there's really no benefit to leaving any of it on anyways but if you want to be warned it might fight the script.

## Customizing the script
Wooo! you've probably already gone farther than 90% of people who had the idea of debloating their phone. Next we want to transfer over your alternative apps for stuff like the Play Store if you're using alternatives. To do this plug your phone into your PC, open up the notification shade and change your USB mode to transfer files on your phone, then on your PC drag the apk files into the Download folder on your phone, back to the phone open the My Files app and install the apps by clicking on the APKs, it'll ask for permission you can go ahead and grant it- the My Files app gets removed with the other Samsung junk later.

On to the script! In its current state it's honestly barely even a script, eventually I'll make bash and ps1 versions that prompt the user about different things but for now we're doing stuff the old fashioned way (copy and paste!). Open up [debloat.txt](https://github.com/bigfinfrank/SamsungDebloater/blob/main/debloat.txt) and comment out any packages you don't want to remove by adding a `#` at the start of the line. This isn't super difficult and you can go back and re-run the script later with less packages commented out if you change your mind down the road and want to remove something you previously commented out. You can also uncomment some of the stuff that's commented out by default but please read the comments I added by each of these- typically stuff commented out by default breaks stuff in some way and I keep the default script setup in a way that I can use on all defaults, I tend to lean much more towards the get rid of everything side than you probably do anyways so keep that in mind.

## Connecting with ADB
Now, open up your Terminal of choice- I prefer Windows so I'll be using the latest version of [PowerShell](https://aka.ms/powershell-release?tag=stable) through [Windows Terminal](https://github.com/microsoft/terminal/releases) but the process should be virtually identical on your system- if you run into trouble then [Google your issue](https://google.com) and if you're feeling generous make a [PR](https://github.com/bigfinfrank/SamsungDebloater/pulls) with the solution you find or make a issue if Google wasn't helpful. 

From your terminal, navigate to wherever you have your `platform-tools` folder with the `cd` command. (If you moved platform-tools to your Documents folder for example, the command would be `cd ~/Documents/platform-tools`).

Now on your device we'll need to enable ADB debugging (sometimes called USB debugging). To do this, go to your phone's settings app, scroll down to about, find Build Number (for me it's under Software Information), and click it until it tells you that developer mode has been turned on, if you added a password during your phone's setup you'll be prompted to input it when enabling developer mode. Now go back to the main settings page and at the very bottom of the main page below About phone you should see Developer Options, open up that menu and look for `USB debugging` or `ADB debugging` (for me the setting is at the top of the Debugging section visible when I first open the Developer Options menu) and turn it on. Now to verify that ADB debugging is turned on, in your Terminal run `./adb.exe devices`, you should get a response that includes your device's serial number with the text `device` to the right of it, you will need to confirm that you want to use ADB debugging with your computer on your phone before your device will appear and you might need to disconnect and reocnnect the USB cable as well.


## Execution
The execution itself is actually pretty simple, run `./adb.exe shell` in your terminal while in the platform-tools folder, this will put you into the ADB Shell. From here, copy paste all of the text inside of [debloat.txt](https://github.com/bigfinfrank/SamsungDebloater/blob/main/debloat.txt) into your ADB Shell and let the script do its magic, it will probably take a while and depending on both how much of this software your phone comes with and how fast your device is it could take anywhere from 30 seconds to a few minutes, just wait until you see the script version number and warning that's at the end of the script and your terminal has calmed down- for me on PowerShell 7.1.3 via Windows Terminal the text in the ADB Shell gets really buggy (visually showing some commands being cut in half and merging comments onto the incorrect lines, etc.)- as far as I have been able to tell the commands are still executed properly and this is just a visual issue, I have no idea if this issue is exclusive to Windows/WT or if its caused by the ADB Shell itself.

## Finalization
Now restart your phone and do the part that's either the most fun or the most boring depending on who you are (I'm in the former party myself :D), setting up your phone! It'll be like it's brand new and it may even run a bit faster than new with all the pointless background processes removed. After you've gone through and gotten all of your stuff set up the way you want it with your SIM card installed and your device having been connected to WiFi/the internet for a while I'd recommend doing a restart, running the script one last time, then doing a final restart to make sure everything that's going to stick has applied. This is mainly to combat garbage reinstallation which happened every time I connected to the internet for the first time but as far as I can tell everything that gets reinstalled when you first connect to the internet goes away for good once you remove it for a second time.

## One last thing to keep in mind
From my experience this isn't as big of an issue as you be used to if you use Windows for example, but it is possible for Software updates to reinstall stuff you've removed. This is especially true when a Software update includes changes to one of the removed apps (which is relatively common). This simply means that after a software update you should re-run the script, personally I haven't bothered disconnecting from the internet or factory resetting after software updates as I haven't found it necessary.

# To Do
- Make proper PowerShell and Bash scripts, instead of big txt files with commands *if this ever happens it probably won't happen soon so don't sit around waiting lol*
- Add names for each app to the script
- Make an undo script, it's possible even with the `uninstall` adb command that I like to use :)
- Buy a f\*\*king Pixel and install CalyxOS god Samsung is awful
