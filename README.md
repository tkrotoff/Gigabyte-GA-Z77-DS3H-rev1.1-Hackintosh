# Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh

Hackintosh for [Gigabyte GA-Z77-DS3H rev1.1](http://www.gigabyte.com/products/product-page.aspx?pid=4326) motherboard using OS X 10.8.2 Mountain Lion.

Intel Z77 chipset.

Supports 3rd Gen. Intel 22nm CPUs and 2nd Gen. Intel Core CPUs (LGA1155 socket).

Onboard devices:

- Qualcomm Atheros AR8161 Gigabit Ethernet controller
- Realtek ALC887 audio chipset

Sources:

- [AR8161 LAN on new MoBo revisions (ga-z77-ds3h and ga-h77-ds3h, others)](http://www.tonymacx86.com/desktop-compatibility/77447-ar8161-lan-new-mobo-revisions-ga-z77-ds3h-ga-h77-ds3h-others.html)

## BIOS Settings

Latest BIOS: version [F9 (2012/09/27 update)](http://www.gigabyte.com/products/product-page.aspx?pid=4326#bios)

- SATA Mode Selection - **AHCI**
- Intel Virtualization Technology - **Disabled** (or add kernel flag [`dart=0`](https://github.com/tkrotoff/Gigabyte-GA-Z77-DS3H-rev1.1-Hackintosh/issues/1))
- VT-d - **Disabled**  (or add kernel flag `dart=0`)

## DSDT

No DSDT needed!

Sources:

- [Huge News! Gigabyte UEFI Sleep/Wake with NO DSDT! [TESTING]](http://www.tonymacx86.com/buying-advice/49446-huge-news-gigabyte-uefi-sleep-wake-no-dsdt-testing.html)

## MultiBeast

Using version 5.2.1.

Check:

- UserDSDT or DSDT-Free Installation
- ALC887/888b Current
- TRIM Enabler (if you own a SSD disk)
- Atheros - Shailua's ALXEthernet
- GraphicsEnabler=No (if you own a natively supported GPU like the Nvidia GeForce GT 640)

Sources:

- [Success: Mountain Lion Gigabyte GA-Z77-DS3H, i5 3570k Ivy Bridge, 16GB](http://www.tonymacx86.com/user-builds/75407-success-mountain-lion-gigabyte-ga-z77-ds3h-i5-3570k-ivy-bridge-16gb.html)
- [Loginfailed's Build - i7-3770k / GA-Z77-DS3H / 16GB RAM / 6850](http://www.tonymacx86.com/golden-builds/74578-loginfaileds-build-i7-3770k-ga-z77-ds3h-16gb-ram-6850-a.html)
- [Experimental Atheros AR81(31/32/51/52/61/62/71/72) Driver for 10.7/10.8](http://www.insanelymac.com/forum/topic/284119-experimental-atheros-ar813132515261627172-driver-for-107108/)
- [Gigabyte GA-Z77-DS3H Mac Install Guide](http://www.insanelymac.com/forum/topic/283293-gigabyte-ga-z77-ds3h-mac-install-guide/)

## License

Do whatever you like, this is public domain.
