To get started -


https://github.com/IVDC-Club-IIT-Indore/SLAM/assets/104747561/90d546af-9987-41ea-b4dc-346d2035e11c



1. Run the following nodes in each case in different terminals
-----------------------------------------------------------------------------------------------------------
   CASE 1: real lidar is used

- dynamic binding(assuming the ouster is setup using the instructions in ouster_setup.py)
   `sudo dnsmasq -C /dev/null -kd -F 192.168.5.50,192.168.5.100 -i <name of your ethernet port eg. eth0 or enp43s0> --bind-dynamic`
- wait till the host name appears in the terminal ( around 15-30 sec)
- the lidar driver node `ros2 launch ouster_ros driver.launch.py`
- ros2 launch kiss_icp odometry.launch.py topic:=topic_pts ( replace topic_pts appropriately)

----------------------------------------------------------------------------------------------------------
   CASE 2 : rosbags for imu/ points / tf topic 
- play the rosbag ( make sure to check the topic over which points are published say topic_pts)
- ros2 launch kiss_icp odometry.launch.py topic:=topic_pts ( replace topic_pts appropriately)
