# windows-boot-repair-trouble-shooting-notes
## Rebuilding EFI Boot After CMS/UEFI Transition on Gigabyte X470 using microsd and windows 7 laptop

## Problem: 
  Attempted to enable TPM 2.0 and Secure Boot for Windows 11 Upgrade. Disabling CMS Supper caused all UEFI boot entries to be lost, leaving system unable to boot

## Envirement: 
  - Motherboard- Gigabyte X470 Aorus Ultra Gaming (BIOS F61c)
  - CPU: AMD Ryzen 9 5900x
  - OS: Windows 10
  - Recovery Media created on: Windows 7 laptop using 7-Zip and diskpart

## Root Cause:
  Disabling CMS (Compatibility Support Module) in BIOS removed legacy boot entries. The system had no UEFI boot entry pointing to Windows EFI partition, so it could not find a bootable device.

## Resolution: 
  - Created bootable Windows 11 x64 media on a microSD card using 7-Zip to extract the ISO and diskpart to format and mark the partition active
  - Booted from the microSD into WIndows 11 setup
  - Opened Command Prompt via Troubleshoot > Advance Options > Command Prompt
  - Used diskpart to identify the correct volume letters
  - Rebuilt EFi boot files with bcdboot

## Key commands:
```
  diskpart
  list vol
  exit
  bcdboot G:\Windows /s C: /f UEFI
  
```
## Result: 
  Boot files successfully recreated. System booted into Windows normally
