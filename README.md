# Lenovo Yoga 530-14IKB Hackintosh - OpenCore

<img align="right" src="https://p2-ofp.static.pub/fes/cms/2022/09/23/2hlnrsq97hxle4024baiqqu71epwks693597.png" alt="PC image" width="425">

[![macOS](https://img.shields.io/badge/macOS-Sequoia-orange.svg?logo=apple)](https://developer.apple.com/documentation/macos-release-notes)
[![macOS](https://img.shields.io/badge/macOS-Tahoe-blue.svg?logo=apple)](https://developer.apple.com/documentation/macos-release-notes)
[![OpenCore](https://img.shields.io/badge/OpenCore-1.0.7-brightgreen.svg)](https://github.com/acidanthera/OpenCorePkg)
[![Model](https://img.shields.io/badge/Model-14Ikb-9cf)](https://psref.lenovo.com/syspool/Sys/PDF/Yoga/Yoga_530_14IKB/Yoga_530_14IKB_Spec.pdf)
[![BIOS](https://img.shields.io/badge/BIOS-7QCN46WW-red)](https://pcsupport.lenovo.com/us/en/products/laptops-and-netbooks/yoga-series/yoga-530-14ikb/downloads/driver-list/component?name=BIOS%2FUEFI&id=5AC6A815-321D-440E-8833-B07A93E0428C)

**DISCLAIMER:**  
This OpenCore EFI works well on my "INTEL" Lenovo 530 Yoga. 
As you embark on your Hackintosh journey you are encouraged to **READ** the entire README and [Dortania](https://dortania.github.io/getting-started/) guides before you start to get an understanding of the install process. It will save many a message instructing you to read the manual. 

ℹ️ Take also a look to the "Images" folder above!

You can also find a wealth of knowledge on [Reddit](https://www.reddit.com/r/hackintosh/), [TonyMacX86](https://www.tonymacx86.com) or [Google](https://www.google.com).

## 👋 Introduction

<details>  
<summary><strong>📖 Getting started</strong></summary>
</br>

**The Bootloader:**

- [Why OpenCore](https://dortania.github.io/OpenCore-Install-Guide/why-oc.html)
- Dortania's [website](https://dortania.github.io)

**Recommended tools:**

- Plist editor [ProperTree](https://github.com/corpnewt/ProperTree) or [OpenCore Configurator](https://mackie100projects.altervista.org/download-opencore-configurator/)
- Handy-dandy ESP mounting script [MountEFI](https://github.com/corpnewt/MountEFI) if you don't want to use OpenCore Configurator and manually copy the EFI
- Cross-platform GUI management tools for OpenCore [OCAT](https://github.com/ic005k/OCAuxiliaryTools) if you are on WINDOWS
- Py script that uses acidanthera's macserial to generate SMBIOS [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS)
- The Swiss army knife of vanilla Hackintoshing [Hackintool](https://github.com/benbaker76/Hackintool)

**Resources**

- [OpenCore](https://github.com/acidanthera/OpenCorePkg)
- The classic OpenCore Legacy Patcher for SEQUOIA: (https://github.com/dortania/OpenCore-Legacy-Patcher/releases/tag/2.4.1)
- OCLP-PLUS: a modded version ONLY for macOS TAHOE, credits to "YBronst": (https://github.com/YBronst/OCLP-Plus/releases/tag/3.2.2)

</details>

<details> 
<summary><strong>💻 My Hardware</strong></summary>
</br>

| Category  | Component                                            | Note                                                         |
| --------- | ---------------------------------------------------- | ------------------------------------------------------------ |
| Type      | 81EK                                                 |                                                              |
| CPU       | Intel(R) Core(TM) i5-8250U CPU @ 1.60GHz (Turbo up to 3.40GHz)            |                                                              |
| GPU 0     | Intel UHD Graphics 620 (Integrated)                             |                                                              |
| GPU 1     | Nvidia GeForce MX130 (Discrete)                      | macOS doesn't support Optimus technology, so i disabled it with SSDT in order to save power      |
| SSD       | Intel SSD 760p 256GB — M.2 2280 NVMe PCIe 3.0 x4     | ✅ Compatible with macOS ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎‼️ If you plan to buy a new SSD, read this guide first [Anti-Hackintosh Buyers Guide - Storage](https://dortania.github.io/Anti-Hackintosh-Buyers-Guide/Storage.html)     |
| Screen    | 14" FHD 1920x1080                                    | Multi touch and pen* support working (with "-vi2c-force-polling" in boot-args) |
| Memory    | 16GB DDR4 2400Mhz                                    |                                                              |
| Camera    | 720p Camera                                          |                                                              |
| Audio     | Realtek® ALC236                                      | I suggest to use layout ID `13`. It works very well.         |
| Touchpad  | Synaptics I2C Touchpad                               | Works with multi-gestures.                                   |
| Wifi & BT | Intel Dual Band Wireless-AC 3165 + Bluetooth         | Use AirportItlwm for your macOS version and enjoy native Wi-Fi control. Bluetooth already works with my modified kexts for Tahoe and controller info in NVRAM, so you don't have to do anything  |
| Input     | 🕹️ Synaptics I2C Touchpad ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎  ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎  ‎ ‎  ‎ ‎ ‎ ‎ ‎  ‎ ‎ ‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎  ‎‎‎‎‎‎ ‎‎‎‎‎‎  ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎‎‎‎‎‎‎‎‎‎‎‎‎⌨️ Cypress Integrated PS/2 Keyboard ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎  ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎👆 Touchscreen ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎  ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎  ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎ ‎  ‎ ‎ ‎  ‎ ‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎ ‎‎‎‎‎‎🖊️‎‎‎ Wacom Active Pen Driver | I'm using [YogaSMC](https://github.com/zhen-zen/YogaSMC) for media keys. The kext is in the folder but **you must install the YogaSMC app separately.** |

</details>

<details>
<summary><strong>📦 Main software</strong></summary>

| Component     | Version |
| ------------- | ------- |
| macOS [Sequoia](https://www.apple.com/newsroom/2024/06/macos-sequoia-takes-productivity-and-intelligence-on-mac-to-new-heights/) / [Tahoe](https://www.apple.com/newsroom/2025/06/macos-tahoe-26-makes-the-mac-more-capable-productive-and-intelligent-than-ever/)  | 15.7.9 / 26.3.1  |
| OpenCore      | v1.0.7  |

</details>

## 📖 Installation

<details>  
<summary><strong>💿 How to install macOS</strong></summary>
</br>

1. [Create an installation media](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/#making-the-installer)
1. Download the [latest EFI folder](https://github.com/marione-3093/Yoga-530-14Ikb-Hackintosh/archive/refs/heads/main.zip) and copy it into the ESP partiton
1. Change your BIOS settings according to the table below
1. Boot from the USB installer (press `F12` to choose boot volume) and [start the installation process](https://dortania.github.io/OpenCore-Install-Guide/installation/installation-process.html#booting-the-opencore-usb)

### BIOS Configuration (F2 after pressing power button)

| Menu     |                                 | Setting     |
| -------- | ------------------------------- | ----------- |
| Config   | Wireless LAN                    | `✅ Enabled`    |
|          | Intel Virtual Technology        | `✅ Enabled`    |
|          | Intel(R) Hyper-Threading Technology [(about)](https://www.intel.com/content/www/us/en/gaming/resources/hyper-threading.html)          | `✅ Enabled`    |
|          | BIOS Back Flash                 | `❌ Disabled`    |
|          | HotKey Mode                     | `✅ Enabled`     |
|          | Always On USB                   | `✅ Enabled`    |
|          | DPTF                            | `✅ Enabled`    |
| Security | Intel Platform Trust Technology           | `✅ Enabled`    |
|          | Intel SGX						 | `❌ Disabled`    |
|          | Secure Boot              		 | `❌ Disabled`    |
| Boot	   | Boot Mode                       | `UEFI` |
|          | Fast Boot                       | `❌ Disabled`    |
|          | USB Boot                        | `✅ Enabled`     |
|          | PXE Boot to LAN                 | `❌ Disabled`     |
| Exit	   | OS optimized defaults           | `✅ Enabled` |
</details>

<details>  
<summary><strong> Enable Apple Services</strong></summary>
</br>

Config to allow you to use Apple Services (such as iMessage)

> **🗒️ Note:**
>
> If you (still) can't login to iMessage you may need to contact Apple Support to unblacklist your AppleID (You can try opening the Message app from terminal to check the log to see if you're getting a Customer Code error, which is an indication that your AppleID got blacklisted. [See more info here](https://dortania.github.io/OpenCore-Post-Install/universal/iservices.html#customer-code-error))

1. Download (or clone) [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) and run it in terminal
2. Type `3` to generate SMBIOS, then press <kbd>Enter</kbd>
3. Type `MacBookPro15,2`, then press <kbd>Enter</kbd>
4. Open `EFI/Config.plist` (I highly recommend using [ProperTree](https://github.com/corpnewt/ProperTree)) and navigate to `PlatformInfo -> Generic`
5. Add one of the script's result to `MLB`, `SystemSerialNumber`, and `SystemUUID`
6. Replace `ROM` with your MAC Address (`System Preferences -> Network -> Ethernet -> Advanced -> Hardware -> MAC Address`, then remove all the colons `:`). Or you can also try using a real Apple MAC Address
7. Save and Reboot
8. Check the Serial Number validity. Repeat step 5 and choose different result (or generate new set of SMBIOS) until you find invalid Serial Number
</details>

## 🧰 Post-install (TO-DO)

<details>  
<summary><strong>🔊 Audio Setup</strong></summary>

The Ideapad 530 Yoga has ALC236 for audio which requires the boot-arg **or** device property below that I've already included in the EFI. You can only use the boot-args to initially setup your config.plist file as suggested in the guide or simply add the device property. Everything should work, built-in microphone, speakers, headphone jack and microphone. **In macOS Tahoe, you have to rollback AppleHDA.kext to make the audio work** (https://github.com/Mirone/MyKextInstaller/releases/download/1.0/AppleHDA.zip) with MyKextInstaller (https://github.com/Mirone/MyKextInstaller/releases/download/1.0/MyKextInstaller.zip)

NVRAM:

| Key       | Value    |
| --------- | -------- |
| boot-args | alcid=13 |

DeviceProperties

| Key                        | Type       | Value        |
| -------------------------- | ---------- | ------------ |
| PciRoot(0x0)/Pci(0x1F,0x3) | Dictionary |              |
| layout-id                  | Data       | **0d000000** |

</details>

<details>  
<summary><strong>🛜 Enable Intel WLAN card</strong></summary>
</br>

Although the Intel AC-3165 Card is compatible with both kexts (use either one or the other), there are Pros and Cons to both of them (check the [**FAQs**](https://openintelwireless.github.io/itlwm/FAQ.html#features) for other differences):

> [!IMPORTANT]
> **WiFi Kext Compatibility**: The included `AirportItlwm.kext` is specifically for **macOS Sequoia and Tahoe**.  
> If you plan to install **macOS Sonoma**, you **MUST** replace this kext with the version compiled for Sonoma. Using the wrong version will result in boot failures or non-functional WiFi.

- **AirportItlwm**: (used in macOS Sonoma)
	- **Pro**: Can be used during macOS Setup/Recovery which is not possible with `itlwm.kext`
	- **Pro**: Supports Location Services and "Find My Mac"
 	- **Pro**: Connects faster to Wi-Fi Hotspots than `itlwm.kext`
	- **Con**: Doesn't perform as well as `itlwm.kext`
	- **Con**: Can't connect to hidden WiFi Networks
	- **Con**: Requires the correct kext per macOS version, so running multiple version of macOS requires multiple versions of this kext controlled via `MinKernel` and `MaxKernel` settings

- **itlwm.kext** (used in Sequoia)
	- **Pro**: `itlwm.kext` works across _multiple_ versions of macOS
	- **Pro**: Loading webpages feels a lot quicker than with `AirportItlwm` 
	- **Pro**: Can connect to hidden WiFi Networks
 	- **Pro**: Does work with iMessage and FaceTime 	
	- **Con**: Requires [**HeliPort**](https://github.com/diepeterpan/HeliPort/releases) app to connect to Wi-Fi hotspots, so it can't be used during macOS Setup/Recovery
	- **Con**: Doesn't support Location Services

- Pre-compiled WiFi kexts for other versions of macOS can be found in the [Additional Files](https://github.com/OpenIntelWireless/itlwm/releases) section! You will need them if you want to run other macOS versions than Sonoma or Sequoia!

> **🗒️Note:**
> 
> My config uses `AirportItlwm.kext` by default since it allows accessing the internet during macOS installation (unlike `itlwm.kext` which requires an additional app to do so). Currently, AirportItlwm kexts for macOS Sequoia is included but you must patch following this tutorial: (https://youtu.be/C_wa3tQzWt8?si=QljfTeTbMhlmHEn6). If you want to use itlwm, disable AirportItlwm (all variants) and enable itlwm in the config.plist instead. Next, download the Heliport app, run it and add it to "Login Items" (in System Settings) so that it starts automatically with macOS.

</details>

<details>  
<summary><strong>🧠 CPUFriend power management</strong></summary>
<br>

Generate `CPUFriendDataProvider` or `ssdt_data.aml` (choose one) for your machine [here](https://github.com/acidanthera/CPUFriend) or use my stable configuration provided. My files are set for power conservation over performance. Highly recommended that you use power management.

</details>

<details> 
<summary><strong>🔌 USB Ports</strong></summary>

I mapped and enabled all the USB ports using (https://github.com/usbtoolbox/tool)

</details> 

## 🛠️ Other tweaks (optional)

<details>  
<summary><strong>🖥️ Enable HiDPI</strong></summary>
</br>

1. [Disable SIP](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/troubleshooting.html#disabling-sip)
2. Run the following script in Terminal
   ```bash
   bash -c "$(curl -fsSL https://raw.githubusercontent.com/xzhih/one-key-hidpi/master/hidpi.sh)"
   ```
3. Follow the instructions, then reboot
4. Re-enable SIP (if desired)

Or try an [alternative method](https://github.com/bbhardin/A-Guide-to-MacOS-Scaled-Resolutions)
</details>

<details>  
<summary><strong>🖌️ Personalize "About my Mac" section</strong></summary>
</br>

1. [Disable SIP](https://dortania.github.io/OpenCore-Install-Guide/troubleshooting/troubleshooting.html#disabling-sip)
2. Follow this guide: (https://www.reddit.com/r/hackintosh/comments/1iubdhk/guide_to_change_about_this_mac_name_and_photo_on/)

</details>

<details>  
<summary><strong>⏯️ Enable multimedia keys, fan & LEDs control </strong></summary>
</br>

- Download [**YogaSMC-App**](https://github.com/zhen-zen/YogaSMC/files/14324664/Builds.zip) and mount it. This is a custom build which fixes the "Failed to open Preferences" [issue](https://github.com/zhen-zen/YogaSMC/issues/189) in Ventura and newer  
	- Double-click the YogaSMC **prefPane** to install it
	- Drag the `YogaSMC` app into the "Programs" folder and run it
	- Click on the icon (`⌥`) in the menu bar and select "Start at Login"
	- Now you can control performance profiles, fan speed and other settings
</details>

<details>  
<summary><strong>📸 Use STAMP key as Screenshot shortcut (like on WINDOWS)</strong></summary>
</br>

Super useful shortcut that I wish I had it on my previous MBP. Default is `⌘⇧5`.

1. Open SystemPreferences.app
2. Go under `Keyboard > Shortcuts > Screenshots`
3. Click on `Screenshot and recording options` field
4. Press `Stamp` on your keyboard (it should came out as `F13`) and click done

</details>

<details>  
<summary><strong>🏎️ Faster macOS dock animation</strong></summary>
</br>

This enables auto-hide and speeds up the animation

1. Run the following script in Terminal
   ```bash
   defaults write com.apple.dock autohide-delay -float 0; defaults write com.apple.dock autohide-time-modifier -float 0.5; killall Dock
   ```
   </details>

<details>  
<summary><strong>🕰️ Fix Windows Time Sync</strong></summary>
</br>

`RealTimeIsUniversal` registry key still works in Windows 8, 10, and 11! Just tested it by myself. The instructions to use this method are explained lot of times everywhere, for example in this answer.

I will replicate the answer here:

`Win+R`, `regedit`, `Enter`.

Navigate to the key:

`HKEY_LOCAL_MACHINE\SYSTEM\CurrentControlSet\Control\TimeZoneInformation`.
Create new `DWORD (32-bit) Value`, name it `RealTimeIsUniversal`. Set its value to `1`.

After this is done, just reboot your machine. After it is up and running again, let Windows set time automatically (click on the current time in tray, `Date and Time` `Settings` > `Set Time Automatically`), this time it will not mess with it.
</details>

<details>  
<summary><strong>⚙️ Boot process tweaks</strong></summary>
</br>

| Menu |       |            | Setting    | What does it do?     |
| :--- | :---- | :--------- | :--------- | :------------------- |
| Misc | Boot  | ShowPicker | `False`    | Skip bootloader page |
| UEFI | Audio | PlayChime  | `Enabled`  | Play chime on boot   |

</details>

<details>  
<summary><strong>🌙 Setup hibernation and sleep</strong></summary>
</br>

[Script](https://www.tonymacx86.com/threads/release-sleeponlowbattery-solb.264785) that performs auto sleep/hibernate at low battery. 

**⚠️ If you have problems with sleep, follow this [guide](https://dortania.github.io/OpenCore-Post-Install/universal/sleep.html#preparations) ⚠️**

1. Open terminal
2. Enter commands below one by one

   Settings for AC:

   ```
   sudo pmset -c standby 1
   sudo pmset -c hibernatemode 0
   ```

   Setting for battery:

   ```
   sudo pmset -b standby 1
   sudo pmset -b standbydelayhigh 900
   sudo pmset -b standbydelaylow 60
   sudo pmset -b hibernatemode 25
   sudo pmset -b highstandbythreshold 70
   ```

   Settings for all:

   ```
   sudo pmset -a acwake 0
   sudo pmset -a lidwake 1
   sudo pmset -a powernap 0
   ```

To restore default system settings run

```
sudo pmset restoredefaults
```
</details> 

<details> 
<summary><strong>🚹 Grant/remove accessibility permissions to any app</strong></summary>

tccutil with extended capabilities allowing you to grant/remove accessibility permissions to any app.

I never recommend manually modifying any system database because if a mistake is made you risk boot-looping your computer. This is why this tool is using the undocumented TCC.framework to make changes just like macOS does internally. 

Requires SIP and AMFI to be disabled.

Currently can only add one or all (not recommended) services at a time. Using `reset All` is fine.

```
tccplus [add/reset] SERVICE [BUNDLE_ID]
Services: 
 - All 
 - Accessibility 
 - AddressBook 
 - AppleEvents 
 - Calendar 
 - Camera 
 - ContactsFull 
 - ContactsLimited 
 - DeveloperTool 
 - Facebook 
 - LinkedIn 
 - ListenEvent 
 - Liverpool 
 - Location 
 - MediaLibrary 
 - Microphone 
 - Motion 
 - Photos 
 - PhotosAdd 
 - PostEvent 
 - Reminders 
 - ScreenCapture 
 - ShareKit 
 - SinaWeibo 
 - Siri 
 - SpeechRecognition 
 - SystemPolicyAllFiles 
 - SystemPolicyDesktopFolder 
 - SystemPolicyDeveloperFiles 
 - SystemPolicyDocumentsFolder 
 - SystemPolicyDownloadsFolder 
 - SystemPolicyNetworkVolumes 
 - SystemPolicyRemovableVolumes 
 - SystemPolicySysAdminFiles 
 - TencentWeibo 
 - Twitter 
 - Ubiquity 
 - Willow
 ```
Usage Example:
Get application bundle ID:

`grep 'BundleIdent' -A 1 /Applications/<APPLICATION NAME>/Contents/Info.plist`

Pass result to `tccplus`
```bash
user@iMac ~ % grep 'BundleIdent' -A 1 /Applications/Discord.app/Contents/Info.plist
    <key>CFBundleIdentifier</key>
    <string>com.hnc.Discord</string>
user@iMacc ~ % grep 'BundleIdent' -A 1 /Applications/zoom.us.app/Contents/Info.plist
    <key>CFBundleIdentifier</key>
    <string>us.zoom.xos</string>
user@iMac ~ % ./tccplus add Microphone com.hnc.Discord
Successfully added Microphone approval status for com.hnc.Discord
```

</details> 

<details>  
<summary><strong>⚡️ Advanced energy management</strong></summary>

😃 You can copy my preset and paste them into Terminal (NOTE: it will ask for your admin user password because of "sudo"):

```bash

sudo pmset -a gpuswitch 0

sudo pmset -a standby 0

sudo pmset -a autopoweroff 0

sudo pmset -a powernap 0

sudo pmset -a proximitywake 0

sudo pmset -a tcpkeepalive 0

sudo pmset -a ttyskeepawake 0

sudo pmset -a womp 0

sudo pmset -a networkoversleep 0

```

or just choose yourself what to do: 

`acwake`: wake the machine when power source (AC/battery) is changed (value = 0/1)

`lidwake`: wake the machine when the laptop lid (or clamshell) is opened (value = 0/1)

`powernap`: enable/disable Power Nap on supported machines (value = 0/1)

`standbydelayhigh` and `standbydelaylow` specify the delay, in seconds,
before writing the hibernation image to disk and powering off memory for Standby.
standbydelayhigh is used when the remaining battery capacity is above `highstandbythreshold`(has a default value of 50 percent),
and standbydelaylow is used when the remaining battery capacity is below highstandbythreshold.

`hibernatemode` supports values of 0, 3, or 25. To disable hibernation, set hibernatemode to 0.  
`hibernatemode` = 0 by default on desktops. The system will not back memory up to persistent storage. The system must wake from the contents of memory; the system will lose context on power loss.  
`hibernatemode` = 3 by default on portables. The system will store a copy of memory to persistent storage (the disk), and will power memory during sleep. The system will wake from memory, unless a power loss forces it to restore from hibernate image.  
`hibernatemode` = 25 is only settable via pmset. The system will store a copy of memory to persistent storage (the disk), and will remove power to memory. The system will restore from disk image. If you want "hibernation" - slower sleeps, slower wakes, and better battery life, you should use this setting.

[Source](https://www.dssw.co.uk/reference/pmset.html)

</details>

## 📊 Status

<details>  
<summary><strong>✅ What's working</strong></summary>
</br>

- [x] Intel UHD 620 Graphics `including full graphics acceleration with Metal` (2048MB of VRAM)
- [x] Battery management and conservation mode
- [x] USB ports (type -A and -C)
- [x] HDMI
- [x] Internal camera `working fine on FaceTime, Skype, Zoom and others`
- [x] Sleep / Wake / Shutdown / Reboot
- [X] Intel WiFi & Bluetooth (thanks to [itlwm](https://github.com/OpenIntelWireless/itlwm) & [HeliPort](https://github.com/OpenIntelWireless/HeliPort) )
- [x] iMessage, FaceTime, App Store, iTunes Store `(Requires valid SMBIOS)`
- [x] Speakers and headphones combo jack
- [x] Microphone
- [x] Keyboard map and hotkeys with [YogaSMC](https://github.com/zhen-zen/YogaSMC)
- [x] Multi-Touch Screen `Touchscreen feels more natural than using Touchpad (Touchpad gesture enabled). Pen also working`
- [x] `Genesys` SD Card Reader (with macOS generic kext)

</details>

<details>  
<summary><strong>⚠️ What's not working</strong></summary>
</br>

- [ ] 🌐 Safari DRM `Use Chromium engine to watch Apple TV+, Amazon Prime Video, Netflix and others`
- [ ] 🫆 `Synaptics WBDI-SGX` Fingerprint reader - `No. Don't expect macOS driver any time soon.`
- [ ] Sidecar Wireless `doesn't work without apple native WIFI card`
- [ ] AirDrop
- [ ] Nvidia MX130 (disabled with SSDT-dGPU-Off.aml) -> Discrete graphic card is not working, since macOS doesn't support Optimus technology

</details>

<details>  
<summary><strong>🔄 Not tested</strong></summary>
</br>

- [ ] ⌚️ Apple Watch Unlock
- [ ] 🌀 Fan reading and control

</details>


## Credits

- [Apple](https://apple.com) for macOS.
- [Acidanthera](https://github.com/acidanthera) for OpenCore and all the lovely hackintosh work.
- [CorpNewt](https://github.com/corpnewt) for ProperTree, CPUFriendFriend and SSDTTime
- [Dortania](https://dortania.github.io/OpenCore-Install-Guide/) Made the OpenCore Install Guide which was used to make this EFI.
- [ic005k](https://github.com/ic005k/OCAuxiliaryTools) for OpenCore Auxiliary Tools
- [benbaker76](https://github.com/benbaker76/Hackintool) for Hackintool
- [zhen-zen](https://github.com/zhen-zen/YogaSMC) for YogaSMC
- [r/hackintosh](https://www.reddit.com/r/hackintosh/) community for helping me find solution to various issue I came across
---
