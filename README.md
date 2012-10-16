mkinitcpio-antievilmaid
=======================

This hook allows for Anti Evil Maid support for devices with a TPM. It is
essentially a port of the Dracut module by Invisible Things Lab to mkinitcpio.

Usage
-----
* Prepare a USB stick using the [Anti Evil Maid](http://theinvisiblethings.blogspot.com/2011/09/anti-evil-maid.html) utility.
* Add the `antievilmaid` hook to your /etc/mkinitcpio.conf. It needs to be placed before the `encrypt` hook to be effective, and you should also make sure that you have the `udev` and `usb` hooks before it. For example,
    HOOKS="base consolefont keymap udev autodetect pata scsi sata usb antievilmaid encrypt lvm2 filesystems usbinput fsck"
* Reboot, mount your USB stick at /boot, and then seal a secret passphrase. This process will need to be repeated each time you do a kernel upgrade.
    echo "This is my secret passphrase." | tpm_sealdata -z -o /boot/antievilmaid/sealed_secret.blob --pcr 0 --pcr 1 --pcr 2 --pcr 3 --pcr 4 --pcr 8 --pcr 9 --pcr 12 --pcr 14
