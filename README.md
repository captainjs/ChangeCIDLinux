# Change CID Linux is a modified version of another git repository of Raburton called evoplus_cid:
Source:
https://github.com/raburton/evoplus_cid

That project was compiled for Android and requires rooted Android device.
This project was modified to work under Linux.

The following is a modified Readme based on the original work quoted above. It is a Tool to change the CID on Samsung Evo Plus SD Cards from Linux. 

Precompiled Linux binary not included. It works on regular Linux, tested using a real sd controller, not a usb mass storage type sd reader.

See http://richard.burtons.org/2016/07/01/changing-the-cid-on-an-sd-card/
for more details.

**USE AT YOU OWN RISK!**

## Prerequisites:

* A working Linux. I tested using a live usb stick of Ubuntu 21.10.
* Installing "gcc" to compile the code: sudo apt install gcc
* A computer with SD card reader, I tested on an old Dell Latitude E6430.
* A SD adapter to fit the micro SD card
* A 32GB Micro SD card, Samsung Evo Plus SD, older than 2016. Note: Apparently, newer versions have a vulnerability patched, the one that was allowing to change the CID. It is possible that it works for other cards. There is a lot of information spread on several websites, refer to Raburton's website, the url is shared above.

## Compile

`gcc evoplus_cid.c -o evoplus_cid`

If done properly, there should not be any compilation warnings.


## Usage:
```
./evoplus_cid <device> <cid> [serial]
device - sd card block device e.g. /dev/block/mmcblk1
cid - new cid, must be in hex (without 0x prefix)
  it can be 32 chars with checksum or 30 chars without, it will
  be updated with new serial number if supplied, the checksum is
  (re)calculated if not supplied or new serial applied
serial - optional, can be hex (0x prefixed) or decimal
  and will be applied to the supplied cid before writing
```

Based on the reverse engineering and code of Sean Beaupre,
see: https://github.com/beaups/SamsungCID

## Operation instructions:

These instructions are high level and expect a bit of know-how. 
* From the ubuntu live usb, insert the SD adapter containing the Micro SD card.
* Find the mount point. Remember the prerequisite of having a SD card reader:
find /sys -name cid -print
It should return a very long output, looking a bit similar to: "/sys/devices/pci0000:00/0000:00:04.0/....". 
Copy that entire line.
* View existing card's CID: more /sys/devices/pci0000:00/0000:00:04.0/...cid
It's good practice to copy that somewhere, in case there is a need to revert the card CID (which is not needed in our scenario).
* Find the card mount point:
mount | grep mmc
That command should return the mounted path for the SD card, for example:
/dev/mmcblk0p1
Note: if any other type of adapter was used, like USB, or even a SD card read on a newer computer, the SD card might appear as /dev/sdax, it probably won't work. Also, the device information required is not the full information, we won't use the ending (p1).
* At this stage, it should be ready to run the command to change the cid, using the relevant information:

sudo ./evoplus_cid /dev/mmcblk0 0941504d494253540219c2a601012300

The CID used above is an example of CID for a SD card for Discover media MIB2 (VW Touran II  2016-), as found online and tested.

* Verify: Unmount the SD card, reconnect it, and check that the CID was properly changed. The instructions to find the cid and view it are above.
At this point the CID should be the new one we indicated above, like 09415... 

Either git clone this repository or download the zip file in a specific folder. Once downloaded extract, and compile the code. Then it should be ready to use.

