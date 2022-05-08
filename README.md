# Hackintosh MSI Z370 SLI PLUS

|  <img src="Pictures\info.png">  |
| ---- |
|  <img src="Pictures\desktop.png" width="700">  |

This repository contains OpenCore EFI for booting macOs Monterey with the following configuration: 

|  Component    |   Model   |
| ---- | ---- |
|   Motherboard & Chipset   |   MSI Z370 SLI PLUS   |
|   CPU   |   Intel Coffee Lake Family   |
|   GPU   |   iGPU with onboard HDMI output  |
|   Hard Drive   |   Sata SSD `Main`, NTFS NVMe SSD `Side` |
|   WiFi/Bluetooth   |   Intel Wireless-AC 9260   |
|   USB Ethernet   |   Android USB Ethernet/RNDIS   |

## BIOS

* **Bios Version:** 7B46vAB2(Beta version)


## EFI

* **OpenCore Version**: 0.8.0 DEBUG
* **Drivers**:
    - _OpenCanopy.efi_
    - _OpenRuntime.efi_
    - _HFSPlus.efi_
    - _NTFS.efi_ From Clover?
* **Kexts**:
    - [_VirtualSMC.kext_](https://github.com/acidanthera/VirtualSMC) 1.2.9 DEBUG
    - [_Lilu.kext_](https://github.com/acidanthera/Lilu) 1.6.0 DEBUG
    - [_WhateverGreen.kext_](https://github.com/acidanthera/WhateverGreen) 1.5.8 DEBUG
    - [_AppleALC.kext_](https://github.com/acidanthera/AppleALC) 1.7.1 DEBUG
    - [_IntelMausi.kext_](https://github.com/acidanthera/IntelMausi) 1.0.7 DEBUG
    - [_USBInjectAll.kext_](https://bitbucket.org/RehabMan/os-x-usb-inject-all/src/master/) 2018-1108
    - [_AirportItlwm.kext_](https://github.com/OpenIntelWireless/itlwm) v2.1.0 stable Monterey
    - [_IntelBluetoothFirmware.kext_](https://github.com/OpenIntelWireless/IntelBluetoothFirmware) v2.1.0
    - [_NVMeFix.kext_](https://github.com/acidanthera/NVMeFix) 1.0.9 DEBUG
    - [_BlueToolFixup.kext_](https://github.com/acidanthera/BrcmPatchRAM) 2.6.1 DEBUG
    - [_HoRNDIS.kext_](https://github.com/chris1111/HoRNDIS) Notarized HoRNDIS


## Installation

* Download macOs recovery image and create the USB with [this](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/) guide.
* Change `SMBIOS` data with following [this](https://dortania.github.io/OpenCore-Install-Guide/config.plist/coffee-lake.html#platforminfo) guide. 
* Copy `EFI` folder from this repo to the USB.

* **USB's Folder Structure**:
    - `com.apple.recovery.boot`
    - `EFI`
      - `BOOT`
      - `OC`

* Boot the USB and start the macOs Installer.


## Troubleshooting

### Black Screen | There is no output with onboard HDMI/DVI | iGpu showing only 7MB VRAM.

* Complete all steps with the `-igfxvesa` [boot flag ](https://dortania.github.io/GPU-Buyers-Guide/misc/bootflag.html#intel-boot-arguments) by editing 
    - `config.plist`>`NVRAM`>`Add`>`7C436110-AB2A-4BBB-A880-FE41995C9F82`>`boot-args`

* Install & Open [Hackintool](https://github.com/headkaze/Hackintool).
    - In `Connectors`->`Advanced` tab, check the `VRAM 2048MB`, `Enable HDMI20(4K)`, `Hotplug Reboot Fix` options.
    - Click `Generate Patch` button to generate XML tree.

* Open your `config.plist` with **TEXT EDITOR** and replace the `PciRoot(0x0)/Pci(0x2,0x0)` node with the generated one. For more information see [here]([here](https://www.tonymacx86.com/threads/guide-general-framebuffer-patching-guide-hdmi-black-screen-problem.269149/))

* Remove the `-igfxvesa` flag.