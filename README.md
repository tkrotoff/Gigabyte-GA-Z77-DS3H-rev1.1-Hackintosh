# Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh

Hackintosh for [Gigabyte GA-Z77-DS3H rev1.1](http://www.gigabyte.com/products/product-page.aspx?pid=4326) motherboard using OS X 10.10 Yosemite.  
This is a minimal guide that fits my hardware configuration.

Intel Z77 chipset, LGA1155 socket.  
Supports 3rd gen. Intel Core CPUs ([22 nm - Ivy Bridge](http://en.wikipedia.org/wiki/Ivy_Bridge_(microarchitecture))) and 2nd gen. Intel Core CPUs ([32 nm - Sandy Bridge](http://en.wikipedia.org/wiki/Sandy_Bridge)).

Onboard devices:
- Qualcomm Atheros AR8161 Gigabit Ethernet controller (DS3H rev1.0 has AR8151)
- Realtek ALC887 audio chipset

Sources:
- [AR8161 LAN on new MoBo revisions (ga-z77-ds3h and ga-h77-ds3h, others)](http://www.tonymacx86.com/desktop-compatibility/77447-ar8161-lan-new-mobo-revisions-ga-z77-ds3h-ga-h77-ds3h-others.html)

## BIOS Settings

Latest BIOS: version [F9 (2012/09/27 update)](http://www.gigabyte.com/products/product-page.aspx?pid=4326#bios)

- Save & Exit > Load Optimized Defaults
- Peripherals > SATA Mode Selection - **AHCI**
- BIOS Features > Intel Virtualization Technology - **Disabled** (or add kernel flag [`dart=0`](https://github.com/tkrotoff/Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh/issues/1) to `/Extra/org.chameleon.Boot.plist`)
- BIOS Features > VT-d - **Disabled** (or add kernel flag `dart=0`)

Note: [Intel Virtualization Technology (VT-x)](http://en.wikipedia.org/wiki/X86_virtualization#Intel_virtualization_.28VT-x.29)
is supported by almost every Intel [Sandy Bridge](http://en.wikipedia.org/wiki/Sandy_Bridge_%28microarchitecture%29)
and [Ivy Bridge](http://en.wikipedia.org/wiki/Ivy_Bridge_%28microarchitecture%29) processors.
This is not the case for [I/O MMU virtualization (VT-d)](http://en.wikipedia.org/wiki/X86_virtualization#I.2FO_MMU_virtualization_.28AMD-Vi_and_VT-d.29).

Sources:
- [How to set up the UEFI of your Hackintosh's Gigabyte motherboard](http://www.macbreaker.com/2012/08/set-up-hackintosh-gigabyte-uefi.html)
- [BIOS/UEFI Screenshots - Gigabyte Z77X-UP5-TH](http://www.tonymacx86.com/bios-uefi/130888-bios-uefi-screenshots-gigabyte-z77x-up5-th.html)

## MultiBeast

Using version 7.x

Beside defaults, check/uncheck:
- Quick Start > DSDT Free
- Drivers > Audio > Realtek ALCxxx > ALC887/888b Current
- ~~Drivers > Disk > 3rd Party SATA~~
- Drivers > Disk > TRIM Enabler (if you own a SSD disk)
- ~~Drivers > Misc > USB 3.0 - Universal ([does not work](https://github.com/tkrotoff/Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh/issues/8) for me - at least not all ports)~~
- Drivers > Network > Atheros > AtherosE2200Ethernet
- Customize > Boot Options > Verbose Boot (if you want to see what's going on)

Manually add kernel flag `UseMemDetect=No` to `/Extra/org.chameleon.Boot.plist` if "About This Mac" displays "0 MHz" for the memory.

Sources:
- [Success: Mountain Lion Gigabyte GA-Z77-DS3H, i5 3570k Ivy Bridge, 16GB](http://www.tonymacx86.com/user-builds/75407-success-mountain-lion-gigabyte-ga-z77-ds3h-i5-3570k-ivy-bridge-16gb.html)
- [Loginfailed's Build - i7-3770k / GA-Z77-DS3H / 16GB RAM / 6850](http://www.tonymacx86.com/golden-builds/74578-loginfaileds-build-i7-3770k-ga-z77-ds3h-16gb-ram-6850-a.html)
- [Gigabyte GA-Z77-DS3H Mac Install Guide](http://www.insanelymac.com/forum/topic/283293-gigabyte-ga-z77-ds3h-mac-install-guide/)
- [Building a Hackintosh](http://www.savjee.be/2012/12/building-a-hackintosh/)
- [Solution for Qualcomm Atheros AR816x, AR817x and Killer E220x](http://www.insanelymac.com/forum/topic/300056-solution-for-qualcomm-atheros-ar816x-ar817x-and-killer-e220x/)
- [How to use Multibeast 7: a comprehensive guide for Yosemite](http://www.macbreaker.com/2014/11/how-to-use-multibeast-7-yosemite-guide.html)

## Tricks

### 4K Advanced Format hard disk

To boot on a [4K Advanced Format hard disk](http://en.wikipedia.org/wiki/Advanced_Format), check [How to fix the boot0 error for your Hackintosh](http://www.macbreaker.com/2012/02/hackintosh-boot0-error.html) and [boot0 Error: The Official Guide](http://www.tonymacx86.com/25-boot0-error-official-guide.html).

### Fix copy-pasted kexts inside /System/Library/Extensions (S/L/E)

```Shell
sudo chown -R root:wheel MyKext.kext # owner: root, group: wheel
sudo chmod -R 755 MyKext.kext        # user: r+w+x, group: r+x, world: r+x
```

### Prevent OS X from mounting a volume

```Shell
sudo vifs
```

Example:
```
# Do not mount NTFS disk 'Windows 7 Boot'
LABEL=Windows\0407\040Boot none ntfs ro,noauto

# Do not mount NTFS disk 'HD502HJ'
LABEL=HD502HJ none ntfs ro,noauto

# Mount NTFS disk 'HD204UI' in read-write mode (experimental: at your own risk)
# Option 'nobrowse' is mandatory. You will have to manually open /Volumes/HD204UI
# using the Finder or Disk Utility
LABEL=HD204UI none ntfs rw,auto,nobrowse

# Do not mount ExFAT disk 'WD20EZRX'
LABEL=WD20EZRX none exfat rw,noauto
```

Sources:
- [Write in NTFS using Mavericks](http://apple.stackexchange.com/a/112990)
- [Prevent a partition from mounting in OS X](http://www.cnet.com/how-to/prevent-a-partition-from-mounting-in-os-x/)

## Performance

Using [Geekbench](http://www.primatelabs.com/geekbench/), you should get a score (Intel Core i7-3770 @ 3.40 GHz) > 3000 (single-core) ~13000 (multi-core), see [issue #2](https://github.com/tkrotoff/Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh/issues/2).

## License

Do whatever you like, this is public domain.
