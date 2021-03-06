# Arch-Install

Installation on my Huawei Matebook X Pro (512 GB storage, 16 GB RAM, Nvidia MX150), Dual Boot with Windows10.

## Dual boot with Windows10
(Feel free to skip this step if you don't want dual-boot)

Wipe entire drive


## Increase the size of EFI partition
Boot into your Windows media creation tool.
Then click "Custom installation"


1. Select your installation target and make sure it has no partitions (except unallocated space)
2. Click the ```New``` and then the ```Apply``` button.
You should now have four partitions: Recovery, System (ESP), MSR, and Primary.

3. Select each of the System, MSR, and Primary partitions in turn and click the Delete button to delete these partitions. Leave the Recovery partition in place.
4. Press ```Shift+F10``` to open the Command Prompt
5. Type ```diskpart.exe``` and press ```Enter``` to open the disk partitioning tool
6. Type ```list disk``` and press ```Enter``` to list out your disks
7. Type ```select disk n``` where n is the number for the disk you want to install to as identified by the above command and press Enter
8. Type ```create partition efi size=600``` where 600 is the desired size of the ESP in Megabytes (MiB), and press Enter
9. Type ```format quick fs=fat32 label=System``` and press ```Enter``` to format the ESP
10. Type ```exit``` and press ```Enter``` to exit the disk partitioning tool
11. Type ```exit``` and press ```Enter``` again to exit the Command Prompt

You should now be back in the graphical Windows Setup partitioning tool where nothing has changed since the last time you looked at it.

Click the Refresh button to detect your partition changes
You should now have a disk with a default Windows Recovery tools partition, a 600 MiB UEFI System Partition, and some unallocated space for your Windows installation.

Select the unallocated space from the disk list and click the New button to automatically recreate the MSR and System partition in the remaining space

From here you can continue your installation as normal.

**NOTE:** This list is copied from ([source](https://www.ctrl.blog/entry/how-to-esp-windows-setup.html))


->Allow the Windows installation to finish, and then install all drivers required. This may take some time.


## Make partitions
Using the program GParted I resized the disk into several partitions (in addition to those Windows already has made)
Ensure that they are formatted into format **.ext4**

* Home partition (140gb)
* Arch Partition (100gb)
* Swap Partition (20gb)

(+ I also have one partition for Ubuntu)


## Make a bootable USB Key with Arch
[Arch ISO](https://www.archlinux.org/download/)

Use a program such as Rufus (for Windows) to burn the ISO to a USB stick.



#------------- In progress -------------#

Boot into USB-Key

Mounting disks and swap

```setfont latarcyrheb-sun32```

use ```wifi-menu``` to get online
```# timedatectl set-ntp true```

```# mkswap /dev/path/to/partition```

```# mount /dev/path/to /mnt```

```# mkdir /mnt/home```

```# mount /dev/path/home /mnt/home```

```# swapon /dev/path/to```

```# mkdir /mnt/boot```

```# mount /dev/nvme0n1p1 /mnt/bootc```


```# pacstrap /mnt base base-devel```

```# genfstab -U /mnt >> /mnt/etc/fstab```


[Audio Fix](https://aymanbagabas.com/2018/07/23/archlinux-on-matebook-x-pro.html)
