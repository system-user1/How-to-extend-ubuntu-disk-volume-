# How-to-extend-ubuntu-disk-volume

https://packetpushers.net/ubuntu-extend-your-default-lvm-space/

Use Your Default Free Space

As you can see above: the Ubuntu installer (by default) left almost half of my disk space unusable by the root file system! I’ve looked around to find an explanation on why these are the default settings, but can’t find anything. Before extending your underlying hypervisor disk or storage volume, you may want to see if you have free space available and ready to be used to extend your existing file system. If you used the Ubuntu defaults during installation, then there is a good chance you have this free space.

## STEP 1
To use up that free space on your Volume Group (VG) for your root Logical Volume (LV), first run the __*lvdisplay*__ command and check the Logical Volume size, then run __*lvextend -l +100%FREE /dev/ubuntu-vg/ubuntu-lv*__ to extend the LV to the maximum size usable, then run __*lvdisplay*__ one more time to make sure it changed.
![대체 텍스트(alternative text)](https://packetpushers.net/wp-content/uploads/2021/11/screen3-590x557.png "extend the block volume")

## STEP 2
At this point you have increased the size of the block volume where your root filesystem resides, but you still need to extend the filesystem on top of it. First, __*run df -h*__ to verify your (almost full) root file system, then run __*resize2fs /dev/mapper/ubuntu--vg-ubuntu--lv*__ to extend your filesystem, and run __*df -h*__ one more time to make sure you’re successful.
