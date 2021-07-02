1. Install nvidia-docker
	1. Check nouveau & do blacklist it
		1. `$ lsmod | grep nouveau`
		\
		2. If you can see the list of "nouveau", follow it, if not, ignore it
		3. Create blacklist file
		4. `$ sudo nano /etc/modprobe.d/blacklist-nouveau.conf `
		5. Writhe under lines
		```
		blacklist nouveau 
		options nouveau modeset=0
		```
		6. `$ sudo update-initramf -u `
		7. `$ sudo service gdm stop `
	2. Install ubuntu driver
		1. `$ sudo add-apt-repository ppa:graphics-drivers `
		2. `$ sudo apt-get update `
		3. You can check now the available nvidia-driver version at "software & Updates" app
		4. Move to "Additional Drivers" tap
		5. `$ sudo apt-get install nvidia-driver-460` (if you want to install "460" version)
		6. `$ sudo reboot`
	3.
