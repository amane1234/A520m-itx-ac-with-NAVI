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
| macOS            | Sequoia 15.1                       |



## Intel WIFI/BT

You need to manually download and install itlwm.kext (or airportitlwm.kext) to use intel WIFI

itlwm / Airportitlwm : https://github.com/OpenIntelWireless/itlwm

Heliport : https://github.com/OpenIntelWireless/HeliPort


## Function / Bugs


### Functions:

Everything works except Apple airportcard required functions, and S4(Hibernation) sleep.

You may swap your wifi card into natively supported devices, such as BCM94360 or BCM94350, with patches from OCLP to work these functions properly.



### Bugs:

- A2 Error (Boot device undetected) during POST, because ASRock motherboards sometimes cannot detect EFI partition (Even Windows and Linux) during POST.
- Intel Wi-Fi/Bluetooth are not officially supported in MacOS, they could be laggy.
- Internal USB LED controller (Port 11) is disabled due to laggy behavior. The USB


#### Internal USB LED controller bugs:






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



## Disable ACPI injections for OS multi booting by using OpenCore_NO_ACPI_Build

Ryzentosh requires a lot of SSDT / Patch / Quirks modifications, which are the main reasons of BSOD in Windows.

If you are dual-booting both Ryzen hackintosh and Windows OS, I recommand to use NO_ACPI_Build version of OC.



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
