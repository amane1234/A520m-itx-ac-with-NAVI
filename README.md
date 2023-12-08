# A520m-itx/ac ryzen Hackintosh

EFI for A520m-itx/ac ryzen cpu and NAVI GPU


### Desktop Spec

| Component        | Brank                              |
| ---------------- | ---------------------------------- |
| CPU              | Ryzen 3300x                        |
| dGPU             | Sapphire RX 5700XT                 |
| Mainboard        | ASRock A520m-itx/ac                |
| NVMe             | WD Blue SN570 NVMe                 |
| SmBios           | MacPro 7,1                         |
| BootLoader       | OpenCore 0.9.6                     |
| macOS            | Sonoma                             |


### Intel WIFI/BT
You need to manually download and install itlwm.kext (or airportitlwm.kext) to use WIFI

itlwm / Airportitlwm : https://github.com/OpenIntelWireless/itlwm

Heliport : https://github.com/OpenIntelWireless/HeliPort


### What works:

Every function (including Sleep at S3) works well.


### Bugs:

- Blackscreen after wake-up and POST randomly.

- A2 Error (Boot device undetected) during POST.

- Since intel Wi-Fi/Bluetooth are not officially supported in MacOS, it might be laggy.
  

ASRock motherboards are not good for hackintoshing, change your motherboard into different manufacture (ASUS,GIGABYTE) will resolve blackscreen errors.


### SMBIOS:

This hackintosh EFI uses MacPro 7,1 SMBIOS.

Create your own MacPro 7,1 SMBIOS with GenSMBIOS

https://github.com/corpnewt/GenSMBIOS


### MacOS bootable USB creation:
- Read the Dortania guide for creating your USB from Windows or macOS
- [Guide Dortania](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/) - USB creation
- Download EFI and copy it to your USB drive.


## Bios settings
### Enable :
Resizable BAR Support
Above 4G encoding


### Disable : 
CSM Support
