<b> It's under costruction </b>

---

# linux arch installation flow

----

### A good reference:

1 - [official arc docs](https://wiki.archlinux.org/title/Installation_guide)<br>
2 - [youtube](https://www.youtube.com/watch?v=RsrPrA8NJHk)<br>
3 - [Stack Exchange Network](https://askubuntu.com/questions/726972/dual-boot-windows-10-and-linux-ubuntu-on-separate-hard-drives)<br>

---

- download arch iso linux:<br>
  [archlinux official downloads](https://archlinux.org/download/) > select "Magnet link"
  
- download rufus:<br>
  [rufus official downloads](https://rufus.ie/it/)
  <br>  
  - create an <i>iso bootable</i> usb drive with arch iso image
  - raccommended: check your bios is an uefi:
    - in bios (better) find it into the options
    - in [windows](https://kb.parallels.com/115815#:~:text=Click%20the%20Search%20icon%20on,of%20BIOS%2C%20Legacy%20or%20UEFI): find "system information" and "BIOS"
  - [raccommended option](https://blog.htbaa.com/wp-content/uploads/2013/11/rufus.png): GPT UEFI, MBR, FAT32, 8192byte, and load iso of arch.
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
