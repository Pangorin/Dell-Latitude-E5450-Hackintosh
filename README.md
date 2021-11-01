# How to build an EFI for Dell Latitude E5450
This guide will help you make your ol' Dell laptop become a MacBook Air, and say goodbye Windows!
* Notes: before copying the EFI into USB boot drive, make sure your have copy the Resources folder from OpenCorePkg into the EFI/OC folder. And you need a mouse to install macOS first, once you've done the installation process, head to this guide: [Fixing trackpads](https://dortania.github.io/Getting-Started-With-ACPI/Laptops/trackpad.html) in order to make the trackpad working.

## Preparation
* Time
* Some Google-ing skills
## About my laptop specs
  - CPU: Intel Core i5-5300U (Broadwell-U)
  - RAM: Micron 4GB DDR3L 1600MHz
  - Graphics: Intel HD 5500
  - Storage (Windows + macOS): Western Digital Green 240GB
## Installation

How to make the USB boot drive:
 - Windows: [click here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/winblows-install.html)
  - macOS: [click here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/mac-install.html) (this guide is mainly using for hackintosh the Mac which can't run the new macOS. Though, you can still using this method to make a boot drive for desktops and laptops build)
  - Linux: [click here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/linux-install.html)

Prepare the base OpenCore system: [click here](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/opencore-efi.html).

Necessary files: [click here](https://dortania.github.io/OpenCore-Install-Guide/ktext.html).

The drivers, kexts, and SSDTs I used are as follows:
  - Driver:
    * HfsPlus.efi
    * OpenRuntime.efi (included with OpenCore)

 - Kext:
    * Lilu.kext
    * WhateverGreen.kext
    * VirtualSMC.kext
      * SMCProcessor.kext
      * SMCSuperIO.kext
      * SMCLightSensor.kext
      * SMCDellSensors.kext
      * SMCBatteryManager.kext
    * USBInjectAll.kext
    * IntelMausi.kext
    * IntelSnowMausi.kext
    * USBInjectAll (required when installing macOS, you can delete this kext after you map your USB and replace it with USBMap you generated)
    * VoodooI2C.kext
    * VoodooI2CHID.kext
    * VoodooPS2Controller.kext
    * SATA-unsupported.kext

  - SSDT:
    * SSDT-PLUG-DRTNIA.aml
    * SSDT-EC-LAPTOP.aml
    * SSDT-PNLF.aml
    * SSDT-GPI0.aml (this SSDT does not included in the EFI, you have to patching it when you have installed macOS)

## OpenCore Configuration

Follow the OpenCore Install Guide to [setup the config.plist](https://dortania.github.io/OpenCore-Install-Guide/config.plist/) and [configure for Intel Broadwell Laptops](https://dortania.github.io/OpenCore-Install-Guide/config-laptop.plist/broadwell.html#starting-point).
> - If you have no audio, please find another `layout-id`.
> - Where to find my `layout-id`? [AppleALC Supported Codecs](https://github.com/acidanthera/AppleALC/wiki/Supported-codecs).

| SMBIOS          | CPU Type           | GPU Type      | Display size |
| ----------------| -------------------|---------------|--------------|
| `MacBookAir7,2` | Dual Core 15W      | iGPU: HD 6000 | 13"          |

This SMBIOS is suitable for our Dell, because our laptop's CPU has similar TDP compare to the MacBook Air early 2015 and Mid 2017.

## BIOS Setting
- Enable:
  * Hyper-Threading
  * SATA Mode: AHCI (or RAID, your choice)
- Disable:
  * Fast Boot
  * Secure Boot
  * Serial/COM Port
  * Parallel Port
  * Intel Platform Trust

