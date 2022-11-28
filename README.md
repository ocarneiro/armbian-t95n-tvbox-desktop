# armbian-t95n-tvbox-desktop
Armbian image for Amlogic S905x with graphical interface

## Download

Check the Releases (or tags) page: https://github.com/ocarneiro/armbian-t95n-tvbox-desktop/releases

## How it was made

### What do you need

 - armbian source code: https://github.com/armbian/build
 - a hypervisor (ex: VirtualBox)
 - a supported image (check armbian's basic requirements. I used Ubuntu Jammy 22.04 x64)
 - a working image that boots properly in your device (I used ophub's: https://github.com/ophub/amlogic-s9xxx-armbian).

### Step by step

1. Create your virtual machine and build your own armbian image from source (I'll call this IMG1);
1. Create 2 virtual disks with 4GB each in VirtualBox;
1. Burn IMG1 into one of these disks.  

    E.g.: dd if=IMG1.img of=/dev/sdb   \
    (don't fool around with dd, understand what it does or don't use it!)
    
1. Get your working image (I used Armbian_22.11.0_Aml_s905x_bullseye_5.15.79_server_2022.11.21.img.gz from ophub) and burn it into one of your virtual disks.
  
    Example: dd if=IMG2.img of=/dev/sdc   \
    (don't do it! use proper configuration based on your setup)

dd on IMG1 will produce two partitions, one for u-boot and one for the Operating System itself. E.g.: /dev/sdb1 and /dev/sdb2

dd on IMG2 will produce one partition, e.g. /dev/sdc1

1. Now copy the partition from IMG2 over the second partition from IMG1. E.g.: dd if=/dev/sdc1 of=/dev/sdb2

1. Get the UUID from the partition from IMG2 (should be the same in /dev/sdc1 and /dev/sdb2):

    lsblk -f

1. Copy this UUID into the uEnv.txt file in the first partition of IMG1. It would be in the partition /dev/sdb1 in this example.

1. Burn the first disk (the one with the two partitions) into an image (like the one I made) or directly into your microsd (or TF) card.

    E.g. dd if=/dev/sdb of=IMG3.img  # don't do it like this, check your setup!

1. Insert the card into your TVBox and turn it on!



