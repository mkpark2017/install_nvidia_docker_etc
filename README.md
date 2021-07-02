1. Install nvidia-docker
	1. check nouveau & do blacklist it
		1. `$ lsmod | grep nouveau`
		\
		2. If you can see the list of "nouveau"
		3. Create blacklist file
		4. `$ sudo nano /etc/modprobe.d/blacklist-nouveau.conf `
		5. Writhe under lines
		6. ```
		blacklist nouveau 
		options nouveau modeset=0
		```
