# Gigabyte GA-Z77-DS3H rev1.1 Hackintosh

Hackintosh for [Gigabyte GA-Z77-DS3H rev1.1](https://www.gigabyte.com/Motherboard/GA-Z77-DS3H-rev-11#ov) motherboard using macOS Monterey (version 12).

macOS Monterey is the last version that works for non-[AVX2](https://en.wikipedia.org/wiki/Advanced_Vector_Extensions#Advanced_Vector_Extensions_2) CPUs.

[Intel Z77 chipset](https://ark.intel.com/content/www/us/en/ark/products/64024/intel-z77-express-chipset.html), [LGA 1155 socket](https://en.wikipedia.org/wiki/LGA_1155).
Supports 3rd gen. ([22 nm - Ivy Bridge](<https://en.wikipedia.org/wiki/Ivy_Bridge_(microarchitecture)>)) and 2nd gen. ([32 nm - Sandy Bridge](https://en.wikipedia.org/wiki/Sandy_Bridge)) Intel Core CPUs.

Onboard devices:

- Qualcomm Atheros AR8161 Gigabit Ethernet controller (DS3H rev1.0 has AR8151)
- Realtek ALC887 audio chipset

This is a minimal guide that fits my hardware configuration:

- [Intel Core i7-3770](https://ark.intel.com/content/www/us/en/ark/products/65719/intel-core-i73770-processor-8m-cache-up-to-3-90-ghz.html)
- [Sapphire NITRO+ RX 580 8G G5](https://www.sapphiretech.com/en/consumer/nitro-rx-580-8g-g5)
- [802.11ac WiFi card Broadcom BCM94360CD](https://github.com/tkrotoff/Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh/issues/10)
- [SSD Crucial MX500](https://www.crucial.com/ssd/mx500/ct2000mx500ssd1)

## OpenCore documentation

https://dortania.github.io/OpenCore-Install-Guide/

https://dortania.github.io/docs/release/Configuration.html

Check comments in [EFI/OC/config.plist](EFI/OC/config.plist)

⚠️ Use [GenSMBIOS](https://github.com/corpnewt/GenSMBIOS) to change SystemSerialNumber, MLB, SystemUUID, ROM in Root > PlatformInfo > Generic

Similar systems:

- Z77-DS3H rev1.0: https://www.tonymacx86.com/threads/robbishs-8yr-old-atx-ivybridge-hackintosh-ga-z77-ds3h-i5-3570k-hd-4000-opencore-macos-big-sur.311037/
- Z77-DS3H rev?: https://www.insanelymac.com/forum/topic/348196-z77-ds3h-opencore-073-monterey-beta-3-perfect-install
- Z77X-D3H: https://github.com/nickw444/opencore-efi-z77

## BIOS Settings

[BIOS](https://www.gigabyte.com/Motherboard/GA-Z77-DS3H-rev-11/support#support-dl-bios): F9 (2012/09/27 latest stable), F11a (2013/11/13 latest beta - recommended)

- Save & Exit > Load Optimized Defaults
- BIOS Features
  - Fast Boot > _Disabled_
  - Execute Disable Bit > _Enabled_
  - Intel Virtualization Technology (i.e. VT-x) > _Enabled_ (default is Disabled)
  - VT-d > _Disabled_ (default is Enabled) (Enabled if DisableIoMapper is true in config.plist)
  - OS Type > _Windows 8 WHQL_ (default is Other OS)
  - CSM Support > _Never_ (default is Always)
  - Secure Boot > _Disabled_
- Peripherals
  - SATA Mode Selection > _AHCI_ (default is IDE)
  - XHCI Pre-Boot Driver > Enabled
  - xHCI Mode > _Enabled_ (default is Smart Auto)
  - Internal Graphics > _Disabled_ (default is Auto)
  - Intel Rapid Start Technology > _Disabled_
  - Legacy USB Support > Disabled (default is Enabled)
  - XHCI Hand-off > _Enabled_
  - EHCI Hand-off > _Enabled_ (default is Disabled)
  - Port 60/64 Emulation > Disabled
  - Trusted Computing > TPM Support > _Disable_
  - Super IO Configuration > Serial Port A > _Disabled_

## Mount EFI

```
diskutil list
sudo diskutil mount disk0s1
```

## License

Do whatever you like, this is public domain.
