# How to build an EFI for Dell Latitude E5450
This guide will help you make your ol' Dell laptop become a MacBook Air, and say goodbye Windows!
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
    * USBInjectAll (required when installing macOS)
    * VoodooI2C.kext
    * VoodooI2CHID.kext
    * VoodooPS2Controller.kext
    * SATA-unsupported.kext
