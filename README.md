<b> It's under costruction </b>

---

# linux arch installation flow

----

### A good reference:

1 - [official arc docs](https://wiki.archlinux.org/title/Installation_guide)<br>
2 - [youtube](https://www.youtube.com/watch?v=RsrPrA8NJHk) / [youtube](https://www.youtube.com/watch?v=sm_fuBeaOqE) / [youtube](https://www.youtube.com/watch?v=JRdYSGh-g3s)<br>
3 - [Stack Exchange Network](https://askubuntu.com/questions/726972/dual-boot-windows-10-and-linux-ubuntu-on-separate-hard-drives)<br>

---

- download arch iso linux:<br>
  [archlinux official downloads](https://archlinux.org/download/) > select "Magnet link"
  
- download rufus:<br>
  [rufus official downloads](https://rufus.ie/it/) and starto to create an <i>iso bootable</i> usb drive with arch iso image
  - raccommended: check your bios is an uefi:
    ...in bios you can find it in the options
    ...in windows: win+R and write "msinfo32" and "BIOS" (or BIOS mode)
  - [raccommended option](https://blog.htbaa.com/wp-content/uploads/2013/11/rufus.png): GPT, UEFI, FAT32, 8192byte, and load iso of arch.
  <br>

- Test connection:<br>

  `$ ping archlinux.org`<br>

  If not working:<br>

  (Check if exist a wlan)<br>
  `$ ip a`

  (if exist...)<br>
  `$ Iwtcl`

  First, if you do not know your wireless device name, list all Wi-Fi devices:

  `[iwd]# device list`

  Then, to initiate a scan for networks (note that this command will not output anything):

  `[iwd]# station DEVICE scan`

  You can then list all available networks:

  `[iwd]# station DEVICE get-networks`

  Finally, to connect to a network:

  `[iwd]# station DEVICE connect SSID`


- Install on disk:

  `$cfdisk`

  Select gpt (it's for over 2t disks)

  Get 2G of SSD, set type: Linux Swap
  Get other of SSD, set type: Linux system

  Enter on [ write ]

  If you read "syncing disks" you're rady
