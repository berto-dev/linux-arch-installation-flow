# linux arch installation flow
<b> Tested on dicember 2023 (under update!!) </b>

### A good reference:

1 - [official arch docs](https://wiki.archlinux.org/title/Installation_guide)<br>
2 - [youtube](https://www.youtube.com/watch?v=RsrPrA8NJHk) / [youtube](https://www.youtube.com/watch?v=LGhifbn6088&t=309s) / [youtube](https://www.youtube.com/watch?v=C3D_qzw94v8) / [youtube](https://www.youtube.com/watch?v=sm_fuBeaOqE) / [youtube](https://www.youtube.com/watch?v=JRdYSGh-g3s)<br>
3 - [Stack Exchange Network](https://askubuntu.com/questions/726972/dual-boot-windows-10-and-linux-ubuntu-on-separate-hard-drives)<br>

<br><hr><br>

<b>[STEP:1/3] ISO AND BOOTABLE</b>

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
	- if in _windows_: download [rufus official downloads](https://rufus.ie/it/) and start to create an <i>iso bootable</i> usb drive with arch iso image
    	- raccommended: check your bios is an uefi:<br>
      	...in bios you can find it in the options<br>
      	...in windows: win+R and write "msinfo32" and "BIOS" (or BIOS mode), check if "secure boot" is off or set it via bitlocker<br>
    	- [raccommended option](https://blog.htbaa.com/wp-content/uploads/2013/11/rufus.png): MBR, FAT32, 8192byte, and load iso of arch.<br>
	- if in _linux_:
		- use [Impression](https://gitlab.com/adhami3310/Impression)
<br><br>

- No second drive? need a partition:<br><sup><sub>⚠️ Warning: if you not an expert see on youtube before this action! Shrink, formatting and move partition can cause an irreversible lost of data</sub><sup>
  - via linux terminal [(this link)](https://phoenixnap.com/kb/linux-create-partition)
  - in windows:<br>
    - win+r and write `diskmgmt.msc`<br>
    - right click on NFTS window partition and shrink it with min 6GB for linux
<br><br>

- Restart and boot way:<br>
	a) go to bios and load arch from usb (or set it first boot)<br>
 	b) via windows:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;1) open win menu and find "startup"<br>
	&nbsp;&nbsp;&nbsp;&nbsp;2) open "advanced sturtup recovery" (ITA:modifica le opzioni di avvio avanzato)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;3) click on "advanced sturtup" > "use a device" > select your bootable arch usb
<br><br>

<br> <b>[STEP:2/3] PREPARING TO INSTALLATION</b>

- Set Keyboard Layout:<br>
    `$ loadkeys it` (or other lang)
<br><br>

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
          &nbsp;&nbsp;&nbsp;&nbsp;`[iwd]# station DEVICE connect SSID`
<br><br>

<br> <b>[STEP:3/3] INSTALL LINUX OS</b>

- from 2022 you can use a parametric/graphical installer ( in dic 2023 it's now amazing! ):<br>
  `$ archinstall`<br>

   follow the instruction into installer ( and save your json profile if you want ;) )<br>
   <top><sub>SUGGEST: <i>Always select more than one mirror to avoid potential crashes or update failures</i></sub></top><br><br>
   Installation exemple:<br>

	- set multiple mirrors, exemple: _[Worldwide, United States, United Kingdom, Spain, Italy]_
	- set your lang + UTF8 on keyboard : _[ layout: it, language: it_IT.UTF-8, encoding: UTF-8 ]_
    	- set `disk layout` to `btrf` standard and choose : _[ no to subvolumes, no to separate home, yes to compression ]_
     	- set `disk encripting` to your preference
      	- set `swap` on `true`<br>
	- set bootloader as `GRUB` (2023 systemd-boot it isn't present)
    	- set your name host (the computer device name, ex: linux)
    	- set a password and one profile, set it as an admin
    	- set profile for a dekstop > gnome > nvidia property driver:<br>
    &nbsp;&nbsp;&nbsp;&nbsp;if over 3000 series => nvidia proprietary or nouveau +Tensor drivers<br> 
    &nbsp;&nbsp;&nbsp;&nbsp;if Cuda and minor of 3000 => nvidia proprietary<br>
    	- set audio to `pipewire`
    	- set kernel `linux-zen` (better performance) or the mainline `linux`
    	- set net equal to iso configuration<br>
	- set timezone on your place (ex: Europe/Rome)
 	- set NTP on `true`<br><br>

	now install 🚀<br><br>

    an image of installer (WRONG, I MUST TO UPDATE IMAGE YET!):<br> 
    ![arch installer profile](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PROFILE.jpg)<br>
    ![arch installer partitions](https://github.com/berto-dev/linux-arch-installation-flow/blob/main/ARCHINSTALLER-PARTITIONS-btrf.jpg)<br>
    
    Installation completed? Don't set nothing other! You are probably in the root of installer... Digit `exit` and `reboot`
<br><br>

- Add asterisks to consolle password, open it and...<br>
	`$ cd /etc/`<br>
	`$ sudo -s`<br>
	`$ cp sudoers sudoers.bak`<br>
	`$ EDITOR=nano visudo`<br>
	now find or add the string:<br>
	`Defaults env_reset,pwfeedback`<br>
	Ctrl + x and S for save
<br><br>

- UPDATING... <del>Install windows in boot loader <sup>(if you have windows, obious)</sup></del>

	-   <del>start autoupdater service:<br></del>
		<del>`$ sudo systemctl start systemd-boot-update.service`<br></del>
		<del>`$ bootctl update`<br></del>
      
	<del>In some case system not view windows EFI if in a second drive, so...<br></del>

	-  <del>find windows partition (EFI of microsoft):<br></del>
		<del>`$ sudo fdisk -l`<br></del>

	-  <del>mount it ("b1" or other of efi win):<br></del>
		<del>`$ mount /dev/sdb1 /mnt`<br></del>

	-  <del>copy efi into boots:<br></del>
		<del>`$ sudo cp -r /mnt/EFI/Microsoft/ /boot/EFI/Microsoft/`<br></del>

		<del>extra step only if not view the windows label:<br></del>
		<del>create a new /boot/loader/entries/windows.conf file:<br></del>
		<del>`$ sudo nano /boot/loader/entries/windows.conf`<br></del>
		<del>and write into it:</del>
		<del>```
		title   Windows 10
		efi     /EFI/Microsoft/Boot/bootmgfw.efi
		```</del>
	-  <del>check ends:<br></del>
		<del>`$ bootctl update`<br></del>
		<del>`$ bootctl list`<br><br></del>
          
		<del><i>you should probably have windows in the boot list.</i></del>
<br><br>

- Unlock mirrors:<br>
	`$ sudo nano /etc/pacman.conf`<br>
 	find and uncomment (remove "#") the:
	```
	[multilib]
	Include = /etc/pacman.d/mirrorlist
	```
	now you can install from mirrolist in 32/64
<br><br>

- Set windows on center:<br>
	`$ gsettings set org.gnome.mutter center-new-windows true`
<br><br>

- Swipe win/alt <sup>if you have it reversed</sup>:<br>
	`$ setxkbmap -option altwin:swap_alt_win`
<br><br>

- Launch audio services... <sup>(if not running)</sup><br>
  	`$ pactl info | grep "Server Name"` if not result "Name: PulseAudio (on PipeWire 0.XXXX)":<br>
	`$ systemctl --user --now enable pipewire`<br>
  	`$ systemctl --user list-unit-files | grep -E 'pulse|wire' | awk '{ print $1,"-", $2 }'` (check enables services, is it true?)<br>
	If you have some problem see [this](https://www.reddit.com/r/pop_os/comments/v3g2w9/comment/ib0dysx/?utm_source=share&utm_medium=web3x&utm_name=web3xcss&utm_term=1&utm_content=share_button), [this](https://askubuntu.com/a/1067880), [this](https://srobb.net/pipewire.html) for set output, [this](https://unix.stackexchange.com/a/390908) and you can have support via software by [pavucontrol](https://archlinux.org/packages/extra/x86_64/pavucontrol/) and [easyeffects](https://aur.archlinux.org/packages/easyeffects-git) or [JDSP4Linux](https://github.com/Audio4Linux/JDSP4Linux)
<br><br>

- Launch bluetooth services: <sup>(if not running)</sup><br>
	`$ systemctl status bluetooth.service` if isn't "active (running)":<br>
	`$ systemctl enable bluetooth.service`<br>
	`$ systemctl start bluetooth.service `
 <br><br>

- install Git for cloning pro packages<br>
	`$ sudo pacman -S git base-devel`
<br><br>

- install [Pamac](https://www.osside.net/wp-content/uploads/2023/07/pamacgtk43.webp) for a real [AUR](https://aur.archlinux.org/packages) Store packages management<br><br>
	- install trizen:<br>
	`$ git clone https://aur.archlinux.org/trizen.git ./trizen`<br>
	`$ makepkg -sri`<br>
	- install pamac:<br>
	`trizen -S pamac-aur-git libpamac-git archlinux-appstream-data-pamac`
	- remove trizen:<br>
	`$ sudo pacman -Runs trizen`<br>
	set inside pamac option > thirdy parts > AUR turned ON...  Now you can get all aur packages from Pamac Store Application: "**Ṩ**"<br><br>
   	if you would remove pamac you can do:<br>
	`$ sudo pacman -R pamac-aur-git libpamac-git archlinux-appstream-data-pamac`<br>
	`$ sudo pacman -S archlinux-appstream-data`<br>
	Pamac follow the standard directory of FSH or package instruction, press ctrl+L and:<br>
 	&nbsp;&nbsp;&nbsp;&nbsp;» ALL OFFICIAL REPOS DOWNLOAD: _/var/lib/pacman/local_<br>
 	&nbsp;&nbsp;&nbsp;&nbsp;» AUR DOWNLOAD AD UNSPECIFIED: _/opt_ (suggested for all other software)<br>
 	&nbsp;&nbsp;&nbsp;&nbsp;» FLATPAK DOWNLOAD PACKS: _/var/lib/flatpak_<br>
 	&nbsp;&nbsp;&nbsp;&nbsp;» DEPENCIES AND LIBS: _/var/lib/_ and _/lib64_
<br><br>

- add gpu settings {**Ṩ** nvidia-settings}: <sup>(if not installer)</sup><br>
	`$ sudo pacman -S nvidia-settings`<br>

- add gpu cuda for 3d heavy<br>
	`$ sudo pacman -S opencl-nvidia`<br>
	`$ sudo pacman -S opencl-headers`<br>
 	`$ sudo pacman -S cuda`<br>
	`$ sudo pacman -S clinfo` <sup>digit clinfo for gpu informations</sup><br>
 	reboot
<br><br>

- install snaps backups system {**Ṩ** snapper, snapper-git, grub-btrfs, btrfs-assistant }<br>
  	1] install packages: `$ sudo pacman -S snapper snapper-git grub-btrfs btrfs-assistant`<br>
   	2] go in root `$ cd /` and check subvolumes: `$ btrfs subvolume list /`<br>
	3] if not exist snapshots:<br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$ su -` (become the root)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$ cd /` (enter in the root)<br>
	&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;`$ snapper -c root create-config /`<br>
 	4] Now you can open the btrf-assistant, get the snap and set or make new shoots! (suggest: after all this files, make a shoot)
<br><br>

- Install [Network & Network Manager](https://archlinux.org/packages/extra/x86_64/networkmanager/) {**Ṩ** networkmanager}: <br><br>
  	**Before all**: you need to get you good firmware for you wifi card if is a basic installation... In mycase is an AX210 by [Intel](https://www.intel.com/content/www/us/en/support/articles/000005511/wireless.html)~[data-sheet](https://wireless.wiki.kernel.org/en/users/drivers/iwlwifi) with all instructions for install inside the .tar pack (goodluck my friends).<br>

	if `$ systemctl status NetworkManager` respon "could not be found": 
	`$ sudo pacman -S networkmanager` <br>
  	now... you can have list of networks services via: `systemctl list-unit-files --state=enabled` and, eventually, enable it:<br>
 	`$ sudo systemctl enable NetworkManager`<br>
	`$ sudo systemctl start NetworkManager`
<br><br>

- Fix the probable Gnome Network Manager problem "lost connection" after reboot:<br>
	_way one (suggested)_:<br>
	`$ sudo systemctl restart iwd` <sup><sub>It's not strictly necessary</sub></sup><br>
	`$ sudo systemctl restart NetworkManager && nmcli device wifi list && nmcli device wifi connect YOURWIFISSIDORNAME password YOURWIFIPASSWORD`<br>
	_way complicated:_<br>
	`$ sudo systemctl enable wpa_supplicant.service`<br>
	now make or edit with `wifi.powersave=1` for disable power save [more info here](https://wiki.archlinux.org/title/Network_configuration/Wireless#Troubleshooting_drivers_and_firmware) :<br>
	for intel: `$ sudo nano /etc/modprobe.d/iwlwifi.conf` and save inside `ptions iwlwifi power_save=1`<br>
	other way: `$ sudo nano /etc/NetworkManager/conf.d/default-wifi-powersave-on.conf` (not tested, not recommended!)
<br><br>

- Now update and reboot system:<br>
	`$ sudo pacman -Syu && reboot`
<br><br>

<br><hr><br>

### POST INSTALLATION
<sup><b><i>OPTIMIZATION, ESSENTIAL EXTENSIONS, CUSTOMIZING (Gnome 4X.X)</i></b><br><br></sup>

<b>Make a pratty sudo alias</b><br>
Open terminal and copy:
`$ alias super='sudo'`<br>
`$ super whoami` if respond root, you can use super or sudo ;)<br>
add super as a sudo:<br>
`$ sudo gnome-text-editor /etc/sudoers` and add: `super ALL=(ALL:ALL) ALL` like root. Now you have complete alias for sudo.
<br><br>

<b>install pretty shell:</b><br>
- dowload [Firacode](https://www.nerdfonts.com/font-downloads) from list<br>
- copy firacode in `.local/share/fonts` (simple local, not root) and refresh fonts chache via cli `$ fc-cache -f -v`<br>
- install [starship](https://starship.rs/), open the terminal<br>
	- `$ pacman -S starship`<br>
	- `$ sudo nano ~/.bashrc`<br>
	- add line: `eval "$(starship init bash)"` and save<br>
	- add a theme like this: `$ starship preset bracketed-segments -o ~/.config/starship.toml` or [other... ](https://starship.rs/presets/)<br>
 	- end all with `$ sudo pacman -S screenfetch && clear && screenfetch` for view somethigs of beautyful
<br><br>

<b>Set Autologin:</b><br>
`$ sudo nano /etc/gdm/custom.conf`<br>
Add into file:
```
[daemon]
AutomaticLoginEnable=True
AutomaticLogin=username
```
<br>

<b>Install font manager {**Ṩ** font-manager}:</b><br>
Open console and:<br>
- `$ pacman -S font-manager `<br>
- Install/Fix Unicode Charactes:<br>
	Open Packages folder and add new fonts (make attention to not install the useless fontforge):
	- `$ git clone https://aur.archlinux.org/font-symbola.git ./symbola && cd ./symbola`<br>
	- `$ makepkg -si && cd ..`<br>
	Extra:<br>
	- `$ sudo pacman -S noto-fonts-emoji` or/and `$ sudo pacman -S ttf-font-awesome`<br>
	- `$ sudo fc-cache -f -v`
<br><br>

<b>Debloat packs:</b><br>

<top><sub><i>Note: Rscgn remove all dependencies (dangerous) of pack</i></sub></top><br>

- `$ sudo pacman -Q` <top><sub><i>(for list) (use "| grep NAMEPACK" for detect it)</i></sub></top><br>
- `$ sudo pacman -Rusn gnome-contacts`<br>
- `$ sudo pacman -Rusn gnome-maps`<br>
- `$ sudo pacman -Rusn simple-scan`<br>
- `$ sudo pacman -Rusn gnome-music`<br>
- `$ sudo pacman -Rusn gnome-font-viewer` <top><sub><i>(if you have font manager)</i></sub></top><br> 
- `$ sudo pacman -Rusn gnome-calendar`<br>
- `$ sudo pacman -Rusn gnome-tour`<br>
- `$ sudo pacman -Rusn malcontent` <top><sub><i>(parental control)</i></sub></top><br>
- `$ sudo pacman -Rusn loupe` <top><sub><i>(photo albums)</i></sub></top><br> 
- `$ sudo pacman -Rusn totem` <top><sub><i>(video player)</i></sub></top><br> 
- `$ sudo pacman -Rusn htop`<br>
- `$ sudo pacman -Rusn vim`<br>
- `$ sudo pacman -Rusn gnome-tour`<br>
- `$ sudo pacman -Rusn gnome-software` <top><sub><i>(if you use pamac)</i></sub></top><br> 
- Etc...
<br><br>


<b>Extend Gnome File shortcuts</b><br>
open `~/.config/gtk-3.0` in File and add you shortcut, for me it is:<br>
- `file:///home/master/Scrivania`<br>
- `file:///run/media/master/Projects`<br><br>
note a part... monuting a disk:
- terminal: `cd /run/media/<USERNAME>/`<br>
- terminal: `sudo mount /dev/sda1 ./Projects` or `sudo mount -t ntfs-3g /dev/sda1 ./Projects`  if it's a NTFS<br>
- `sudo nano /etc/fstab` and add `UUID=9CA24555A24534D4 /run/media/master/Projects ntfs-3g defaults 0 0`

<br><br>


<b>Expand Files (nautilus):</b><br>
> all other extensions are on [nautilus-extension in github](https://github.com/topics/nautilus-extension) and [GNOME/Files](https://wiki.archlinux.org/title/GNOME/Files) or direct in pamac!
Open console and:<br>
- `$ git clone https://aur.archlinux.org/nautilus-admin.git ./nautilus-admin` {**Ṩ** nautilus-admin}<br>
- `$ cd nautilus-admin && makepkg && nautilus -q `<br>
   _note:you can try "sudo pacman -Sy nautilus-admin && nautilus -q"_
<br><br>

<b>Essentials extensions:</b>

- AUR Packs:<br>

	- <del>pacman -S filemanager-actions</del> (currently not available)<br>

	- [Easy Effects](https://github.com/wwmm/easyeffects) {**Ṩ** easyeffects-git} <br>
	`$ git clone https://aur.archlinux.org/easyeffects-git.git ./easyeffects && cd ./easyeffects`<br>
	`$ makepkg -si && cd ..`<br>

	- [Fragments](https://flathub.org/apps/details/de.haeckerfelix.Fragments) {**Ṩ** fragments-git}<br>
	`$ git clone https://aur.archlinux.org/fragments-git.git ./fragments && cd ./fragments`<br>
	`$ makepkg -si && cd ..`<br>

	- [Impression](https://flathub.org/apps/io.gitlab.adhami3310.Impression) {**Ṩ** impression}<br>
	`$ git clone https://aur.archlinux.org/impression.git ./impression && cd ./impression`<br>
	`$ makepkg -si && cd ..`<br>

	- [google chrome](https://aur.archlinux.org/packages/google-chrome) {**Ṩ** google-chrome} (it's google standard, not [chromium](https://wiki.archlinux.org/title/chromium))<br>
	`$ git clone https://aur.archlinux.org/google-chrome.git ./google-chrome && cd ./google-chrome`<br>
	`$ makepkg -si && cd ..`<br>

	- [google chrome](https://aur.archlinux.org/packages/google-chrome) {**Ṩ** google-chrome} (it's google standard, not [chromium](https://wiki.archlinux.org/title/chromium))<br>
	`$ git clone https://aur.archlinux.org/google-chrome.git ./google-chrome && cd ./google-chrome`<br>
	`$ makepkg -si && cd ..`<br>

	- [Gradience](https://github.com/GradienceTeam/Gradience) {**Ṩ** gradience}<br>
	`$ git clone https://aur.archlinux.org/gradience.git ./gradience && cd ./gradience`<br>
	`$ makepkg -si && cd ..`<br>

 	- [Wine](https://www.winehq.org/) {**Ṩ** wine} [info install](https://wine.htmlvalidator.com/install-wine-on-arch-linux.html)<br>
	`$ sudo pacman -S wine`
<br><br>

- dev pack (if you need one, we love you!) :

	- [vscode](https://aur.archlinux.org/packages/visual-studio-code-bin) {**Ṩ** visual-studio-code-bin}<br>
	`$ git clone https://aur.archlinux.org/visual-studio-code-bin.git ./vscode && cd ./vscode`<br>
	`$ makepkg -si && cd ..`<br>
	fixing: if, on double click, vscode open the dir on desktop:<br>
	`$ xdg-mime default org.gnome.Nautilus.desktop inode/directory`

	- [nvm-desktop](https://aur.archlinux.org/nvm-desktop.git) {**Ṩ** nvm-desktop} <br>
	`$ git clone https://aur.archlinux.org/nvm-desktop.git ./nvm-desktop && cd ./nvm-desktop`<br>
	`$ makepkg -si && cd ..`<br>
	Probably it install yarn, read how to clen it [here](https://stackoverflow.com/questions/42334978/how-do-i-uninstall-yarn) and [here](https://www.reddit.com/r/archlinux/comments/hdqhea/how_do_i_uninstall_yarn/)<br>

  	- [openssl](https://www.openssl.org/) {**Ṩ** openssl} <br>
   	`$ sudo pacman -S openssl && pacman -Q openssl`

   	- [mongodb](https://www.mongodb.com/) {**Ṩ** mongosh-bin} {**Ṩ** mongodb-bin} <br>
	Install the shell:<br>
	`$ git clone https://aur.archlinux.org/mongosh-bin.git  ./mongosh && cd ./mongosh`<br>
	`$ makepkg -si && cd ..`<br>
	`$ mongosh --version`<br><br>
	Install the database:<br>
	`$ git clone https://aur.archlinux.org/mongodb-bin.git  ./mongodb && cd ./mongodb`<br>
	`$ makepkg -si && cd ..`<br>
	`$ sudo systemctl start mongodb`<br>
	`$ mongodb --version`<br><br>

- Gnome Extensions:<br>
	before all: if you use chrome need to install [gnome browser connector](https://aur.archlinux.org/packages/gnome-browser-connector) {**Ṩ** gnome-browser-connector} via AUR for extension management<br>
	`$ git clone https://aur.archlinux.org/gnome-browser-connector.git ./chrome-connector && cd ./chrome-connector`<br>
	`$ makepkg -si && cd ..`<br>

	- [Add to desktop](https://extensions.gnome.org/extension/3240/add-to-desktop/)
	- [Alt Tab Slide](https://extensions.gnome.org/extension/97/coverflow-alt-tab/)<br>
	- [Arch update alert icon](https://extensions.gnome.org/extension/1010/archlinux-updates-indicator/)<br>
	 	- note: you need to install `sudo pacnman -S pacman-contrib`, into the options remove classic command with this:<br>
		```bash
		kgx -- /bin/sh -c "echo -e \"\n***\n\nSystem Updating:\n\" && sudo pacman -Syu || echo -e \"\nNothing to update\" \ && echo -e \"\n***\n\nSnap Packs Updating:\n\" && sudo snap refresh && echo -e \"\n***\n\nFlatpack Updating:\n\" && flatpak update && echo -e \"\n***\n\nPacman Updating:\n\" && (pacman -Qdtq | grep -q .) && echo -e \"\n***\n\nPacks Cleaning:\" && sudo pacman -Rns \$(pacman -Qdtq) || echo \"Nothing to clean\" && echo -e \"\n***\n\" && echo Done - Perss Enter to exit; read && exit"
		```
	- [Bluetooth battery indicator](https://extensions.gnome.org/extension/3991/bluetooth-battery/)
	- [Bluetooth quick connect](https://extensions.gnome.org/extension/1401/bluetooth-quick-connect/)
	- [Blur my shell](https://extensions.gnome.org/extension/3193/blur-my-shell/)
	- [Burn My Windows](https://extensions.gnome.org/extension/4679/burn-my-windows/)
	- [Compact quick settings](https://extensions.gnome.org/extension/5527/compact-quick-settings/)
	- [Compiz windows effect](https://extensions.gnome.org/extension/3210/compiz-windows-effect/)
	- [Clipboard Manager](https://extensions.gnome.org/extension/779/clipboard-indicator/)
	- [Desktop (icons,drag,dock)](https://extensions.gnome.org/extension/2087/desktop-icons-ng-ding/)
	- [Just perfection](https://extensions.gnome.org/extension/3843/just-perfection/)
	- [Removable drive in menu](https://extensions.gnome.org/extension/7/removable-drive-menu/)
	- [Settings center](https://extensions.gnome.org/extension/2899/settingscenter/)
	- [Top bar organizer](https://extensions.gnome.org/extension/4356/top-bar-organizer/)
	- [Trayicons reloaded](https://extensions.gnome.org/extension/2890/tray-icons-reloaded/)
	- [User themes](https://extensions.gnome.org/extension/19/user-themes/)
	- [Vitals](https://extensions.gnome.org/extension/1460/vitals/)
	- [Weather in the clock](https://extensions.gnome.org/extension/5470/weather-oclock/)
	- [Wi-Fi Qr](https://extensions.gnome.org/extension/5416/wifi-qrcode/)
	- <del>[Blur on lockscreen](https://extensions.gnome.org/extension/2935/control-blur-effect-on-lock-screen/)</del> (native in gnome 45)
	- <del>[Desktop GTK4 (icons,drag,dock)](https://extensions.gnome.org/extension/5263/gtk4-desktop-icons-ng-ding/)</del> Bug: currently gjx libs crash
	- <del>[Day/night theme switcher](https://extensions.gnome.org/extension/4968/lightdark-theme-switcher/)</del> 2023: gnome 44.X uncompatible
	- <del>[Easy Screen Cast](https://extensions.gnome.org/extension/690/easyscreencast/)</del> (2023: native with gnome screeshot)
	- <del>[Screenshot Tool](https://extensions.gnome.org/extension/1112/screenshot-tool/)</del> (2023: native with gnome screeshot)<br>
	<del>&nbsp;&nbsp;&nbsp;&nbsp;<sup><sub>note: you need to install `sudo pacnman -S gnome-screenshot`</sub></sup></del><br>
	- <del>[No titlebar when maximized](https://extensions.gnome.org/extension/4630/no-titlebar-when-maximized/)</del> 2023: under test (optional)
	

  set all preinstalled undebloatable on OFF without Pamac Update Indicator and Removeble Drive Menu

<br>

#### Add a simple shell theme packs (it's my simple theme asset)

1) download the [theme pack](https://github.com/berto-dev/linux-arch-installation-flow/raw/main/Theme-Pack.tar.xz) and unzip it.<br><sup>extracting [original pack online](https://github.com/vinceliuice/Fluent-gtk-theme) CLI:` ./install.sh -d '/home/master/.themes' -t grey -c dark --tweaks round`</sup>

2) open Theme-Pack folder and...<br>
	- open nautilus and unlock hidden files
	- copy files of the theme into home directory
	- set in the customization (gnome tweaks>apparence) like the screenshot<br>

![arch installer partitions](https://raw.githubusercontent.com/berto-dev/linux-arch-installation-flow/main/theme.screenshot.png)<br>

- add Gradience color profile<br>
  open the app and make/save first standard colors, after it you have the forlder and can copy in it:<br>
  `$ sudo cp -r ./gradience/*  /home/YOUR_USR_NAME/.var/app/com.github.GradienceTeam.Gradience/config/presets/user`<br>
  now go in cofingurations (top right of topbar) and load "Shell-Colors"... all done.<br><br>



<br><hr><br>

### CLEANING SYSTEM

or you can install [bleachbit](https://www.bleachbit.org/download)<br>
- bleachbit AUR {**Ṩ** bleachbit-git}:<br>
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
