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
    - set disk to suggest layout and change ext4 standard ( exluded boot, you can switch it in btrf for compression )
    - set bootloader as systemd-boot (it's simplest of grub)
    - set your name host (the computer device name)
    - set a password and profile
    - set profile to dekstop > gnome > nvidia property driver<br>
    &nbsp;&nbsp;&nbsp;&nbsp;if over 3000 series => +Tensor drivers<br> 
    &nbsp;&nbsp;&nbsp;&nbsp;if Cuda and minor of 3000 => nvidia standrad<br>
    - set audio to pipewire
    - set kernel to kinux or linux-zen (in case have rare hardware)
    - set net equal to iso configuration<br>

    an image of installer:<br>
    ![arch installer profile](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PROFILE.jpg)<br>
    ![arch installer partitions](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PARTITIONS.jpg)
    
    Installation completed? Reboot<br><br>
    
    - add asterisks to consolle, open it and...
        `$ cd /etc/`<br>      
        `$ sudo -s`<br>
        `$ cp sudoers sudoers.bak`<br>
        `$ EDITOR=nano visudo`<br>
        now find or add the string:<br>
        `Defaults env_reset,pwfeedback`<br>
        Ctrl + x and S for save<br>

    - install windows in boot loader

      -  start autoupdater service:<br>
          `$ sudo systemctl start systemd-boot-update.service`<br>
          `$ bootctl update`<br>
      
      In some case system not view windows EFI if in a second drive, so...<br>

      -  find windows partition (EFI of microsoft):<br>
          `$ sudo fdisk -l`<br>

      -  mount it ("b1" or other of efi win):<br>
          `$ mount /dev/sdb1 /mnt`<br>

      -  copy efi into boots:<br>
          `$ sudo cp -r /mnt/EFI/Microsoft/ /boot/EFI/Microsoft/`<br>

          extra step only if not view the windows label:<br>
          create a new /boot/loader/entries/windows.conf file:<br>
          `$ sudo nano /boot/loader/entries/windows.conf`<br>
          and write into it:
          ```
          title   Windows 10
          efi     /EFI/Microsoft/Boot/bootmgfw.efi
          ```
       -  check ends:<br>
          `$ bootctl update`<br>
          `$ bootctl list`<br><br>
          
      <i>you should probably have windows in the boot list.</i><br><br>


    - check/active system HDMI sound services for Nvidia:<br>
      `$ lspci -k | grep -A 2-E "(VGA|3D)"`<br>
      if nvida driver is OK:<br>
      `$ modprobe nvidia dmsg`<br>
      wait a 30/60 seconds or reboot for check sound in control settings panels<br>

    - check/active Nvidia settings:<br>
      `$ sudo pacman -Sy nvidia xconfig && pacman -Syu nvidia-settings`<br>
      now reboot...<br>

    - check/active bluetooth services:<br>
      `$ systemctl enable bluetooth.service`<br>
      `$ systemctl start bluetooth.service `<br>

    - Use and prepare Packages <top><sub>(git/chrome/aur)</sub></top><br>

      - Make a folder for "Package" and enter into it<br>
        `$ mkdir -p ./Packages && cd ./Packages`<br>

      - install Git for cloning pro packages<br>
        `$ sudo pacman -S git`<br>

      - Use Aur for first time, exemple:<br>
        `$ git clone https://aur.archlinux.org/google-chrome.git ./google-chrome`<br>
        `$ cd ./google-chrome`<br>
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
      `$ git clone https://aur.archlinux.org/gnome-software-snapd.git ./snapd-gnome && cd ./snapd-gnome`<br>
      `$ makepkg -si && cd ..`<br>
      <i>on question "remove gnome conflict" ... ever yes.</i><br>

    - Now update and reboot system:<br>
      `$ sudo pacman -Syu && reboot`<br>

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
- `$ sudo pacman -Rsn htop`<br>
- `$ sudo pacman -Rsn vim`<br>
- Etc...

<br>

<b>Expand Files (nautilus):</b><br>
Open console and:<br>
- `$ git clone https://aur.archlinux.org/nautilus-admin.git ./nautilus-admin`<br>
- `$ cd nautilus-admin && makepkg && nautilus -q `<br>
   // note:you can try "sudo pacman -Sy nautilus-admin && nautilus -q"<br><br>

or other extensions on [nautilus-extension in github](https://github.com/topics/nautilus-extension)<br>

<br>

<b>Essentials extensions:</b>

before all: if you use chrome need to install [gnome browser connector](https://aur.archlinux.org/packages/gnome-browser-connector) via AUR for extension management<br>
  `$ git clone https://aur.archlinux.org/gnome-browser-connector.git ./chrome-connector && cd ./chrome-connector`<br>
  `$ makepkg -si && cd ..`<br>

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
  - [Screenshot Tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)
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
  - [Easy Effects](https://flathub.org/apps/details/com.github.wwmm.easyeffects)
  - [Gradience](https://flathub.org/apps/details/com.github.GradienceTeam.Gradience)
  - [Fragments](https://flathub.org/apps/details/de.haeckerfelix.Fragments)

<!--
  via CLI:<br>
  - Grub Customizer:<br>
  `$ sudo pacman -S grub-customizer`<br>
-->

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
  `$ sudo cp -r ./wallpaper/* /usr/share/backgrounds/gnome`<br><br>


- add Gradience color profile<br>
  open the app and make/save first standard colors, after it you have the forlder and can copy in it:<br>
  `$ sudo cp -r ./gradience/*  /home/YOUR_USR_NAME/.var/app/com.github.GradienceTeam.Gradience/config/presets/user`<br>
  now go in cofingurations (top right of topbar) and load "Shell-Colors"... all done.<br><br>



<br><hr><br>

### CLEANING SYSTEM

- remove all orphan pack and dependencies:<br>
  `$ sudo pacman -Rns $(pacman -Qtdq)`<br>

- empty chache:<br>
  `$ sudo du -sh ~/.cache/ && rm -rf ~/.cache/*`<br>

- clean flatpak<br>
  `$ sudo rm -rfv /var/tmp/flatpak-cache-*`<br>
  `$ flatpak uninstall --unused`<br>


- duplicated and corrupted links via rmlint:<br>
  `$ sudo pacman -S rmlint && rmlint -v`<br>
  `$ rmlint -g -c sh:link && bash rmlint.sh` and press "y"<br>

And this is the end... Good Luck Baby 🚀
