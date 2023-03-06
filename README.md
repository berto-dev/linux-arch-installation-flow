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

  NOTE: next step have better solution for make the partitions
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

    an image of installer:<br>
    <top><sub>Attention: Select a desktop env (gnome or kde) and not "minimal" if your not expert to install it via cli!!</sub></top>
    ![arch installer profile](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PROFILE.jpg)<br>
    ![arch installer partitions](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PARTITIONS.jpg)
    
    Installation completed? Reboot<br>
    
    - Now update and reboot system:<br>
      `$ sudo pacman -Syu && reboot`<br>

    - Use and prepare Packages <top><sub>(git/chrome/aur)</sub></top><br>

      - Make a folder for "Package" and enter into it<br>
        `$ mkdir -p ./Packages && cd ./Packages`<br>

      - install Git for cloning pro packages<br>
        `$ sudo pacman -S git`<br>

      - Use Aur for first time, exemple:<br>
        `$ git clone https://aur.archlinux.org/google-chrome.git ./google-chrome` && cd ./google-chrome`<br>
        `$ makepkg -si && cd ..`<br>
        
    - Install [Snap Store](https://snapcraft.io/install/snap-store/arch) in arch via console<br>
      `$ git clone https://aur.archlinux.org/snapd.git ./snapd && cd ./snapd`<br>
      `$ makepkg -si && cd ..`<br>
      `$ sudo systemctl enable --now snapd.socket`<br>
      `$ sudo ln -s /var/lib/snapd/snap /snap`<br>
      return in <i>./Packages</i> and add to gnome software:<br>
      `$ git clone https://aur.archlinux.org/snapd-glib.git ./snap-glib && cd ./snap-glib`<br>
      `$ makepkg -si && cd ..`<br>
      return in <i>./Packages</i> and add to gnome software:<br>
      `$ git clone https://aur.archlinux.org/gnome-software-snapd.git ./snapd-gnome && cd ./snap-gnome`<br>
      `$ makepkg -si && cd ..`<br>
      <i>on question "remove gnome conflict" ... ever yes.</i><br>


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

<top><sub><i>Note: Rscgn remove all dependencies (dangerous) of pack</i></sub></top><br>

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

before all: if you use chrome need to install [gnome browser connector](https://aur.archlinux.org/packages/gnome-browser-connector) via AUR for extension management<br>
  `$ git clone https://aur.archlinux.org/gnome-browser-connector.git ./chrome-connector && cd ./chrome-connector`<br>
  `$ makepkg -si && cd ..`



  - [Add to desktop](https://extensions.gnome.org/extension/3240/add-to-desktop/)
  - [Alt Tab Slide](https://extensions.gnome.org/extension/97/coverflow-alt-tab/)
  - [Arch update alert icon](https://extensions.gnome.org/extension/1010/archlinux-updates-indicator/)
  - [Blur on lockscreen](https://extensions.gnome.org/extension/2935/control-blur-effect-on-lock-screen/) (optional)
  - [Bluetooth battery indicator](https://extensions.gnome.org/extension/3991/bluetooth-battery/)
  - [Bluetooth quick connect](https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/)
  - [Blur my shell](https://extensions.gnome.org/extension/3193/blur-my-shell/)
  - [Burn My Windows](https://extensions.gnome.org/extension/4679/burn-my-windows/)
  - [Compact quick settings](https://extensions.gnome.org/extension/5527/compact-quick-settings/) (optional)
  - [Compiz windows effect](https://extensions.gnome.org/extension/3210/compiz-windows-effect/)
  - [Clipboard Manager](https://extensions.gnome.org/extension/4422/gnome-clipboard/)
  - [Desktop icons neo](https://extensions.gnome.org/extension/4337/desktop-icons-neo/)
  - [Day/night theme switcher](https://extensions.gnome.org/extension/4968/lightdark-theme-switcher/)
  - [Easy Screen Cast](https://extensions.gnome.org/extension/690/easyscreencast/)
  - [Just perfection](https://extensions.gnome.org/extension/3843/just-perfection/)
  - [No titlebar when maximized](https://extensions.gnome.org/extension/4630/no-titlebar-when-maximized/) (optional)
  - [Removable drive in menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
  - [Settings center](https://extensions.gnome.org/extension/2899/settingscenter/)
  - [Top bar organizer](https://extensions.gnome.org/extension/4356/top-bar-organizer/)
  - [Trayicons reloaded](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)
  - [User themes](https://extensions.gnome.org/extension/19/user-themes/)
  - [Vitals](https://extensions.gnome.org/extension/1460/vitals/)
  - [Weather in the clock](https://extensions.gnome.org/extension/5470/weather-oclock/)
  - [Wi-Fi Qr](https://extensions.gnome.org/extension/5416/wifi-qrcode/)
  - [Window navigator](https://extensions.gnome.org/extension/10/windownavigator/)<br>

  via AUR:<br>
  - [Filemanager actions](https://archlinux.org/packages/community/x86_64/filemanager-actions/)<br>

  via flathub:<br>
  - [Fragments](https://flathub.org/apps/details/de.haeckerfelix.Fragments)
  - [Gradience](https://flathub.org/apps/details/com.github.GradienceTeam.Gradience)

  via CLI:<br>
  - Grub Customizer:<br>
  `$ sudo pacman -S grub-customizer`<br>

  preinstalled undebloatable ON/OFF list
  - Application Menu: OFF
  - Auto Move Windows: OFF
  - Launch new istance: OFF
  - Native Window Placement: ON
  - Place Status Indicator: OFF
  - Screenshot Window Sizer: ON
  - Window List: OFF
  - Workspace Indicator: OFF

<br>

#### Add a simple shell theme packs (it's my simple theme asset)

1) download the [theme pack](https://github.com/berto-dev/linux-arch-installation-flow/raw/main/Theme-Pack.zip) and unzip it.

2) copy file of theme...<br>
remember: "gnome have the hidden folder for override (unlock hide file and search, for exemple, .icons in /home) but not all it's getted good. In that case you can follow the below command lines for copy direct into the system user folder."<br>

open Theme-Pack folder and...<br>
- add shell theme (Based on Fluent-Round-White/Dark)<br>
  `$ sudo cp -r ./themes/* /usr/share/themes`<br>

- add icons (Based on Depeen) and cursor (Based on Qogir)<br>
  `$ sudo cp -r ./icons/* /usr/share/icons`<br>

- add the wallpaper<br>
  `$ sudo mkdir -p /usr/share/wallpaper`<br>
  `$ sudo cp -r ./wallpaper/* /usr/share/wallpaper && xdg-open /usr/share/wallpaper`<br><br>


- add Gradience color profile<br>
  `$ sudo cp -r ./gradience/*  /home/YOUR_USR_NAME/.var/app/com.github.GradienceTeam.Gradience/config/presets/user`<br><br>


And this is the end... Good Luck Baby 🚀
  
  

