# ChatRTLinuX
Docker-based solution to run ChatRTX on Linux. Tested in Arch (btw).

# !!!WARNING!!!
# this is an unfinished work in progress. if you can see this message <--, this does NOT work (yet).

# Why doesn't NVidia provide default linux support for ChatRTX?

man i got no clue

anyways here's a quick and dirty dockerized solution very much plaigarized from noahc1510:
https://github.com/noahc1510/trt-llm-rag-linux

i run arch (btw) and can't (don't want to figure out how to) work with .deb files soooo i made a dockerized version of this solution <3


# How do I use this?

installation is simple:
# dependencies:
1. install docker and the latest nvidia drivers: ```sudo pacman -Syu docker nvidia nvidia-utils # you MIGHT not need nvidia-utils but it's generally recommended```

2. enable/start docker: ```sudo systemctl enable docker && sudo systemctl start docker```

3. add your user to the docker group so you don't have to use sudo with docker (optional): ```sudo usermod -aG docker $USER```
# GPU passthrough into docker:
4. install the nvidia-container-toolkit via yay or paru ```yay -S nvidia-container-toolkit```

4.5 if you don't have or know what yay is: https://itsfoss.com/install-yay-arch-linux/

5. ensure your ```/etc/docker/daemon.json``` file looks the same as daemon.json in the repo (feel free to copy & paste it)

6. reboot if this is your first time installing drivers (you monster)

6.5 if you aren't rebooting, restart docker: ```sudo systemctl restart docker```

7. verify this worked: ```sudo docker run --gpus all nvidia/cuda:12.8.0-cudnn-devel-ubuntu22.04``` and you should see your GPU information in docker. neato burrito!
# prep your files:


copy the dockerfile to ~/AI (or any directory of your choice)

cd to AI

build the container: ```docker build -t tensorrt-llm:latest .```

