# Flashing Asus 2008 PIKE to IT Mode

[Source](https://gist.github.com/pjobson/9ec25f7fc991f28d132ca813ab1bd541)

Used on an Asus Z8PE-D18 board with no EFI boot options.  These instructions were written using Linux Mint to create the media, most distributions will work with little modification.

The PIKE 2008 is basically a LSI 9220-8i which you can flash with 9211-8i firmware.  Flashing to IT mode allows you to have direct access to the disks to use `btrfs` or `zfs` or some kind of software RAID instead of the card's RAID.

## Get Your SAS Address

There is a sticker on the back of your PIKE card which has 16 digits starting with `5000`.  Write this address down or take a picture of it.  Note I put `XXXXXXXXXXXX` in this picture as these numbers are unique to the card.  If your card does not have this sticker, instructions will be provided below.

![SAS Address](https://gist.githubusercontent.com/pjobson/9ec25f7fc991f28d132ca813ab1bd541/raw/f840edcd5ff16b78adb359ca7fecbbcc1859a61e/zPIKE_2008.jpg)

## Download FreeDOS

    wget http://www.freedos.org/download/download/FD12FULL.zip

### Unzip It

    unzip FD12FULL.zip

## USB

### Insert and Find Your USB Stick

This will show a list of your drives, be sure to use the correct one.  I've put `/dev/xxx` in the instructions as the USB, yours will be different.

    fdisk -l

It'll show something like this for your USB stick, note the drive size.

    Disk /dev/xxx: 28.9 GiB, 30992891904 bytes, 60532992 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0xd06a3fac

### Unmount your USB

    sudo umount /dev/xxx*

### Write FreeDOS to USB

    sudo dd if=FD12FULL.img of=/dev/xxx

### Add Extended & Logical Partitions to Your USB

    sudo fdisk /dev/xxx

#### Print your partition table.

    Command (m for help): p

#### Should show something like this.

    Disk /dev/xxx: 28.9 GiB, 30992891904 bytes, 60532992 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0xd06a3fac

    Device     Boot Start     End Sectors   Size Id Type
    /dev/xxx1  *       63 1048319 1048257 511.9M  6 FAT16

#### Create an Extended Partition

    Command (m for help): n
    Partition type
       p   primary (1 primary, 0 extended, 3 free)
       e   extended (container for logical partitions)
    Select (default p): e
    Partition number (2-4, default 2): 2
    First sector (1048320-60532991, default 1048576): 1048576
    Last sector, +sectors or +size{K,M,G,T,P} (1048576-60532991, default 60532991): +512M

#### Add a Logical Partition

    Command (m for help): n
    Partition type
       p   primary (1 primary, 1 extended, 2 free)
       l   logical (numbered from 5)
    Select (default p): l

    Adding logical partition 5
    First sector (1050624-2097151, default 1050624): 1050624
    Last sector, +sectors or +size{K,M,G,T,P} (1050624-2097151, default 2097151): 2097151

#### Change The Partition Type to FAT16.

    Command (m for help): t
    Partition number (1,2,5, default 5): 5
    Partition type (type L to list all types): 6

#### Print Your Table - Should display something like this:

    Command (m for help): p
    Disk /dev/xxx: 28.9 GiB, 30992891904 bytes, 60532992 sectors
    Units: sectors of 1 * 512 = 512 bytes
    Sector size (logical/physical): 512 bytes / 512 bytes
    I/O size (minimum/optimal): 512 bytes / 512 bytes
    Disklabel type: dos
    Disk identifier: 0xd06a3fac

    Device     Boot   Start     End Sectors   Size Id Type
    /dev/xxx1  *         63 1048319 1048257 511.9M  6 FAT16
    /dev/xxx2       1048576 2097151 1048576   512M  5 Extended
    /dev/xxx5       1050624 2097151 1046528   511M  6 FAT16

#### Write Your Partition Table

    Command (m for help): w
    The partition table has been altered.
    Calling ioctl() to re-read partition table.
    Syncing disks.

This will drop you back to the `bash` shell.

### Format The Partition

    sudo mkfs.fat /dev/xxx5

### Label Your Partition

    sudo fatlabel /dev/xxx5 SAS

### Re-Mount USB

The most convenient way to do this is unplug it and plug it back in.

## SAS Flash

### Download and Unzip SAS Flash Files

    wget https://gist.github.com/pjobson/9ec25f7fc991f28d132ca813ab1bd541/raw/4468546bfaa499d05a9f244cbcce6a200b1b62e0/sas_flash_files.zip
    unzip sas_flash_files.zip

### Copy Flash Files to USB

    cp megarec.exe /media/_your_user_name_/SAS/
    cp sas2flsh.exe /media/_your_user_name_/SAS/
    cp 2118it.bin /media/_your_user_name_/SAS/
    cp mptsas2.rom /media/_your_user_name_/SAS/
    cp dos4gw.exe /media/_your_user_name_/SAS/
    cp sbrempty.bin /media/_your_user_name_/SAS/

### Disconnect All Drives and Reboot from the USB

You'll want to unplug all of your SAS and SATA drives and reboot with the USB only.  Remove any additional SAS cards if you have any.

### FreeDOS Shell

Let FreeDOS boot. Then Select:

* `Install to harddisk`
* `English`
* `No - Return to DOS`

### Go To Your D: Drive

    D:
    dir

You should see the exe files and rom files.

### Get Your SAS Address

If you do not have the sticker as shown in Step 1, you can use `sas2flsh` to get the address.  Otherwise, you can skip this step.

    sas2flsh.exe -c 0 -list

Should display something like this:

    Adapter Selected is a LSI SAS: SAS2008(B2)

    Controller Number  : 0
    Controller  : SAS2008(B2)
    PCI Address  : 00:01:00:00
    SAS Address  : 5000xxx-x-xxxx-xxxx
    NVDATA Version (Default)  : 14.01.00.08
    NVDATA Version (Persistent)  : 14.01.00.08
    Firmware Product ID  : 0x2213 (IT)
    Firmware Version  : 20.00.07.00
    NVDATA Vendor  : LSI
    NVDATA Product ID  : SAS9211-8i
    BIOS Version  : N/A
    UEFI BSD Version  : N/A
    FCODE Version  : N/A
    Board Name  : SAS9211-8i
    Board Assembly  : N/A
    Board Tracer Number  : N/A

    Finished Processing Commands Successfully.
    Exiting SAS2Flash.

  Note the `SAS Address` this is what you need without the dashes, don't loose it.

### Back-Up Your Card

    megarec.exe -readsbr 0 pike2008.sbr

### Wipe Your Card

    megarec.exe -writesbr 0 sbrempty.bin
    megarec.exe -cleanflash 0

### Reboot

You will need to reboot here.

### Back to D:

As shown above.

### Flash IT Mode

    sas2flsh.exe -o -f 2118it.bin -b mptsas2.rom

### Restore Your SAS Address

Replace `5000xxxxxxxxxxxx` with the one you hopefully wrote down.

     sas2flsh.exe -o -sasadd 5000xxxxxxxxxxxx

### List Card

    sas2flsh.exe -listall

This should show your card and the firmware which you just flashed.

## Additional Info: PIKE Card Chipset and Motherboard Reference

Here is a reference for chipsets and motherboard support for various PIKE cards.  Check out the [LSI RAID Controller and HBA Complete Listing Plus OEM Models](https://forums.servethehome.com/index.php?threads/lsi-raid-controller-and-hba-complete-listing-plus-oem-models.599/) thread on ServeTheHome for more on RAID cards and flashing options.

* [PIKE 1064E](https://www.asus.com/Commercial-Servers-Workstations/PIKE_1064E/) → LSI SAS 1064E
	* [Z8PE-D18](https://www.asus.com/Commercial-Servers-Workstations/Z8PED18/)
	* [Z8NR-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8NRD12/)
	* [Z8NA-D6](https://www.asus.com/Commercial-Servers-Workstations/Z8NAD6/)
	* [P7F-E](https://www.asus.com/Commercial-Servers-Workstations/P7FE/)
	* [DSAN-DX](https://www.asus.com/us/Commercial-Servers-Workstations/DSANDX/)
	* [KGPE-D16](https://www.asus.com/Commercial-Servers-Workstations/KGPED16/)
	* [KFSN5-D/IST](https://www.asus.com/Commercial-Servers-Workstations/KFSN5DIST/)
* [PIKE 1068E](https://www.asus.com/Commercial-Servers-Workstations/PIKE_1068E/) → LSI SAS 1068E
	* [Z8PH-D12 SE/QDR](https://www.asus.com/Commercial-Servers-Workstations/Z8PHD12_SEQDR/)
	* [Z8PE-D18](https://www.asus.com/Commercial-Servers-Workstations/Z8PED18/)
	* [Z8PE-D12X](https://www.asus.com/Commercial-Servers-Workstations/Z8PED12X/)
	* [Z8PE-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8PED12/)
	* [Z8NR-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8NRD12/)
	* [Z8NA-D6](https://www.asus.com/Commercial-Servers-Workstations/Z8NAD6/)
	* [P7F-E](https://www.asus.com/Commercial-Servers-Workstations/P7FE/)
	* [DSAN-DX](https://www.asus.com/us/Commercial-Servers-Workstations/DSANDX/)
	* [KGPE-D16](https://www.asus.com/Commercial-Servers-Workstations/KGPED16/)
* [PIKE 1078](https://www.asus.com/Commercial-Servers-Workstations/PIKE_1078/) → LSI SAS 1078
	* [Z8PH-D12 SE/QDR](https://www.asus.com/Commercial-Servers-Workstations/Z8PHD12_SEQDR/)
	* [Z8PE-D18](https://www.asus.com/Commercial-Servers-Workstations/Z8PED18/)
	* [Z8PE-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8PED12/)
	* [Z8PE-D12X](https://www.asus.com/Commercial-Servers-Workstations/Z8PED12X/)
	* [Z8NR-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8NRD12/)
	* [Z8NA-D6](https://www.asus.com/Commercial-Servers-Workstations/Z8NAD6/)
	* [P7F-E](https://www.asus.com/Commercial-Servers-Workstations/P7FE/)
	* [DSAN-DX](https://www.asus.com/us/Commercial-Servers-Workstations/DSANDX/)
	* [KGPE-D16](https://www.asus.com/Commercial-Servers-Workstations/KGPED16/)
	* [KFSN5-D/IST](https://www.asus.com/Commercial-Servers-Workstations/KFSN5DIST/)
* [PIKE 2008](https://www.asus.com/us/Commercial-Servers-Workstations/PIKE_2008/) → LSI SAS 2008
	* [Z8PH-D12 SE/QDR](https://www.asus.com/Commercial-Servers-Workstations/Z8PHD12_SEQDR/)
	* [Z8PH-D12/IFB](https://www.asus.com/Commercial-Servers-Workstations/Z8PHD12IFB/)
	* [Z8PE-D18](https://www.asus.com/Commercial-Servers-Workstations/Z8PED18/)
	* [Z8PE-D12X](https://www.asus.com/Commercial-Servers-Workstations/Z8PED12X/)
	* [Z8PE-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8PED12/)
	* [Z8NR-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8NRD12/)
	* [Z8NH-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8NHD12/)
	* [Z8NA-D6](https://www.asus.com/Commercial-Servers-Workstations/Z8NAD6/)
	* [P7F-E](https://www.asus.com/Commercial-Servers-Workstations/P7FE/)
	* [KGPE-D16](https://www.asus.com/us/Commercial-Servers-Workstations/KGPED16/)
* [PIKE 2108](https://www.asus.com/us/Commercial-Servers-Workstations/PIKE_2108/) → LSI SAS 2108
	* Intel P9 Series
	* Z9 Series
	* P8 Series
	* Z8 Series with PIKE slot
	* AMD KG Series
	* KC Series with PIKE slot
* [PIKE 2208](https://www.asus.com/us/Commercial-Servers-Workstations/PIKE_2208/) → LSI SAS 2208
	* Intel P9 Series
	* Z9 Series
	* P8 Series
	* Z8 Series with PIKE slot
	* AMD KG Series
	* KC Series with PIKE slot
* [PIKE 2308](https://www.asus.com/us/Commercial-Servers-Workstations/PIKE_2308/) → LSI SAS 2308
	* Intel P9 Series
	* Z9 Series
	* P8 Series
	* Z8 Series with PIKE slot
	* AMD KG Series
	* KC Series with PIKE slot
* [PIKE 6480](https://www.asus.com/Commercial-Servers-Workstations/PIKE_6480/) → Marvell 88SE6480
	* [Z8PE-D18](https://www.asus.com/Commercial-Servers-Workstations/Z8PED18/)
	* [Z8PE-D12X](https://www.asus.com/Commercial-Servers-Workstations/Z8PED12X/)
	* [Z8PE-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8PED12/)
	* [Z8NR-D12](https://www.asus.com/Commercial-Servers-Workstations/Z8NRD12/)
	* [Z8NA-D6](https://www.asus.com/Commercial-Servers-Workstations/Z8NAD6/)
	* [P7F-E](https://www.asus.com/Commercial-Servers-Workstations/P7FE/)
	* [DSAN-DX](https://www.asus.com/us/Commercial-Servers-Workstations/DSANDX/)
	* [KGPE-D16](https://www.asus.com/Commercial-Servers-Workstations/KGPED16/)
* [PIKE 9230](https://www.asus.com/Commercial-Servers-Workstations/PIKE_9230/) → Marvell 88SE9230
	* Intel P9 Series
	* Z9 Series
	* P8 Series
	* Z8 Series with PIKE slot
	* AMD KG Series
	* KC Series with PIKE slot
* [PIKE II 3008-8i](https://www.asus.com/us/Commercial-Servers-Workstations/PIKE_II_30088i/) → Broadcom (LSI) SAS3008
	* [ESC4000 G3](https://www.asus.com/Commercial-Servers-Workstations/ESC4000_G3/)
	* [ESC4000 G3S](https://www.asus.com/Commercial-Servers-Workstations/ESC4000_G3S/)
	* [ESC8000 G3](https://www.asus.com/us/Commercial-Servers-Workstations/ESC8000_G3/)
	* [P9A-I](https://www.asus.com/us/Commercial-Servers-Workstations/P9AIC2750SAS4L/)
	* [P9D-C/4L](https://www.asus.com/us/Commercial-Servers-Workstations/P9DC4L/)
	* [P9D-E/4L](https://www.asus.com/Commercial-Servers-Workstations/P9DE4L/)
	* [P9D-I](https://www.asus.com/us/Commercial-Servers-Workstations/P9DI/)
	* P9D-IV
	* [P9D-M](https://www.asus.com/Commercial-Servers-Workstations/P9DM/)
	* [P9D-MH](https://www.asus.com/us/Commercial-Servers-Workstations/P9DMHSAS10GDUAL/)
	* [P9D-MV](https://www.asus.com/Commercial-Servers-Workstations/P9DMV/)
	* [P9D-V](https://www.asus.com/us/Commercial-Servers-Workstations/P9DV/)
	* [P9D-X](https://www.asus.com/Commercial-Servers-Workstations/P9DX/)
	* [RS500-E8](https://www.asus.com/Commercial-Servers-Workstations/RS500E8PS4/)
	* [RS520-E8](https://www.asus.com/Commercial-Servers-Workstations/RS520E8RS8/)
	* [RS700-E7](https://www.asus.com/us/Commercial-Servers-Workstations/RS700E7RS8/)
	* [RS700-E8](https://www.asus.com/us/Commercial-Servers-Workstations/RS700E7RS8/)
	* [RS720-E7/RS12](https://www.asus.com/Commercial-Servers-Workstations/RS720E7RS12/)
	* [RS720-E7/RS24-EG](https://www.asus.com/me-en/Commercial-Servers-Workstations/RS720E7RS24EG/)
	* [RS720-E8-RS24-E](https://www.asus.com/Commercial-Servers-Workstations/RS720E8RS24E/)
	* [RS720Q-E7/RS12](https://www.asus.com/Commercial-Servers-Workstations/RS720QE7RS12/)
	* [RS720Q-E8-RS12](https://www.asus.com/us/Commercial-Servers-Workstations/RS720QE8RS12/)
	* [TS500-E8-PS4](https://www.asus.com/Commercial-Servers-Workstations/TS500-E8-PS4-V2/)
	* [TS700-E7/RS8](https://www.asus.com/us/Commercial-Servers-Workstations/TS700E7RS8/)
	* [TS700-E8](https://www.asus.com/us/Commercial-Servers-Workstations/TS700-E8-RS8-V2/)
	* [TS700-X7/PS4](https://www.asus.com/us/Commercial-Servers-Workstations/TS700X7PS4/)
	* [X99-E WS](https://www.asus.com/Motherboards/X99E_WS/)
	* [Z10PA-D8](https://www.asus.com/us/Commercial-Servers-Workstations/Z10PAD8/)
	* [Z10PA-U8](https://www.asus.com/Commercial-Servers-Workstations/Z10PAU8/)
	* [Z10PE-D16](https://www.asus.com/us/Commercial-Servers-Workstations/Z10PED16/)
	* [Z10PE-D16 WS](https://www.asus.com/us/Motherboards/Z10PED16_WS/)
	* [Z10PE-D8 WS](https://www.asus.com/us/Motherboards/Z10PED8_WS/)
	* [Z10PH-D16](https://www.asus.com/us/Commercial-Servers-Workstations/Z10PHD16/)
	* [Z10PR-D16](https://www.asus.com/Commercial-Servers-Workstations/Z10PRD16/)
	* [Z9NA-D6](https://www.asus.com/us/Commercial-Servers-Workstations/Z9NAD6/)
	* [Z9NH-D12](https://www.asus.com/Commercial-Servers-Workstations/Z9NHD12/)
	* [Z9NR-D12](https://www.asus.com/Commercial-Servers-Workstations/Z9NRD12/)
	* [Z9PA-D8](https://www.asus.com/us/Commercial-Servers-Workstations/Z9PAD8/)
	* [Z9PA-U8](https://www.asus.com/Commercial-Servers-Workstations/Z9PAU8/)
	* [Z9PE-D16](https://www.asus.com/Commercial-Servers-Workstations/Z9PED16/)
	* [Z9PE-D16-10G/DUAL](https://www.asus.com/me-en/Commercial-Servers-Workstations/Z9PED1610GDUAL/)
	* [Z9PE-D8 WS](https://www.asus.com/Motherboards/Z9PED8_WS/)
	* [Z9PH-D16](https://www.asus.com/us/Commercial-Servers-Workstations/Z9PHD16/)
	* [Z9PR-D12](https://www.asus.com/us/Commercial-Servers-Workstations/Z9PRD12/)
	* [Z9PR-D16](https://www.asus.com/Commercial-Servers-Workstations/Z9PRD16/)
* [PIKE II 3108-8i/16PD](https://www.asus.com/us/Commercial-Servers-Workstations/PIKE_II_31088i16PD/) → Broadcom (LSI) SAS3108
	* This is really just an LSI RAID card with two internal Mini-SAS connectors.
	* I do not know if it works on non-Asus motherboards.
* [PIKE II 3108-8i/16PD/2G](https://www.asus.com/Commercial-Servers-Workstations/PIKE-II-3108-8I-16PD-2G/) → Broadcom (LSI) SAS3108
	* This is really just an LSI RAID card with two internal Mini-SAS connectors.
	* I do not know if it works on non-Asus motherboards.
* [PIKE II 3108-8i/240PD](https://www.asus.com/us/Commercial-Servers-Workstations/PIKE_II_31088i240PD/) → Broadcom (LSI) SAS3108
	* This is really just an LSI RAID card with two internal Mini-SAS connectors.
	* I do not know if it works on non-Asus motherboards.
* [PIKE II 3108-8i/240PD/2G](https://www.asus.com/Commercial-Servers-Workstations/PIKE-II-3108-8I-240PD-2G/) → Broadcom (LSI) SAS3108
	* This is really just an LSI RAID card with two internal Mini-SAS connectors.
	* I do not know if it works on non-Asus motherboards.
