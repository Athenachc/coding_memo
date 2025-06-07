Gazebo with PX4 (airo_control)
```
cd PX4-Autopilot
make px4_sitl_default gazebo

roscd airo_px4/launch
roslaunch px4_sitl.launch 

roscd airo_px4/launch
roslaunch gazebo_fsm.launch

rosrun airo_px4 example_mission_node
```
