# nvidia driver:

I don't know why but sometimes the arch installation don't follow the customization and install the open source nouveau nvidia driver. This is a simple process cli to install fix the wrong installation.

- install official driver:<br>
  `$ sudo pacman -S nvidia nvidia-utils`<br>

- remove old driver:<br>
  `$ sudo nano /etc/modprobe.d/blacklist-nouveau.conf` now write inside: `blacklist nouveau`<br>
  `$ sudo mkinitcpio -p linux`<br>

- reboot and:<br>
  `nvidia-smi` to confirm process

--- 

The actions is terrible dangerous... in case of disaster you can try:

-  `$ sudo mkinitcpio -P`
-  `$ lspci -k | grep -A 2 -E "(VGA|3D)"`
-  `$ sudo modprobe nouveau`
-  `$ lsmod | grep nouveau`
-  `$ sudo nano /etc/modules` and add `nouveau`
