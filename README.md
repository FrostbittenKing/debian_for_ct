Cubietruck Debian Image
======================

This is my debian image for the cubietruck. It is based on [this](http://blog.night-shade.org.uk/2013/12/building-a-pure-debian-armhf-rootfs/) and
[this](http://blog.night-shade.org.uk/2013/12/create-a-bootable-sd-for-a-cubietruck/) guide.

Requirements:

 * >4GB microSD card
 * cubietruck

How to install:

 * do everything as root, or use sudo
 * wipe sdcard with sdisk:
   1. fdisk /dev/sdX
   2. type 'o' to create a new disk label/wipe partitions
   3. create a new 256MB partiton, with 'n', 'p' etc etc.
   4. create another partiton, assign the remaining space to it

 * dd if=u-boot-sunxi-with-spl-ct-20131102.bin of=/dev/sdX bs=1024 seek=8
 * mkfs.ext2 /dev/sdX1
 * mkfs.ext4 /dev/sdX2
 * mount /dev/sdX1 /mnt/cubie_deb
 * tar -C /mnt/cubie_deb -xvf bootfs-part1.tar.gz
 * umount /mnt/cubie_deb
 * sync
 * mount /dev/sdX2 /mnt/cubie_deb
 * tar -C /mnt/cubie_deb -xvf cubie_rootfs.tar.xz
 * umount /mnt/cubie_deb
 * sync

Now insert the microSD card into the sdcard reader of your cubietruck, and boot it.

No users have been created, except root with pw: root.
