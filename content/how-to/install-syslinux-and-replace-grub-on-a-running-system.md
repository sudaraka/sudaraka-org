{
  "title": "Install Syslinux and replace GRUB on a running system",
  "description": "Install Syslinux and replace GRUB on a running system - How to replace GRUB on a running (Arch) Linux system and install Syslinux on it.",
  "keywords": "howto,install syslinux,replace grub,linux",
  "date": "2012-08-12"
}

This article explains how to replace the existing boot loader (assumed GRUB
legacy) on a running system, and install Syslinux on it. Instructions here are
tested on a Arch Linux, but should work on any Linux distribution except for the
package installation bit.<!--more-->

&nbsp;

## Back Story

When I first installed my Arch Linux system about year ago I choose GRUB
(legacy) as my boot loader without giving it much though as it was the one
I'm most familiar with.

Now with the recent GRUB legacy deprecation, I wanted to upgrade my boot
loader and while reading about upgrading to GRUB2 I noticed that it is much
easier to just switch to Syslinux instead (at least for me).

I'm using an old fashion MBR based partitions on my system with /boot on a
separated ext2 partition. And I decided to do change/upgrade as follows.

&nbsp;

## Steps

  - [Re-format /boot with ext4](#re-format-boot-with-ext4)
  - [Install & configure Syslinux](#install-configure-syslinux)
  - [Wipe out GRUB (optional)](#wipe-out-grub-optional)

&nbsp;

### Re-format /boot with ext4

First thing to we need to do is backup our existing kernel files to somewhere
temporarily.

<pre class="console">
<strong>$</strong> <kbd>mkdir /tmp/boot-backup</kbd>
<strong>$</strong> <kbd>cp -v /boot/{vmlinuz,initramfs}* /tmp/boot-backup/</kbd>
‘/boot/vmlinuz-linux’ -> ‘/tmp/boot-backup/vmlinuz-linux’
‘/boot/initramfs-linux-fallback.img’ -> ‘/tmp/boot-backup/initramfs-linux-fallback.img’
‘/boot/initramfs-linux.img’ -> ‘/tmp/boot-backup/initramfs-linux.img’
</pre>

&nbsp;

**Note:** above command will only copy the files standard naming conversion
of the Linux Kernel used in Arch Linux. If your distribution is using a
different naming convention or you are using a custom kernel, make sure you
copy all the files require the Kernel to boot.

Now to re-format the /boot partition.

<pre class="console">
<strong>#</strong> <kbd>umount /boot</kbd>
<strong>#</strong> <kbd>mkfs.ext4 /dev/sda1</kbd>
mke2fs 1.42.4 (12-June-2012)
Filesystem label=
OS type: Linux
Block size=1024 (log=0)
Fragment size=1024 (log=0)
Stride=0 blocks, Stripe width=0 blocks
51200 inodes, 204800 blocks
10240 blocks (5.00%) reserved for the super user
First data block=1
Maximum filesystem blocks=67371008
25 block groups
8192 blocks per group, 8192 fragments per group
2048 inodes per group
Superblock backups stored on blocks:
	8193, 24577, 40961, 57345, 73729

Allocating group tables: done
Writing inode tables: done
Creating journal (4096 blocks): done
Writing superblocks and filesystem accounting information: done
<strong>#</strong> <kbd>mount /dev/sda1 /boot</kbd>
</pre>

&nbsp;

**WARNING:** /dev/sda1 is system dependant, that is the disk partition I have
used for /boot on my system. Make sure you format the correct partition
(device node) for your system configuration. (mkfs out put may also be
different on your system)

**IMPORTANT:** Make sure you change the /etc/fstab so it mounts /boot as ext4.

Now you can copy the kernel files to the new /boot partition from the backup
we made earlier.

<pre class="console">
<strong>#</strong> <kbd>cp -v /tmp/boot-backup/* /boot</kbd>
‘/tmp/boot-backup/initramfs-linux-fallback.img’ -> ‘/boot/initramfs-linux-fallback.img’
‘/tmp/boot-backup/initramfs-linux.img’ -> ‘/boot/initramfs-linux.img’
‘/tmp/boot-backup/vmlinuz-linux’ -> ‘/boot/vmlinuz-linux’
</pre>

&nbsp;

### Install & configure Syslinux

<pre class="console">
<strong>#</strong> <kbd>pacman -S syslinux</kbd>
<em>--- output not shown here ---</em>
</pre>

&nbsp;

At end of the package installation it shows us the instruction to automate
the configuration process, but I'm choosing to do it manually just to have
more fun.

Following commands will initialize the Syslinux configuration and install the
Syslinux MBR to your disk. (Again be aware that device node names are system
dependant).

<pre class="console">
<strong>#</strong> <kbd>extlinux -i /boot/syslinux/</kbd>
/boot/syslinux/ is device /dev/sda1
<strong>#</strong> <kbd>dd if=/usr/lib/syslinux/mbr.bin of=/dev/sda bs=440 count=1</kbd>
1+0 records in
1+0 records out
440 bytes (440 B) copied, 6.3689e-05 s, 6.9 MB/s
</pre>

&nbsp;

We are almost ready to reboot our system using Syslinux. But before you do
make sure you have correct Kernel(s) and parameters specifiled in the
/boot/syslinux/syslinux.cfg

Here is a simplest sample you need.

```
DEFAULT arch
PROMPT 0
TIMEOUT 50

LABEL arch
	MENU LABEL Arch Linux
	LINUX ../vmlinuz-linux
	APPEND root=/dev/sda6 ro
	INITRD ../initramfs-linux.img
```

&nbsp;

### Wipe out GRUB (optional)

Now since we no longer use GRUB (legacy), it can be removed from the system
to make things cleaner. You may keep it if you want to switch back to it in
later time, or in case if you need to install GRUB on another disk mounted to
this system.

<pre class="console">
<strong>#</strong> <kbd>pacman -Rcnsu grub</kbd>
<em>--- output not shown here ---</em>
</pre>
