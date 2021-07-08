1. Install nvidia-docker
	1. Check nouveau & do blacklist it
		1. `lsmod | grep nouveau`
		2. If you can see the list of "nouveau", follow it, if not, ignore it
		3. Create blacklist file
		4. `sudo nano /etc/modprobe.d/blacklist-nouveau.conf `
		5. Writhe under lines
		```
		blacklist nouveau 
		options nouveau modeset=0
		```
		6. `sudo update-initramfs -u `
		7. `sudo service gdm stop `
	2. Install ubuntu driver
		1. `sudo add-apt-repository ppa:graphics-drivers `
		2. `sudo apt-get update `
		3. You can check now the available nvidia-driver version at "software & Updates" app
		4. Move to "Additional Drivers" tap
		5. `sudo apt-get install nvidia-driver-460` (if you want to install "460" version)
		6. `sudo reboot`
		7. After reboot, check installation `$ nvidia-smi`
	3. Install nvidia-docker (refer. https://docs.nvidia.com/datacenter/cloud-native/container-toolkit/install-guide.html#docker)
		1. `sudo apt-get update`
		2. `sudo apt-get install -y apt-transport-https ca-certificates curl gnupg-agent software-properties-common`
		3. `curl https://get.docker.com | sh && sudo systemctl --now enable docker`
		```
		distribution=$(. /etc/os-release;echo $ID$VERSION_ID) \
   && curl -s -L https://nvidia.github.io/nvidia-docker/gpgkey | sudo apt-key add - \
   && curl -s -L https://nvidia.github.io/nvidia-docker/$distribution/nvidia-docker.list | sudo tee /etc/apt/sources.list.d/nvidia-docker.list
   		```
   		4. `sudo apt-get update`
   		5. `sudo apt-get install -y nvidia-docker2`
   		6. `sudo systemctl restart docker`
   		7. Finally check installation `$ sudo docker run --rm --gpus all nvidia/cuda:11.0-base nvidia-smi`
	4. Docker post-installation (refer. https://docs.docker.com/engine/install/linux-postinstall/)
		1. `sudo groupadd docker`
		2. `sudo usermod -aG docker $USER`
		3. Reboot


2. Setup docker for CUDA+JUPYTER+GYM+VNC+TENSORFLOW+PYTORCH
	* Notice, command for remove all images and container 
	```
	docker stop $(docker ps -a -q)
	docker rm $(docker ps -a -q)
	docker rmi $(docker images -q) 
	```
	1. Setup docker which contains cuda10.1 cudnn7.6
	* Follow https://github.com/mkpark2017/Docker_cuda_cudnn/tree/main/CUDA10.1
	2. Setup docker containing gym+jupyter+vnc+tensorflow+pytorch
	* Follow https://github.com/mkpark2017/Docker_cuda_cudnn/tree/main/GYM_VNC


3. Test an example pytorch code and tensorboard
	1. Let's use jupyter. Open browser (e.g., google chrome) and put `0.0.0.0:8888` on url
	2. Run `example.ipynb`
	3. Check the result on tensorboard
		1. Open new terminal
		2. Execute docker
		```
		docker exec -it mk_gym bash
		```
		3. `cd /notebook`
		4. `tensorboard --logdir=runs --port 6006 --host=0.0.0.0`
		5. Open new browser and put `0.0.0.0:6006` on url

4. VNC will be used for ROS and Gazebo later (not updated all yet)
	1. Download VNC viewer from https://www.realvnc.com/en/connect/download/viewer/
	2. Install and run it
	3. Put `0.0.0.0:5900` on url
