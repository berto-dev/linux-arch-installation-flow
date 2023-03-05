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
  [rufus official downloads](https://rufus.ie/it/) and start to create an <i>iso bootable</i> usb drive with arch iso image
  - raccommended: check your bios is an uefi:<br>
    ...in bios you can find it in the options<br>
    ...in windows: win+R and write "msinfo32" and "BIOS" (or BIOS mode), check if "secure boot" is off or set it via bitlocker<br>
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
     1) open win menu and find "startup"<br>
     2) open "advanced sturtup recovery" (ITA:modifica le opzioni di avvio avanzato)<br>
     3) click on "advanced sturtup" > "use a device" > select your bootable arch usb<br>

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
          1) First, if you do not know your wireless device name, list all Wi-Fi devices:<br>
          &nbsp;&nbsp;&nbsp;&nbsp;`[iwd]# device list`<br>
          2) Then, to initiate a scan for networks (note that this command will not output anything):<br>
          &nbsp;&nbsp;&nbsp;&nbsp;`[iwd]# station DEVICE scan`<br>
          3) You can then list all available networks:<br>
          &nbsp;&nbsp;&nbsp;&nbsp;`[iwd]# station DEVICE get-networks`<br>
          4) Finally (or direct if you know params), to connect to a network:<br>
          &nbsp;&nbsp;&nbsp;&nbsp;`[iwd]# station DEVICE connect SSID`<br>

<!--
- Install on disk (basic/obsoleted):

  `$ cfdisk`<br>

    ...Select gpt (it's for over 2t disks)<br>
    ...Get 2G of SSD, set type: Linux Swap<br>
    ...Get other of SSD, set type: Linux system<br>

  Enter on [ write ]

  If you read "syncing disks" you're ok, now set a boot:<br>
  `$ parted` > `$ print` > `$ add "N(number of partition)" "boot" "on"`

  <top><sub><i>NOTE: next step have better solution for make the partitions</i></sub></top>
-->

<br> <b>[STEP:3/3]</b>

- from 2022 you can use a graphical installer (it's good):<br>
  `$ archinstall`<br>

   follow the instruction into installer and save your json profile ;)<br>
   <top><sub>SUGGEST: <i>Always select more than one mirror to avoid potential crashes or update failures</i></sub></top><br>
   Exemple:<br>

    - set your lang everywhere... And UTF8 character sets
    - set disk to suggest layout and change ext4 in btrf, set it compressed (do not touch the boot partition)
    - set bootloader to grub
    - set your name host (the computer device name)
    - set a password and profile
    - set profile to minimal
    - set audio to pipewire
    - set kernel to zen
    - set net equal to iso configuration<br>
    
    Installation completed? Reboot<br>
    
    - Now update and reboot system:<br>
      `$ sudo pacman -Syu` <br>
      `$ sudo reboot`<br>

    - Use and prepare Packages <top><sub>(git/chrome/aur)</sub></top><br>

      - Make a folder for "Package"<br>
        `$ sudo mkdir -p ./Packages`<br>

      - install Git for cloning pro packages<br>
        `$ sudo pacman -S git`<br>

      - Use Aur for first time, exemple:<br>
        `$ sudo git clone https://aur.archlinux.org/google-chrome.git ./Packages/google-chrome`<br>
        `$ cd packages/google-chrome`<br>
        `$ makepkg -si`<br>

<br><hr><br>

### CUSTOMIZING & OPTIMIZATION (Gnome 4X.X)

<b>Set Autologin:</b><br>

`$ sudo nano /etc/gdm/custom.conf`<br>

Add into file:

```
[daemon]
AutomaticLoginEnable=True
AutomaticLogin=username
```

<br>

<b>Debloat packs:</b><br>

<top><sub><i>Note: Rscgn remove all dependencies (dangerous) of pack</i><br>

- `$ sudo pacman -Q` <top><sub><i>(for list) (use "| grep NAMEPACK" for detect it)</i></sub></top><br>
- `$ sudo pacman -Rsn gnome-contacts`<br>
- `$ sudo pacman -Rsn gnome-maps`<br>
- `$ sudo pacman -Rsn simple-scan`<br>
- `$ sudo pacman -Rsn gnome-music`<br>
- `$ sudo pacman -Rsn gnome-calendar`<br>
- `$ sudo pacman -Rsn gnome-photos` <top><sub><i>(photo albums)</i></sub></top><br> 
- `$ sudo pacman -Rsn totem` <top><sub><i>(video player)</i></sub></top><br> 
- `$ sudo pacman -rsn htop`<br>
- `$ sudo pacman -rsn vim`<br>
- Etc...

<br>

<b>Essentials extension:</b>

  - [Add to desktop](https://github.com/Tommimon/add-to-desktop)
  - [Arch update alert icon](https://github.com/RaphaelRochet/arch-update)
  - [Blur on lockscreen](https://github.com/PRATAP-KUMAR/control-blur-effect-on-lock-screen) (optional)
  - [Bluetooth battery indicator](https://github.com/MichalW/gnome-bluetooth-battery-indicator)
  - [Bluetooth quick connect](https://github.com/bjarosze/gnome-bluetooth-quick-connect)
  - [Blur my shell](https://github.com/aunetx/blur-my-shell)
  - [Burn My Windows](https://github.com/Schneegans/Burn-My-Windows)
  - [Compact quick settings](https://github.com/mariospr/compact-quick-settings-gnome-shell-extension) (optional)
  - [Compiz windows effect](https://github.com/hermes83/compiz-windows-effect)
  - [Clipboard Manager](https://github.com/b00f/gnome-clipboard)
  - [Desktop icons neo](https://github.com/DEM0NAssissan7/desktop-icons-neo)
  - [Day/night theme switcher](https://github.com/fthx/theme-switcher)
  - [Easy Screen Cast](https://github.com/EasyScreenCast/EasyScreenCast)
  - [Just perfection](https://gitlab.gnome.org/jrahmatzadeh/just-perfection)
  - [No titlebar when maximized](https://github.com/alecdotninja/no-titlebar-when-maximized) (optional)
  - [Removable drive in menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
  - [Settings center](https://github.com/ChrisLauinger77/XES-Settings-Center-Extension)
  - [Top bar organizer](https://gitlab.gnome.org/julianschacher/top-bar-organizer)
  - [Trayicons reloaded](https://github.com/MartinPL/Tray-Icons-Reloaded)
  - [User themes](https://extensions.gnome.org/extension/19/user-themes/)
  - [Vitals](https://github.com/corecoding/Vitals)
  - [Weather in the clock](https://github.com/JasonLG1979/gnome-shell-extension-weather-in-the-clock/)
  - [Wi-Fi Qr](https://gitlab.gnome.org/glerro/gnome-shell-extension-wifiqrcode)
  - [Window navigator](https://extensions.gnome.org/extension/10/windownavigator/)

  preinstalled undebloatable ON/OFF list
  - Application Menu: OFF
  - Auto Move Windows: OFF
  - Launch new istance: OFF
  - Native Window Placement: ON
  - Place Status Indicator: OFF
  - Screenshot Window Sizer: ON
  - Window List: OFF
  - Workspace Indicator: OFF


