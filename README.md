# Change CID Linux is a modified version of another git repository of Raburton called evoplus_cid:
https://github.com/raburton/evoplus_cid
That project was compiled for Android and requires rooted Android device.
This project was modified to work under Linux.

The following is a modified Readme based on the original work quoted above. It is a Tool to change the CID on Samsung Evo Plus SD Cards from Linux. 

Precompiled Linux binary not included. It works on regular Linux, tested using a real sd controller, not a usb mass storage type sd reader.

See http://richard.burtons.org/2016/07/01/changing-the-cid-on-an-sd-card/
for more details.

**USE AT YOU OWN RISK!**

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

## Compile

`gcc evoplus_cid.c -o evoplus_cid`

You can safely ignore compilation warnings.
