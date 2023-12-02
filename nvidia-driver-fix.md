# nvidia driver:

I don't know why but sometimes the arch installation don't follow the customization and install the open source nouveau nvidia driver. This is a simple process cli to install fix the wrong installation.

- install official driver:<br>
  `$ sudo pacman -S nvidia nvidia-utils`<br>

- remove old driver:<br>
  `$ echo "blacklist nouveau" | sudo tee /etc/modprobe.d/blacklist-nouveau.conf`<br>
  `$ sudo mkinitcpio -p linux`<br>

- reboot and:<br>
  `nvidia-smi` to confirm process
