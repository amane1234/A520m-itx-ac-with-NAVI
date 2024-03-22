# A520m-itx/ac ryzen Hackintosh

Opencore EFI for A520m-itx/ac ryzen cpu and NAVI GPU



## Desktop Spec

| Component        | Brank                              |
| ---------------- | ---------------------------------- |
| CPU              | Ryzen 3300x                        |
| dGPU             | Sapphire RX 5700XT                 |
| Mainboard        | ASRock A520m-itx/ac                |
| NVMe             | WD Blue SN570 NVMe                 |
| SmBios           | MacPro 7,1                         |
| BootLoader       | OpenCore 1.0.0                     |
| macOS            | Sonoma 14.4                        |



## Intel WIFI/BT
You need to manually download and install itlwm.kext (or airportitlwm.kext) to use WIFI

itlwm / Airportitlwm : https://github.com/OpenIntelWireless/itlwm

Heliport : https://github.com/OpenIntelWireless/HeliPort


## Function / Bugs


### Functions:

Every function works except Apple airportcard required ones ,such as sidecar and airdrop. 

You may swap your wifi card into natively supported devices BCM94360 or BCM94350 with OCLP patcher to work these functions properly. My recommandation is wireless modules from "Fenvi"



### Bugs:

- Random blackscreen during POST.
- A2 Error (Boot device undetected) during POST.
- Since intel Wi-Fi/Bluetooth are not officially supported in MacOS, it might be laggy.

ASRock motherboards are not good for hackintoshing, change your motherboard into different manufactures such as ASUS,GIGABYTE may resolve A2 Boot errors.
(Seems ASRock motherboards sometimes cannot recongnize Bootstrap related efi partitions)

If you experience blackscreen/unresponsiveness before OC picker, you may try manual boot config with efibootmgr : https://www.reddit.com/r/hackintosh/comments/fj3zrj/booting_opencore_without_the_usb_on_an_asrock/


## SMBIOS

This hackintosh EFI uses MacPro 7,1 SMBIOS.

Create your own MacPro 7,1 SMBIOS with GenSMBIOS

https://github.com/corpnewt/GenSMBIOS



## MacOS bootable USB creation

- Read the Dortania guide for creating your USB from Windows or macOS
- [Guide Dortania](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/) - USB creation
- Download EFI and copy it to your USB drive.
- Replace SMBIOS parameters.


## Bios settings


### Enable :
Resizable BAR Support / 
Above 4G encoding



### Disable : 
CSM Support



## (Optional) Radeon Sensor

https://github.com/aluveitie/RadeonSensor



## (Optional) Adobe support for ryzen hackintosh devices

https://github.com/NyaomiDEV/AMDFriend

Since photoshop 25, no additional adobe patch is required.


## Disable ACPI injections for OS multi booting by using OpenCore_NO_ACPI_Build

Ryzentosh requires a lot of SSDT / Patch / Quirks modifications, which are the main reasons of BSOD in Windows.

If you are using Ryzentosh and Windows, I recommand to use NO_ACPI_Build version of OC.



### How to:

Download the correct OpenCore_NO_ACPI_Build that matches your OpenCore version and unzip it 

https://github.com/wjz304/OpenCore_NO_ACPI_Build/releases

Replace the following files in your EFI Folder:

    BootX64.efi (in EFI/Boot)
    OpenCore.efi (in EFI/OC)
    Any Drivers you use (in EFI/OC/Drivers)
    Any Tools you use (in EFI/OC/Tools)

Add the following Keys to your config.plist:

    Under ACPI/Quirks, add: EnableForAll (Type: Boolean) and set it to False
    Under Booter/Quirks, add: EnableForAll (Type: Boolean) and set it to False
