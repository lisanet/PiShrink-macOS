# PiShrink-macOS #
This is a port of PiShrink bash script for Linux to run under macOS.

PiShrink [https://github.com/Drewsif/PiShrink](https://github.com/Drewsif/PiShrink) is a bash script that automatically shrinks a pi image. This will make putting the image back onto the SD card faster and the shrunk images will compress better.

Besides the original script it uses a few utils for the ext2/3/4 filesystem. All of these tools can be easily build by running the provided helper scripts in this repository. For mor information see below.

## Usage ##
`pishrink imagefile.img [newimagefile.img]`

If you specify the `newimagefile.img` parameter, the script will make a copy of `imagefile.img` and work off that. You will need enough space to make a full copy of the image to use that option.

## Prerequisites ##
If you are trying to shrink a [NOOBS](https://github.com/raspberrypi/noobs) image it will likely fail. This is due to [NOOBS paritioning](https://github.com/raspberrypi/noobs/wiki/NOOBS-partitioning-explained) being significantly different than Raspberry Pi OS. 


## Installation ##
Since you are using a Raspberry Pi, I'm quite sure, that you've already installed the command line tools. If not, please do so.

Then clone the repo run make and sudo make install. Here are the corresponding commands:

```bash
git clone https://github.com/lisanet/PiShrink-macOS.git
cd PiShrink-macOS
make
sudo make install
```

## Example ##
```bash
>pishrink raspi.img 
Checking filesystem on partition 2 ...
e2fsck 1.46.5 (30-Dec-2021)
Pass 1: Checking inodes, blocks, and sizes
Pass 2: Checking directory structure
Pass 3: Checking directory connectivity
Pass 4: Checking reference counts
Pass 5: Checking group summary information
rootfs: 63484/1918208 files (0.3% non-contiguous), 836061/7725184 blocks
resize2fs 1.46.5 (30-Dec-2021)

Shrinking partition 2 starting at block 532480 on raspi.img...
resize2fs 1.46.5 (30-Dec-2021)
Resizing the filesystem on /dev/disk6s2 to 1054340 (4k) blocks.
Begin pass 2 (max = 403329)
Relocating blocks             XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Begin pass 3 (max = 236)
Scanning inode table          XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
Begin pass 4 (max = 7632)
Updating inode references     XXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX
The filesystem on /dev/disk6s2 is now 1054340 (4k) blocks long.

"disk6" ejected.

Updating partition table to new size ...
Enter 'help' for information
fdisk: 1>          Starting       Ending
 #: id  cyl  hd sec -  cyl  hd sec [     start -       size]
------------------------------------------------------------------------
 2: 83  128   0   1 -  143   3  16 [    532480 -   61801472] Linux files*
Partition id ('0' to disable)  [0 - FF]: [83] (? for help) Do you wish to edit in CHS mode? [n] Partition offset [0 - 62333952]: [532480] Partition size [1 - 61801472]: [61801472] fdisk:*1> Writing MBR at offset 0.
fdisk: 1> 

Shrunk raspi.img from 30G to 4,3G
```


