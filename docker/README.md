# Docker

## Install
- [Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)
- [Linux post-installation steps for Docker Engine](https://docs.docker.com/engine/install/linux-postinstall/)
- **DON'T** need to install Docker Desktop unless you know what you are doing.

## Docker with GPU
If `--gpus all` fails despite working nvidia-smi, check if your Docker installation is missing NVIDIA Container Toolkit (nvidia-docker2). \
Without it, Docker cannot forward GPU devices into containers even if your host has a GPU.

- Install NVIDIA Container Toolkit
```
# 1. Define your distribution (ensure it is correct)
distribution=$(. /etc/os-release;echo $ID$VERSION_ID)
echo $distribution  # should print ubuntu22.04

# 2. Add NVIDIA GPG key
curl -s -L https://nvidia.github.io/libnvidia-container/gpgkey | sudo apt-key add -

# 3. Add the repository list
curl -s -L https://nvidia.github.io/libnvidia-container/$distribution/libnvidia-container.list | sudo tee /etc/apt/sources.list.d/nvidia-container.list

# 4. Update package lists
sudo apt-get update

# 5. Install NVIDIA Container Toolkit
sudo apt-get install -y nvidia-docker2

# 6. Restart Docker daemon to apply changes
sudo systemctl restart docker
```
- Verify installation
  After restarting Docker, confirm integration:
```
sudo docker run --rm --gpus all nvidia/cuda:12.0.0-base-ubuntu22.04 nvidia-smi
```

## Solution of missing `xclock` inside container
1. On host, run:
  ```
  echo $DISPLAY
  ```
  Your terminal should output `:0` or `:0.0`.
  Then run:
  ```
  xhost +
  ```
  *Note: This disables all access control (unsafe on shared systems).* 
  
  For safer use:
  ```
  xhost +local:docker
  ```

2. Check if your container has `x11-apps` installed or not
   Inside container, check:
   ```
   sudo apt update
   sudo apt install -y x11-apps
   xclock
   ```
   
## Cheatsheet
```
docker image pull {image_name} # Pull an image
docker run -blah_blah {image_name} # Run an image and create a container
docker container ps -a # List all containers
docker image ls # List all images

docker start {container_name} # Start container
docker attach {container_name} # Attach to a container, namely, get inside the container
docker exec -it {container_name} /bin/bash # Attach to the same container without echoing the same commandline
ctrl + p then ctrl + q to detach from docker
exit # exit container

docker commit {container_name} {new_image_name} 
# Create an image after you modify a container
# This could become your new template

docker rm {container_name}
docker rmi {image_name}

docker tag {container_name} {username}/{remote_image_name}
docker push {username}/{remote_image_name}
# Allow you to publish your image

echo "export PS1='root@<container_name>:\w# '" >> ~/.bashrc
source ~/.bashrc
# Display your container name 
```

### Use docker for e2es’ Gazebo
```
docker ps -a
docker start “eloquent_spence”
docker attach “eloquent_spence”
roscd e2es
./sim.sh
```

### Use docker on SAV
```
roscd airo_px4/launch
roslaunch mavros_ardu.launch

roscd airo_px4/launch
roslaunch vicon.launch


rosrun mavros mavsys rate --all 50
rostopic hz /mavros/local_position/pose

rostopic echo /mavros/rc/in

roslaunch airo_px4 airo_px4_fsm_vicon.launch

rosrun airo_px4 example_mission_node
```

