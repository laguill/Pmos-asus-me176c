# Pmos-asus-me176c
My journey on pmos on tablet Asus memo pad 7 (manjaro)

0. Requirements
Install adb and fastboot 
$ sudo pacman -S android-tools
Flash ths stock device following this guide
https://wiki.postmarketos.org/wiki/ASUS_MeMO_Pad_7_(asus-me176c)

1. Install me176c-boot (unlock bootloader)
https://github.com/me176c-dev/me176c-boot#readme

2. Install twrp
https://forum.xda-developers.com/t/recovery-2019-06-09-unofficial-twrp-3-3-1-for-asus-memo-pad-7-me176c-x.3745190/

3. Install pmbootsrap to install the pmos
https://wiki.postmarketos.org/wiki/Installing_pmbootstrap

4. Create boot and root prebuild images of the device
https://wiki.postmarketos.org/wiki/Installation_guide

Run 
$ pmbootstrap install
I cannot manage to install pmos on internal memory you will need a sdcard
Using an adapter then run 
$ lsblk
to find the block device before running 
$ pmbootstrap install --sdcard=/dev/mmcblk

5. Flash boot partition
$ pmbootstrap flasher flash_rootfs

6. Create a pmos.conf file to boot on pmos
<nowiki>
'title    postmarketOS
volume   80868086-8086-8086-8086-000000000007
linux    /vmlinuz
initrd   /intel-ucode.img
initrd   /acpi-me176c.img
initrd   /initramfs
//Comment this out to get more output on screen while booting
options  console=null</nowiki>'

7. To boot by default on pmos change loader.conf file
  esp/loader/loader.conf
  Change andrdoid by pmos
  <nowiki>
  default  android
auto-entries  no</nowiki>

# Uncomment this to always show the boot menu
#timeout  3
Then you can use adb push to move the the file in the internal storage
    
  
  

