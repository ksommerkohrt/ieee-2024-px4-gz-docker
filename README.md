# px4-gz-docker
Docker files needed to build images for px4_sitl simulation in ROS2 and Gazebo

The `./work` directory setup 

run `./get_src.sh` to clone each repo
```
work/
┣ px4/
┣ ros2_ws/
┃ ┗ src/
┃   ┣ px4_msgs/
┃   ┣ px4-offboard/
┃   ┗ ros_gz/
┗ .gitignore
```
Please build ros_gz from source. [see ros-gz](https://github.com/gazebosim/ros_gz)


### Build and run
To build the image

`docker compose build`

To run the docker image

`./run_dev.sh`

To access the shell of each service, in two different terminals run

Terminal 1: `docker exec -u user -it px4_gz-px4_gz-1 terminator`

To start px4_sitl and ros2 offboard control, split each terminator into 3 panels and run

1. `cd px4 && make px4_sitl` to build px4_sitl first. (This only need to be built once in one of the container shells)\
`PX4_SYS_AUTOSTART=4050 PX4_GZ_WORLD=maze PX4_GZ_MODEL=x500_lidar ./build/px4_sitl_default/bin/px4` to start px4_sitl with x500 w/ lidar in maze using gz-harmonic.

2. `MicroXRCEAgent udp4 -p 8888` to start DDS agent for communication with ROS2
  
3. `cd /work/ros2_ws/ros_gz_sim_demos/launch/gpu_lidar_bridge.launch.py`

    `ros2 launch ros_gz_sim_demos lidar_bridge.launch.py`

   for easy lidar bridge and visualization


### Environment Variables
- `PX4_GZ_MODEL` Name of the px4 vehicle model to spawn in gz
- `PX4_GZ_MODEL_POSE` Spawn pose of the vehicle model, must used with `PX4_GZ_MODEL`
- `PX4_MICRODDS_NS` Namespace assigned to the sitl vehicle, normally associated with px4 instances, but can be set manually
- `ROS_DOMAIN_ID` Separate each container into its own domain 
  
