# linux arch installation flow
<b> Tested on september 2023 </b>

### A good reference:

1 - [official arch docs](https://wiki.archlinux.org/title/Installation_guide)<br>
2 - [youtube](https://www.youtube.com/watch?v=RsrPrA8NJHk) / [youtube](https://www.youtube.com/watch?v=LGhifbn6088&t=309s) / [youtube](https://www.youtube.com/watch?v=C3D_qzw94v8) / [youtube](https://www.youtube.com/watch?v=sm_fuBeaOqE) / [youtube](https://www.youtube.com/watch?v=JRdYSGh-g3s)<br>
3 - [Stack Exchange Network](https://askubuntu.com/questions/726972/dual-boot-windows-10-and-linux-ubuntu-on-separate-hard-drives)<br>

---
<br> <b>[STEP:1/3] ISO AND BOOTABLE</b>

- Download arch iso linux:<br>
  [archlinux official downloads](https://archlinux.org/download/) via:<br>
	- "Magnet link" <sup>Raccomended</sup><br>
			if you don't have a torrent client you can use [Fragments](https://flathub.org/apps/de.haeckerfelix.Fragments) <i>(better, but only in linux - how to install is below)</i> or [Deluge](https://deluge-torrent.org/) <i>(windows/mac/linux)</i>.<br>
	- "Browser" <sup>slow</sup><br>
    		- latest ISO from [EU ITALY Mirror](https://archmirror.it/repos/iso/latest/)<br>
    		- latest ISO from [EU UK Mirror](https://www.mirrorservice.org/sites/ftp.archlinux.org/iso/latest/)<br>
    		- latest ISO from [USA Mirror](http://mirror.fossable.org/archlinux/iso/latest/) <br>
    		- latest ISO from [INDIA Mirror](https://mirror.sahil.world/archlinux/iso/latest/)<br>
    		- latest ISO from [JAPAN Mirror](https://repo.jing.rocks/archlinux/iso/latest/)<br>
    		- latest ISO from [RUSSIA Mirror](https://mirror.yandex.ru/archlinux/iso/latest/)<br>
    		- latest ISO from [AFRICA Mirror](https://mirrors.urbanwave.co.za/archlinux/iso/latest/)<br>
    		- latest ISO from [CHINA Mirror](https://hkg.mirror.rackspace.com/archlinux/iso/latest/)<br>
    		- latest ISO from [AUSTRALIA Mirror](https://archlinux.mirror.digitalpacific.com.au/iso/latest/)<br>
    		- latest ISO from [ARGENTINA Mirror](https://mirrors.eze.sysarmy.com/archlinux/iso/latest/)<br>

- Make an iso bootable usb<br>
	- if in windows: download [rufus official downloads](https://rufus.ie/it/) and start to create an <i>iso bootable</i> usb drive with arch iso image
    	- raccommended: check your bios is an uefi:<br>
      	...in bios you can find it in the options<br>
      	...in windows: win+R and write "msinfo32" and "BIOS" (or BIOS mode), check if "secure boot" is off or set it via bitlocker<br>
    	- [raccommended option](https://blog.htbaa.com/wp-content/uploads/2013/11/rufus.png): MBR, FAT32, 8192byte, and load iso of arch.<br>

	- if in linux:
		- use [Impression](https://gitlab.com/adhami3310/Impression)

- No second drive? need a partition:<br><sup><sub>⚠️ Warning: if you not an expert see on youtube before this action! Shrink, formatting and move partition can cause an irreversible lost of data</sub><sup>
  - via linux terminal [(this link)](https://phoenixnap.com/kb/linux-create-partition)
  - in windows:<br>
    - win+r and write `diskmgmt.msc`
    - right click on NFTS window partition and shrink it with min 6GB for linux<br>

- Restart and boot way:<br>
	a) go to bios and load arch from usb (or set it first boot)<br>
 	b) via windows:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;1) open win menu and find "startup"<br>
	&nbsp;&nbsp;&nbsp;&nbsp;2) open "advanced sturtup recovery" (ITA:modifica le opzioni di avvio avanzato)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;3) click on "advanced sturtup" > "use a device" > select your bootable arch usb<br>

<br> <b>[STEP:2/3] PREPARING TO INSTALLATION</b>

- Set Keyboard Layout:<br>
    `$ loadkeys it` (or other lang)<br>

- Set time zone:<br>
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

<br> <b>[STEP:3/3] INSTALL LINUX OS</b>

- from 2022 you can use a graphical installer (it's good! :D):<br>
  `$ archinstall`<br>

   follow the instruction into installer ( and save your json profile if you want ;) )<br>
   <top><sub>SUGGEST: <i>Always select more than one mirror to avoid potential crashes or update failures</i></sub></top><br><br>
   Installation exemple:<br>

    - set your lang everywhere... And `UTF8` character sets
    - set disk to suggest layout and change `btrf` standard and:<br>
    &nbsp;&nbsp;&nbsp;&nbsp;set `compressed` on true<br>
    &nbsp;&nbsp;&nbsp;&nbsp;set `swap` on true<br>
    - set bootloader as `systemd-boot` (it's simplest of grub) and `gdm`
    - set your name host (the computer device name)
    - set a password and one profile, set it as an admin
    - set profile to dekstop > gnome > nvidia property driver<br>
    &nbsp;&nbsp;&nbsp;&nbsp;if over 3000 series => +Tensor drivers<br> 
    &nbsp;&nbsp;&nbsp;&nbsp;if Cuda and minor of 3000 => nvidia standrad<br>
    - set audio to `pipewire`
    - set kernel to `linux` or `linux-zen` (in case have rare hardware)
    - set net equal to iso configuration<br>

    an image of installer:<br> 
    ![arch installer profile](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PROFILE.jpg)<br>
    ![arch installer partitions](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PARTITIONS-btrf.jpg)<br>
another way is partitioned in fat or ext4 mix single btrf (not raccomended way)<br>
    ![arch installer partitions](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PARTITIONS-ext4.jpg)<br>
    
    Installation completed? Reboot<br><br>
    
- Add asterisks to consolle password, open it and...<br>
	`$ cd /etc/`<br>
	`$ sudo -s`<br>
	`$ cp sudoers sudoers.bak`<br>
	`$ EDITOR=nano visudo`<br>
	now find or add the string:<br>
	`Defaults env_reset,pwfeedback`<br>
	Ctrl + x and S for save<br>

- Install windows in boot loader

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

- check/active HDMI system:<br><sup><sub>⚠️ Warning: this step is under checks, from 2023 in installer you have property driver but it install the open in any case. The result of this operations is dangerous and not stable</sub></sup>
	- sound services for Nvidia:<br>
		`$ lspci -k | grep -A 2 -E "(VGA|3D)"`<br>
		if nvida driver is OK:<br>
		`$ modprobe nvidia dmsg`<br>
		wait a 30/60 seconds or reboot for check sound in control settings panels<br>

	- set Nvidia settings:<br>
		`$ sudo pacman -Sy nvidia xconfig && pacman -Syu nvidia-settings`<br>
		now reboot...<br>

- Launch audio services...<br>
	`$ systemctl --user --now enable pipewire`<br>
  	`$ systemctl --user list-unit-files | grep -E 'pulse|wire' | awk '{ print $1,"-", $2 }'` (check enables services, is it true?)<br>

- Launch bluetooth services:<br>
	`$ systemctl enable bluetooth.service`<br>
	`$ systemctl start bluetooth.service `<br>

- Install Network Manager: <br>
	`$ sudo pacman -S networkmanager`<br>
 	`$ sudo systemctl enable NetworkManager`<br>
	`$ sudo systemctl enable NetworkManager.service`<br>
	`$ sudo systemctl start NetworkManager.service`<br>
	`$ sudo systemctl enable wpa_supplicant.service`<br>
	now make or edit with `wifi.powersave=2` the :<br>
	`$ sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf` (not recommended!)<br>
	need to refresh wi-fi? :<br>
	`$ sudo systemctl restart NetworkManager && sudo systemctl enable wpa_supplicant.service`<br>


- Use and prepare Packages <top><sub>(git/aur/other)</sub></top><br><blockquote>💩 make attention: Linux doesn't have a bond for make single folder for programs and more of thems are installed following the [FHS](https://it.wikipedia.org/wiki/Filesystem_Hierarchy_Standard) standard insted have all files in their a property folder. Yep, it's a problem for understand what is installed and all relative dependecies but other solutions, currently, doesn't exist (or better, i don't find it). I suggest install all your packs via AUR (not gnome-software) and track it via Bauh. Anyway, you can try to modding folder (like below) of flatpack/flathub install [info](https://www.reddit.com/r/flatpak/comments/a1l8wk/methods_to_save_space_on_your_root_partition/)] - [[flatpak-installation](https://man7.org/linux/man-pages/man5/flatpak-installation.5.html)] - [[user-vs-system-install](https://docs.flathub.org/docs/for-users/user-vs-system-install)]</blockquote>
	- Make a folder for your "Package" (like Programs in window):<br>Open terminal in Home and enter into it `$ mkdir -p ./Packages && cd ./Packages`, now:<br>
		- open nautilus and press `ctrl+L`<br>
		- copy `/etc/flatpak/installations.d` on address bar<br>
		- open that folder in terminal ad with set CLI: `sudo nano extra.conf`<br>
		- copy this for set a new installation folder:<br>
		```txt
		[Installation "packs"]
		Path=/home/YOURUSRNAME/Packages
		DisplayName=Packages Installation
		StorageType=harddisk
		```
		you can use it in this way for flatpack<br>
		```
		1. Add a remote with: `flatpak --installation=packs remote-add flathub https://flathub.org/repo/flathub.flatpakrepo`
		2. Install to it with: `flatpak --installation=packs install flathub org.inkscape.Inkscape` (inkscape is an exemple)
		3. Run from it with: flatpak run org.inkscape.Inkscape
		```

- install Git for cloning pro packages<br>
	`$ sudo pacman -S git`<br>

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
  	Configure your global credential:<br>
	`$ git config --global user.name "JohnDoe"`<br>
	`$ git config --global user.email johndoe@example.com`<br>
	`$ git config --global credential.helper store`<br>
	`$ git config --list --show-origin`<br>
	Are you in .config ? So good, restart terminal!<br>

	- Now update and reboot system:<br>
		`$ sudo pacman -Syu && reboot`<br>

<br><hr><br>

### POST INSTALLATION
<sup><b><i>OPTIMIZATION, ESSENTIAL EXTENSIONS, CUSTOMIZING (Gnome 4X.X)</i></b><br><br></sup>

<b>Set Autologin:</b><br>
`$ sudo nano /etc/gdm/custom.conf`<br>
Add into file:
```
[daemon]
AutomaticLoginEnable=True
AutomaticLogin=username
```

<br><b>Debloat packs:</b><br>

<top><sub><i>Note: Rscgn remove all dependencies (dangerous) of pack</i></sub></top><br>

- `$ sudo pacman -Q` <top><sub><i>(for list) (use "| grep NAMEPACK" for detect it)</i></sub></top><br>
- `$ sudo pacman -Rsn gnome-contacts`<br>
- `$ sudo pacman -Rsn gnome-maps`<br>
- `$ sudo pacman -Rsn simple-scan`<br>
- `$ sudo pacman -Rsn gnome-music`<br>
- `$ sudo pacman -Rsn gnome-font-viewer` <br>
- `$ sudo pacman -Rsn gnome-calendar`<br>
- `$ sudo pacman -Rsn gnome-tour`<br>
- `$ sudo pacman -Rsn malcontent` <top><sub><i>(parental control)</i></sub></top><br>
- `$ sudo pacman -Rsn gnome-photos` <top><sub><i>(photo albums)</i></sub></top><br> 
- `$ sudo pacman -Rsn totem` <top><sub><i>(video player)</i></sub></top><br> 
- `$ sudo pacman -Rsn htop`<br>
- `$ sudo pacman -Rsn vim`<br>
- Etc...

<br>

<b>Install Font-manager:</b><br>
Open console and:<br>
- `$ pacman -S font-manager `<br>

- Install/Fix Unicode Charactes:<br>
	Open Packages folder and add new fonts (make attention to not install the useless fontforge):
	- `$ git clone https://aur.archlinux.org/font-symbola.git ./symbola && cd ./symbola`<br>
	- `$ makepkg -si && cd ..`<br>
	Extra:<br>
	- `$ sudo pacman -S noto-fonts-emoji` or/and `$ sudo pacman -S ttf-font-awesome`<br>
	- `$ sudo fc-cache -f -v`<br>




<br>

<b>Expand Files (nautilus):</b><br>
Open console and:<br>
- `$ git clone https://aur.archlinux.org/nautilus-admin.git ./nautilus-admin`<br>
- `$ cd nautilus-admin && makepkg && nautilus -q `<br>
   > note:you can try "sudo pacman -Sy nautilus-admin && nautilus -q"

<br>
or other extensions on [nautilus-extension in github](https://github.com/topics/nautilus-extension) and [GNOME/Files](https://wiki.archlinux.org/title/GNOME/Files)<br>

<br>

<b>Essentials extensions:</b>

- AUR Packs:<br>

	- pacman -S filemanager-actions (currently not available)<br>

	- [snapper gui](https://github.com/ricardomv/snapper-gui) (graphical backup system helper)<br>
	- `$ git clone https://aur.archlinux.org/snapper-gui-git.git ./snapper-gui && cd ./snapper-gui`<br>
	- `$ makepkg -si && cd .. `<br>


	- [Bauh](https://github.com/vinifmor/bauh)<br>
	`$ git clone  https://aur.archlinux.org/bauh.git ./bauh && cd ./bauh`<br>
	`$ makepkg -si && cd ..`<br>

	- [Easy Effects](https://github.com/wwmm/easyeffects)<br>
	`$ git clone https://aur.archlinux.org/easyeffects-git.git ./easyeffects && cd ./easyeffects`<br>
	`$ makepkg -si && cd ..`<br>

	- [Gradience](https://github.com/GradienceTeam/Gradience)<br>
	`$ git clone https://aur.archlinux.org/gradience.git ./gradience && cd ./gradience`<br>
	`$ makepkg -si && cd ..`<br>

	- [Fragments](https://flathub.org/apps/details/de.haeckerfelix.Fragments)<br>
	`$ git clone https://aur.archlinux.org/fragments-git.git ./fragments && cd ./fragments`<br>
	`$ makepkg -si && cd ..`<br>

	- [Impression](https://flathub.org/apps/io.gitlab.adhami3310.Impression)<br>
	`$ git clone https://aur.archlinux.org/impression.git ./impression && cd ./impression`<br>
	`$ makepkg -si && cd ..`<br>

	- [google chrome](https://aur.archlinux.org/packages/google-chrome) (it's google standard, not [chromium](https://wiki.archlinux.org/title/chromium))<br>
	`$ git clone https://aur.archlinux.org/google-chrome.git ./google-chrome && cd ./google-chrome`<br>
	`$ makepkg -si && cd ..`<br>

	- [vscode](https://aur.archlinux.org/packages/visual-studio-code-bin) (probably you are dev, so...)<br>
	`$ git clone https://aur.archlinux.org/visual-studio-code-bin.git ./vscode && cd ./vscode`<br>
	`$ makepkg -si && cd ..`<br>
	fixing: if, on double click, vscode open the dir on desktop:<br>
	`$ xdg-mime default org.gnome.Nautilus.desktop inode/directory`

	- [nvm-desktop](https://aur.archlinux.org/nvm-desktop.git) (are you a js dev like me? so, install nvm, npm, nodejs...)<br>
	`$ git clone https://aur.archlinux.org/nvm-desktop.git ./nvm-desktop && cd ./nvm-desktop`<br>
	`$ makepkg -si && cd ..`<br>
	Probably it install yarn, read how to clen it [here](https://stackoverflow.com/questions/42334978/how-do-i-uninstall-yarn) and [here](https://www.reddit.com/r/archlinux/comments/hdqhea/how_do_i_uninstall_yarn/)<br>


- Gnome Extensions:<br>
	before all: if you use chrome need to install [gnome browser connector](https://aur.archlinux.org/packages/gnome-browser-connector) via AUR for extension management<br>
	`$ git clone https://aur.archlinux.org/gnome-browser-connector.git ./chrome-connector && cd ./chrome-connector`<br>
	`$ makepkg -si && cd ..`<br>

	- [Add to desktop](https://extensions.gnome.org/extension/3240/add-to-desktop/)
	- [Alt Tab Slide](https://extensions.gnome.org/extension/97/coverflow-alt-tab/)<br>
	- [Arch update alert icon](https://extensions.gnome.org/extension/1010/archlinux-updates-indicator/)<br>
	 	- note: you need to install `sudo pacnman -S pacman-contrib`, into the options remove classic command with this:<br>
		```bash
		kgx -- /bin/sh -c "echo -e \"\n***\n\nSystem Updating:\n\" && sudo pacman -Syu || echo -e \"\nNothing to update\" \ && echo -e \"\n***\n\nSnap Packs Updating:\n\" && sudo snap refresh && echo -e \"\n***\n\nFlatpack Updating:\n\" && flatpak update && echo -e \"\n***\n\nPacman Updating:\n\" && (pacman -Qdtq | grep -q .) && echo -e \"\n***\n\nPacks Cleaning:\" && sudo pacman -Rns \$(pacman -Qdtq) || echo \"Nothing to clean\" && echo -e \"\n***\n\" && echo Done - Perss Enter to exit; read && exit"
		```
	- [Blur on lockscreen](https://extensions.gnome.org/extension/2935/control-blur-effect-on-lock-screen/) 
	- [Bluetooth battery indicator](https://extensions.gnome.org/extension/3991/bluetooth-battery/)
	- [Bluetooth quick connect](https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/)
	- [Blur my shell](https://extensions.gnome.org/extension/3193/blur-my-shell/)
	- [Burn My Windows](https://extensions.gnome.org/extension/4679/burn-my-windows/)
	- [Compact quick settings](https://extensions.gnome.org/extension/5527/compact-quick-settings/)
	- [Compiz windows effect](https://extensions.gnome.org/extension/3210/compiz-windows-effect/)
	- [Clipboard Manager](https://extensions.gnome.org/extension/4422/gnome-clipboard/)
	- [Desktop GTK4 (icons,drag,dock)](https://extensions.gnome.org/extension/5263/gtk4-desktop-icons-ng-ding/)
	- <s>[Day/night theme switcher](https://extensions.gnome.org/extension/4968/lightdark-theme-switcher/)</s> 2023: gnome 44.X uncompatible
	- [Easy Screen Cast](https://extensions.gnome.org/extension/690/easyscreencast/)
	- [Just perfection](https://extensions.gnome.org/extension/3843/just-perfection/)
	- [No titlebar when maximized](https://extensions.gnome.org/extension/4630/no-titlebar-when-maximized/) (optional)
	- [Removable drive in menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
	- [Settings center](https://extensions.gnome.org/extension/2899/settingscenter/)
	- [Screenshot Tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;<sup><sub>note: you need to install `sudo pacnman -S gnome-screenshot`</sub></sup><br>
	- [Top bar organizer](https://extensions.gnome.org/extension/4356/top-bar-organizer/)
	- [Trayicons reloaded](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)
	- [User themes](https://extensions.gnome.org/extension/19/user-themes/)
	- [Vitals](https://extensions.gnome.org/extension/1460/vitals/)
	- [Weather in the clock](https://extensions.gnome.org/extension/5470/weather-oclock/)
	- [Wi-Fi Qr](https://extensions.gnome.org/extension/5416/wifi-qrcode/)
	- <s>[Window navigator](https://extensions.gnome.org/extension/10/windownavigator/)</s> 2023: currently useless<br>


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

2) open Theme-Pack folder and...<br>
	- open nautilus and unlock hidden files
	- copy files of the theme into home directory
	- set in the customization (gnome tweaks>apparence) like the screenshot<br>

![arch installer partitions](https://raw.githubusercontent.com/berto-dev/linux-arch-installation-flow/main/Theme-Pack-Screenshot.jpg)<br>

- add Gradience color profile<br>
  open the app and make/save first standard colors, after it you have the forlder and can copy in it:<br>
  `$ sudo cp -r ./gradience/*  /home/YOUR_USR_NAME/.var/app/com.github.GradienceTeam.Gradience/config/presets/user`<br>
  now go in cofingurations (top right of topbar) and load "Shell-Colors"... all done.<br><br>



<br><hr><br>

### CLEANING SYSTEM

or you can install [bleachbit](https://www.bleachbit.org/download)<br>
- bleachbit AUR:<br>
	`$ git clone https://aur.archlinux.org/bleachbit-git.git ./bleachbit && cd ./bleachbit`<br>
	`$ makepkg -si && cd ..`<br><br>

or you can use secure and manually commands:

- remove all orphan pack and dependencies:<br>
  `$ sudo pacman -Rns $(pacman -Qtdq)`<br>

- empty chache:<br>
  `$ sudo du -sh ~/.cache/ && rm -rf ~/.cache/*`<br>

- clean flatpak [*](https://www.debugpoint.com/clean-up-flatpak/)<br>
  `$ sudo rm -rfv /var/tmp/flatpak-cache-*`<br>
  `$ flatpak uninstall --unused`<br>


- duplicated and corrupted links via rmlint:<br>
  `$ sudo pacman -S rmlint && rmlint -v`<br>
  `$ rmlint -g -c sh:link && bash rmlint.sh` and press "y"<br><br><br>


And this is the end... Good Luck Baby 🚀
