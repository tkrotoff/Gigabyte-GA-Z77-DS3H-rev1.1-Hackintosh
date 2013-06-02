# Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh

Hackintosh for [Gigabyte GA-Z77-DS3H rev1.1](http://www.gigabyte.com/products/product-page.aspx?pid=4326) motherboard using OS X 10.8.3 Mountain Lion.  
This is a minimal guide that fits my hardware configuration.

Intel Z77 chipset.  
Supports 3rd Gen. Intel 22nm CPUs and 2nd Gen. Intel Core CPUs (LGA1155 socket).

Onboard devices:

- Qualcomm Atheros AR8161 Gigabit Ethernet controller
- Realtek ALC887 audio chipset

Sources:

- [AR8161 LAN on new MoBo revisions (ga-z77-ds3h and ga-h77-ds3h, others)](http://www.tonymacx86.com/desktop-compatibility/77447-ar8161-lan-new-mobo-revisions-ga-z77-ds3h-ga-h77-ds3h-others.html)

## BIOS Settings

Latest BIOS: version [F9 (2012/09/27 update)](http://www.gigabyte.com/products/product-page.aspx?pid=4326#bios)

- Save & Exit / Load Optimized Defaults
- Peripherals / SATA Mode Selection - **AHCI**
- BIOS Features / Intel Virtualization Technology - **Disabled** (or add kernel flag [`dart=0`](https://github.com/tkrotoff/Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh/issues/1))
- BIOS Features / VT-d - **Disabled** (or add kernel flag `dart=0`)

Note: [Intel Virtualization Technology (VT-x)](http://en.wikipedia.org/wiki/X86_virtualization#Intel_virtualization_.28VT-x.29)
is supported by almost every Intel [Sandy Bridge](http://en.wikipedia.org/wiki/Sandy_Bridge_%28microarchitecture%29)
and [Ivy Bridge](http://en.wikipedia.org/wiki/Ivy_Bridge_%28microarchitecture%29) processors.
This is not the case for [I/O MMU virtualization (VT-d)](http://en.wikipedia.org/wiki/X86_virtualization#I.2FO_MMU_virtualization_.28AMD-Vi_and_VT-d.29).

Sources:

- [How to set up the UEFI of your Hackintosh's Gigabyte motherboard](http://www.macbreaker.com/2012/08/set-up-hackintosh-gigabyte-uefi.html)
- [Gigabyte Z77-DS3H Hackintosh - BIOS Settings](http://myhackmac.blogspot.fr/p/bios-settings.html)

## DSDT

No DSDT needed!

Sources:

- [Huge News! Gigabyte UEFI Sleep/Wake with NO DSDT! [TESTING]](http://www.tonymacx86.com/buying-advice/49446-huge-news-gigabyte-uefi-sleep-wake-no-dsdt-testing.html)

## MultiBeast

Using version 5.3.0.

Check:

- UserDSDT or DSDT-Free Installation
- Audio / Realtek ALC8xx / Without DSDT / ALC887/888b / Current ([mute does not work](https://github.com/tkrotoff/Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh/issues/3))
- Disk / TRIM Enabler (if you own a SSD disk)
- Network / Atheros - Shailua's ALXEthernet
- Boot Options / GraphicsEnabler=No (if you own a natively supported GPU like the Nvidia GeForce GT 640)
- Boot Options / Verbose Boot (if you want to see what's going on)

Sources:

- [Success: Mountain Lion Gigabyte GA-Z77-DS3H, i5 3570k Ivy Bridge, 16GB](http://www.tonymacx86.com/user-builds/75407-success-mountain-lion-gigabyte-ga-z77-ds3h-i5-3570k-ivy-bridge-16gb.html)
- [Loginfailed's Build - i7-3770k / GA-Z77-DS3H / 16GB RAM / 6850](http://www.tonymacx86.com/golden-builds/74578-loginfaileds-build-i7-3770k-ga-z77-ds3h-16gb-ram-6850-a.html)
- [Experimental Atheros AR81(31/32/51/52/61/62/71/72) Driver for 10.7/10.8](http://www.insanelymac.com/forum/topic/284119-experimental-atheros-ar813132515261627172-driver-for-107108/)
- [Gigabyte GA-Z77-DS3H Mac Install Guide](http://www.insanelymac.com/forum/topic/283293-gigabyte-ga-z77-ds3h-mac-install-guide/)

## Remarks

- If you want to boot on a [4K Advanced Format hard disk](http://en.wikipedia.org/wiki/Advanced_Format), check [How to fix the boot0 error for your Hackintosh](http://www.macbreaker.com/2012/02/hackintosh-boot0-error.html)

## Tricks

### Fix copy-pasted kexts inside /System/Library/Extensions (S/L/E)

```
sudo chown -R root:wheel MyKext.kext # owner: root, group: wheel
sudo chmod -R 755 MyKext.kext        # user: r+w+x, group: r+x, world: r+x
```

## License

Do whatever you like, this is public domain.
