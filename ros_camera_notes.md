### install ROS noetic
### see https://linoxide.com/how-to-install-ros-noetic-on-ubuntu-20-04/ and https://idroot.us/install-ros-noetic-ubuntu-20-04/ and http://wiki.ros.org/noetic/Installation/Ubuntu

### update systems first
  `sudo apt update`
  `sudo apt upgrade`
### add ROS repository to Ubuntu
  `echo "deb http://packages.ros.org/ros/ubuntu focal main" | sudo tee /etc/apt/sources.list.d/ros-focal.list`
### add ROS keyring
  `sudo apt-key adv --keyserver 'hkp://keyserver.ubuntu.com:80' --recv-key C1CF6E31E6BADE8868B172B4F42ED6FBAB17C654`
### update package list and install software
  `sudo apt update`
  `sudo apt install ros-noetic-desktop-full`
### enter <y> to continue
### set up environment details
  `echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc`
  `source ~/.bashrc`
### check if installed properly
  `roscd`

### Setup your computer to accept software from packages.ros.org.
  `sudo sh -c 'echo "deb http://packages.ros.org/ros/ubuntu $(lsb_release -sc) main" > /etc/apt/sources.list.d/ros-latest.list`
  `sudo apt install curl` # if you haven't already installed curl
  `curl -s https://raw.githubusercontent.com/ros/rosdistro/master/ros.asc | sudo apt-key add -`
### source this script in every bash terminal you use ROS in.
  `source /opt/ros/noetic/setup.bash`
### automatically source this script every time a new shell is launched
  `echo "source /opt/ros/noetic/setup.bash" >> ~/.bashrc`
  `source ~/.bashrc`
### To install this tool and other dependencies for building ROS packages
  `sudo apt install python3-rosdep python3-rosinstall python3-rosinstall-generator python3-wstool build-essential`
### install rosdep
  `sudo apt install python3-rosdep`
  `sudo rosdep init`
  `rosdep update`
  
### install ROS camera controller
### based on https://github.com/basler/pylon-ros-camera and http://wiki.ros.org/catkin/commands/catkin_make 
### create new directory to receive contents of repository 
```mkdir catkin_ws
   cd catkin_ws
  catkin_make
```
### OR, if that doesn't work:
```
  cd ~/catkin_ws
  cd src
  catkin_init_workspace
  cd ..
  mkdir build
  cd build
  cmake ../src -DCMAKE_INSTALL_PREFIX=../install -DCATKIN_DEVEL_PREFIX=../devel
  

### if error message 'problem with cmake_cxx_compiler'
  sudo apt-get install build-essential
  suod ap-get install g++
 ### then retry above cmake code
  
  
```
### clone repository 
  `cd ~/catkin_ws/src && git clone https://github.com/basler/pylon-ros-camera`
### optional - clone messages 
  `git clone https://github.com/dragandbot/dragandbot_common.git`
### install ROS dependencies (note change from path . to path src in code)
```
sudo sh -c 'echo "yaml https://raw.githubusercontent.com/basler/pylon-ros-camera/master/pylon_camera/rosdep/pylon_sdk.yaml" > /etc/ros/rosdep/sources.list.d/30-pylon_camera.list' && rosdep update && sudo rosdep install --from-paths src --ignore-src --rosdistro=$ROS_neotic -r -y
```

### compile workspace `cd ~/catkin_ws && catkin_make clean && catkin_make && source ~/.bashrc`
### OR
  `cd ~/catkin_ws && catkin clean -y && catkin build && source ~/.bashrc`
### specify the catkin_ws in the .bashrc
  `nano ~/.bashrc`
### add <source ~/catkin_ws/devel/setup.bash> #save and exit bash

### to check .bashrc file
  `sudo gedit ~/.bashrc`
  
### install catkin-tools dependency (unlinked in Ubuntu 20.04 so it has to be manually specified to be installed)
  `sudo apt install python3-catkin-tools python3-osrf-pycommon`
  `sudo apt-get install ros-noetic-catkin python3-catkin-tools`
  
### Camera can be configured 2 ways
  `roslaunch pylon_camera pylon_camera_ip_configuration.launch`
### OR
### by opening config file in GUI
### home -- catkin_ws -- src -- pylon-ros-camera -- pylon_camera -- config -- default.yaml
### to change from any default parameters, uncomment line for that parameter and modify details (e.g, #frame_rate: 10 --> frame_rate: 50)
### changes will not show in viewer until you relaunch ROS

 
### .
### Using ROS for imaging and recording with Baylor camera
### open new terminal & start ROS
  `roscore`

### open 2nd terminal (or new tab in terminal with <Shift Ctl t>)
### plug in camera using USB
  `roslaunch pylon_camera pylon_camera_node.launch`

### open another new terminal to open viewer
  `rqt`

### exit ROS when finished using < Ctl c >


