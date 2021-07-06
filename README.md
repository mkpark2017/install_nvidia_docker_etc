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
		7. After reboot, check installation `$ nvidia-smi`
	3. Install nvidia-docker (refer. https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)
		1. `$ sudo apt-get update`
		2. `$ sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common`
		3. `$ curl https://get.docker.com | sh && sudo systemctl --now enable docker`
		4. `$ distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list`
   		5. `$ sudo apt-get update`
   		6. `$ sudo apt-get install -y nvidia-docker2`
   		7. `$ sudo systemctl restart docker`
   		8. Finally check installation `$ sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi`
	4. Docker post-installation (refer. https://docs.docker.com/engine/install/linux-postinstall/)
		1. `$ sudo groupadd docker`
		2. `$ sudo usermod -aG docker $USER`
		3. Reboot
2. Setup docker for CUDA+JUPYTER+OPENAI+VNC
* Notice, command for remove all images and container 


$ docker stop $(docker ps -a -q)
$ docker rm $(docker ps -a -q)
$ docker rmi $(docker images -q) 


	1. Setup docker with cuda10.1 cudnn7.6
	Follow 
