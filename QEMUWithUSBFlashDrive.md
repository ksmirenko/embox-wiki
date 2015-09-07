To enable USB-flash on qemu start one with following flags
> -device pci-ohci -device usb-host,hostbus=2,hostaddr=3

where:
* **pci-ohci** - pci host controller
* **hostbus && hostaddr** - usb device place which you want to connect. You can show device's list with 'lsusb' command on the host

To create template you should add to x86/qemu following:
*  @Runlevel(2) include embox.driver.usb.hc.ohci_pci
*  @Runlevel(2) include embox.driver.usb.class.mass_storage
*  include embox.cmd.hw.lsusb.lsusb
*  include embox.cmd.usb_whitelist

To format usb-drive use command:
> sudo mkfs.msdos -n EmboxFAT -F 12 /dev/sdb 65536 -I