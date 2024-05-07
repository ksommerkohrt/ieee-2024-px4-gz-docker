Step 1 set up work folder:

`./get_src.sh`

`cd ~/ieee-2024-px4-gz-docker/work/ros2_ws`

`rosdep install -r --from-paths src -i -y --rosdistro humble`

`source /opt/ros/humble/setup.bash`

`colcon build`

Step 2 set up docker:

`cd ~/ieee-2024-px4-gz-docker`

`docker pull melodyliyulin/ieee-2024-px4-gz-docker:latest`

`docker image tag melodyliyulin/ieee-2024-px4-gz-docker:latest px4_gz`


Step 3 run docker image

`cd ~/ieee-2024-px4-gz-docker`

`./run_dev.sh`

Open a new terminal into the same folder

`cd ~/ieee-2024-px4-gz-docker`

`docker exec -u user -it px4_gz-px4_gz-1 terminator`

Step 4 

open 4 terminals in docker image 

In terminal 1:

`cd ~/work/px4`

` make px4_sitl`

`PX4_SYS_AUTOSTART=4050 PX4_GZ_WORLD=maze PX4_GZ_MODEL=x500_lidar ./build/px4_sitl_default/bin/px4`

In terminal 2:

`cd ~/work/`

`MicroXRCEAgent udp4 -p 8888`

In terminal 3:

`cd ~/work/ros2_ws`

`source install/setup.bash`

`ros2 launch ros_gz_sim_demos lidar_bridge.launch.py`

In terminal 4: (to verify bridge is working)

`cd ~/work/ros2_ws`

`source install/setup.bash`

`ros2 topic echo lidar/points`


   
