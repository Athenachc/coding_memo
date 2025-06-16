# Docker

### Install
[Install Docker Engine on Ubuntu](https://docs.docker.com/engine/install/ubuntu/)

### Cheatsheet
```
docker image pull {image_name} # pull an image
docker run -blah_blah {image_name} # run an image and create a container
docker container ps -a # list all container
docker image ls # list all image

docker start {container_name} # start container
docker attach {container_name} # attach to a container, namely, get inside the container
docker exec -it {container_name} /bin/bash # attach to the same container without echoing the same commandline
ctrl + p then ctrl + q to detach from docker
exit # exit container

docker commit {container_name} {new_image_name} 
# create an image after you modify a container
# this could become your new template

docker rm {container_name}
docker rmi {image_name}

docker tag {container_name} {username}/{remote_image_name}
docker push {username}/{remote_image_name}
# basically allow you to publish your image
```

Use docker for e2es’ Gazebo
```
docker ps -a
docker start “eloquent_spence”
docker attach “eloquent_spence”
roscd e2es
./sim.sh
```

Use docker on SAV
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

