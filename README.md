# SamsungDebloater
A debloater script for Samsung phones

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

# Preparing to run the script
Backup your phone. Backup your phone. Backup your phone.
I can't stress enough how important this is as your device probably isn't identical to mine and you can definitely break things uninstalling the wrong packages.

