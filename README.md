<b> It's under costruction </b>

---

# linux arch installation flow

### A good reference:

1 - [official arc docs](https://wiki.archlinux.org/title/Installation_guide)<br>
2 - [youtube](https://www.youtube.com/watch?v=RsrPrA8NJHk) / [youtube](https://www.youtube.com/watch?v=LGhifbn6088&t=309s) / [youtube](https://www.youtube.com/watch?v=C3D_qzw94v8) / [youtube](https://www.youtube.com/watch?v=sm_fuBeaOqE) / [youtube](https://www.youtube.com/watch?v=JRdYSGh-g3s)<br>
3 - [Stack Exchange Network](https://askubuntu.com/questions/726972/dual-boot-windows-10-and-linux-ubuntu-on-separate-hard-drives)<br>

---
<br> <b>[STEP:1/3]</b>

- download arch iso linux:<br>
  [archlinux official downloads](https://archlinux.org/download/) > select "Magnet link"<br>
 
- download rufus:<br>
  [rufus official downloads](https://rufus.ie/it/) and starto to create an <i>iso bootable</i> usb drive with arch iso image
  - raccommended: check your bios is an uefi:<br>
  ⠀...in bios you can find it in the options<br>
  ⠀...in windows: win+R and write "msinfo32" and "BIOS" (or BIOS mode), check if "secure boot" is off or set it via bitlocker<br>
  - [raccommended option](https://blog.htbaa.com/wp-content/uploads/2013/11/rufus.png): MBR, FAT32, 8192byte, and load iso of arch.<br>

- no second drive? need a partition:
  - via linux terminal [(this link)](https://phoenixnap.com/kb/linux-create-partition)
  - in windows:<br>
    - win+r and write "diskmgmt.msc"
    - right click on NFTS window partition and shrink it with min 6GB for linux<br>
    <small><i>warning, if you not an expert see on youtube before this action!</i></small><br>

- restart and boot way:<br>
  a) go to bios and load arch from usb (or set it first boot)<br>
  b) via windows:<br>
 ⠀⠀⠀1) open win menu and find "startup"<br>
 ⠀⠀⠀2) open "advanced sturtup recovery" (ITA:modifica le opzioni di avvio avanzato)<br>
 ⠀⠀⠀3) click on "advanced sturtup" > "use a device" > select your bootable arch usb<br>

<br> <b>[STEP:2/3]</b>

- Set Keyboard Layout:<br>

    `$ loadkeys it` (or other lang)<br>

- Set time date:<br>

    `$ timedatectl set-ntp true`<br>

- Test connection:<br>

  `$ ping archlinux.org`<br>

   ...If not working:<br>
      └ Check if exist a wlan : `$ ip a`<br>
        └ if exist: `$ iwctl` and...<br>
        ⠀⠀⠀1) First, if you do not know your wireless device name, list all Wi-Fi devices:<br>
        ⠀⠀⠀⠀`[iwd]# device list`<br>
        ⠀⠀⠀2) Then, to initiate a scan for networks (note that this command will not output anything):<br>
        ⠀⠀⠀⠀`[iwd]# station DEVICE scan`<br>
        ⠀⠀⠀3)⠀You can then list all available networks:<br>
        ⠀⠀⠀⠀`[iwd]# station DEVICE get-networks`<br>
        ⠀⠀⠀4)⠀Finally (or direct if you know params), to connect to a network:<br>
        ⠀⠀⠀⠀`[iwd]# station DEVICE connect SSID`<br>

- Install on disk (basic/obsoleted):

  `$ cfdisk` (another way is "parted" and "print")<br>

  ⠀...Select gpt (it's for over 2t disks)<br>
  ⠀...Get 2G of SSD, set type: Linux Swap<br>
  ⠀...Get other of SSD, set type: Linux system<br>

  Enter on [ write ]

  If you read "syncing disks" you're rady

<br> <b>[STEP:3/3]</b>

- from 2022 you can use a graphical installer (it's good):
  `$ archinstall`

   follow the instruction into installer and save your json profile ;)
   IMPORTANT NOTE: Always select more than one mirror to avoid potential crashes or update failures
