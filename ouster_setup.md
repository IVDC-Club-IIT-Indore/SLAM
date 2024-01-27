## Installing Ouster ROS drivers

### ROS 2 Setup

Follow ``https://github.com/ouster-lidar/ouster-ros/blob/ros2/README.md``

Hostname: ``os-122333000772.local``

Error1 : Couldn't resolve hostname 

Solution: ``https://github.com/ouster-lidar/ouster_example/issues/137#issuecomment-578435555``


0 points from 0 msg( in rviz ) 
soln: 
1. the ref frame of grid & pointcloud2d should be set to os_sensor  
2. the fixed framed should also be os_sensor
