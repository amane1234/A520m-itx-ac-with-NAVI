
---

# A520M-ITX/AC Ryzen Hackintosh

**OpenCore EFI for ASRock A520M-ITX/AC with Ryzen CPU and NAVI GPU**

---

## Desktop Specifications

| **Component**    | **Brand/Model**                    |
| ---------------- | ---------------------------------- |
| **CPU**          | AMD Ryzen 3300X                    |
| **dGPU**         | Sapphire RX 5700XT                 |
| **Motherboard**  | ASRock A520M-ITX/AC                |
| **NVMe**         | WD Blue SN570 NVMe                 |
| **SMBIOS**       | MacPro 7,1                         |
| **Bootloader**   | OpenCore 1.0.0                     |
| **macOS Version**| macOS 15.1 (Sequoia)               |

---

## Intel Wi-Fi/Bluetooth Support

To enable Intel Wi-Fi and Bluetooth on macOS, you need to install the appropriate kexts. The recommended kexts for this are:

- **itlwm.kext** (or **airportitlwm.kext**) for Intel Wi-Fi:  
  [GitHub - itlwm](https://github.com/OpenIntelWireless/itlwm)
  
- **HeliPort**: A macOS menu bar app to manage Intel Wi-Fi connections:  
  [GitHub - HeliPort](https://github.com/OpenIntelWireless/HeliPort)

---

## System Functionality & Known Issues

### **Working Features**:
- Everything works as expected except for Apple Airport Card functionalities and S4 (Hibernate) sleep.

### **To Enable Full Functionality**:
- You can swap your Intel Wi-Fi/Bluetooth card with a natively supported one (such as the **BCM94360** or **BCM94350**), and use patches from **OpenCore Legacy Patcher (OCLP)** to ensure full support for Apple features.

### **Known Bugs**:
- **A2 Error (Boot device undetected)**: This occurs during POST because ASRock motherboards sometimes fail to detect the EFI partition, even on Windows or Linux.
- **Intel Wi-Fi/Bluetooth**: These devices are not officially supported by macOS and may experience lag or instability.
- **Internal USB LED Controller (Port 11)**: The internal USB LED controller is disabled due to erratic behavior during shutdown and reboot. The LED controller cannot be turned off via the S5 call from macOS.

---

## SMBIOS Configuration

This EFI uses the **MacPro 7,1** SMBIOS, which is recommended for optimal compatibility with modern AMD Ryzen CPUs.

### **Creating Your Own SMBIOS**:
To create or modify your own **MacPro 7,1** SMBIOS, use **GenSMBIOS**:

- [GenSMBIOS GitHub Repository](https://github.com/corpnewt/GenSMBIOS)

---

## Creating a macOS Bootable USB

Follow the Dortania guide to create a bootable macOS USB from either Windows or macOS:

- [Dortania OpenCore Install Guide](https://dortania.github.io/OpenCore-Install-Guide/installer-guide/)

### Steps:
1. **Download the EFI folder** from this release tap and copy it to your USB EFI partition.
2. Replace the **SMBIOS** parameters with your own.
3. Ensure that your USB drive is set up properly using the instructions from Dortania.

---

## BIOS Settings for ASRock A520M-ITX/AC

To ensure compatibility with macOS, adjust the following BIOS settings:

### **Enable**:
- **Resizable BAR Support**
- **Above 4G Decoding**

### **Disable**:
- **CSM Support** (Compatibility Support Module)

---

## Multi-Booting with Windows (Optional)

### **Disabling ACPI injections**:
If you're dual-booting Windows and macOS on your Ryzen system, it's recommended to disable ACPI injections to avoid BSODs and other issues in Windows.

Use the **OpenCore_NO_ACPI_Build** to prevent ACPI-related conflicts.

### Steps:
1. Download the **OpenCore_NO_ACPI_Build** version that matches your current OpenCore version:  
   [OpenCore_NO_ACPI_Build Releases](https://github.com/wjz304/OpenCore_NO_ACPI_Build/releases)
2. Extract the files and replace the following in your EFI folder:
    - **BootX64.efi** (in `EFI/Boot`)
    - **OpenCore.efi** (in `EFI/OC`)
    - Any **Drivers** and **Tools** you use in the respective folders (`EFI/OC/Drivers`, `EFI/OC/Tools`)
3. Modify the `config.plist`:
    - Under **ACPI/Quirks**, add:  
      `EnableForAll` (Type: **Boolean**) → **False**
    - Under **Booter/Quirks**, add:  
      `EnableForAll` (Type: **Boolean**) → **False**

This will ensure that ACPI modifications don't affect other operating systems.

---
