## Installing Cartographer ROS with ROS Noetic

On Ubuntu Focal with ROS Noetic use these commands to install the above tools:

```
sudo apt-get update
sudo apt-get install -y python3-wstool python3-rosdep ninja-build stow
```

    

After the tools are installed, create a new cartographer_ros workspace in 'catkin_ws'.

```
mkdir catkin_ws
cd catkin_ws
wstool init src
wstool merge -t src https://raw.githubusercontent.com/cartographer-project/cartographer_ros/master/cartographer_ros.rosinstall
```
Add Ceres Solver to `./src/.rosinstall` as:

```
- git:
    local-name: cartographer
    uri: https://github.com/cartographer-project/cartographer.git
    version: master
- git:
    local-name: cartographer_ros
    uri: https://github.com/cartographer-project/cartographer_ros.git
    version: master
- git:
    local-name: ceres-solver
    uri: https://github.com/ceres-solver/ceres-solver.git
```
Install the packages by running: 
```
wstool update -t src
```

Remove the dependency `libabsl-dev` in `src/cartographer/package.xml` by removing the line `depend>libabsl-dev</depend>`.

Now you need to install cartographer_ros dependencies.
First, we use `rosdep` to install the required packages.

```
sudo rosdep init
rosdep update
rosdep install --from-paths src --ignore-src --rosdistro=${ROS_DISTRO} -y
```

Cartographer uses the `abseil-cpp` library that needs to be manually installed using this script:

```
src/cartographer/scripts/install_abseil.sh
```

Jinja may throw errors due to a version mismatch. So install the right version by 
```
pip3 uninstall jinja2 && pip3 install jinja2==3.0.3
```

Finally build and install.

```
catkin_make_isolated --install --use-ninja
```

To test the installation first source the setup file:
```
source install_isolated/setup.bash
```
Run Cartographer SLAM on a 2D demo bag

```
wget -P ~/Downloads https://storage.googleapis.com/cartographer-public-data/bags/backpack_2d/cartographer_paper_deutsches_museum.bag

roslaunch cartographer_ros demo_backpack_2d.launch bag_filename:=${HOME}/Downloads/cartographer_paper_deutsches_museum.bag
```



