# RosBot (An Autonomous Navigation Ambition Project)

## Quick Start
This is a quick start guide for running our project in your system
This Repo contains launch files for Gmapping, Hector Map and Rtab Map SLAM Algorithms. 
It also includes launch files for Gazebo simulations as well as Real-time hardware implementation.

ROS installation link - http://wiki.ros.org/kinetic/Installation/Ubuntu  (Desktop-Full Install)

If you are new to ROS please refer ROS wiki page-http://wiki.ros.org/ROS/Tutorials

Install the following dependencies to run this project

`$ sudo apt-get update`

`$ sudo apt-get install ros-kinetic-slam-gmapping`

`$ sudo apt-get install ros-kinetic-hector-slam`

`$ sudo apt-get install ros-kinetic-rtabmap-ros`

`$ sudo apt-get install ros-kinetic-teleop-twist-keyboard`

 To run this project on Melodic version just replace 'kinetic' with 'melodic'.
 
 
Now that we have installed ROS and are ready with our dependencies,firstly download the 'mybot_ws' workspace from the simulation   directory.
 
 create a catkin package by running the below command in a terminal
 
 `$ cd ~/mybot_ws/src`
 
 copy paste the contents form the src to your src folder just created in your PC, and run the following commands
 
  `$ cd ~/mybot_ws`
 
  `$ catkin_make`
 
 The above command 'catkin_make' will build you workspace. Now you are all set to run the simulation
 
 If you close the terminal do the following

 `$ source /opt/ros/kinetic/setup.bash`

 `$ cd ~/mybot_ws`

 `$ source /devel/setup.bash`

**_Add these in .bashrc file for single system ROS implementation_**

export ROS_MASTER_URI=http://localhost:11311/

export ROS_HOSTNAME=localhost

**_Add these in .bashrc file for multi system ROS implementation_**

export ROS_MASTER_URI=http://*<HOS_IP_ADDRESS>*/

export ROS_HOSTNAME=*<HOS_IP_ADDRESS>*

export ROS_IP=*<HOS_IP_ADDRESS>*


```diff
- RUNNING ROSCORE IN THE BACKGROUND IS EXTREAMLY IMPORTANT
```


## STEP FOR RUNNING SIMULATION
 
 #### *GMAPPING*
 
 **Creating the Map**

Run the following commands below. Use the teleop to move the robot around to create an accurate and thorough map.

In Terminal 1, launch the Gazebo world

`roslaunch mybot_gazebo mybot_world.launch`

In Terminal 2, start map building

`roslaunch mybot_navigation gmapping_demo.launch`


In Terminal 3, launch rviz and set the following parameters:

`roslaunch mybot_description mybot_rviz_gmapping.launch`


In Terminal 4, start teleop

`rosrun teleop_twist_keyboard teleop_twist_keyboard.py`


**Saving the Map**

In Terminal 5, save the map to some file path

`rosrun map_server map_saver -f ~/mybot_ws/src/mybot_navigation/maps/test_map`


**Loading the Map followed by localization**

Close all previous terminals and run the following commands below. Once loaded, use rviz to set navigation waypoints and the robot should move autonomously.

In Terminal 1, launch the Gazebo world

`roslaunch mybot_gazebo mybot_world.launch`


In Terminal 2, start map building

`roslaunch mybot_navigation amcl_demo.launch`


In Terminal 3, launch rviz

`roslaunch mybot_description mybot_rviz_amcl.launch`




#### *HECTOR MAPPING*

**Creating the Map**

Run the following commands below. Use the teleop to move the robot around to create an accurate and thorough map.

In Terminal 1, launch the Gazebo world

`roslaunch mybot_gazebo mybot_world.launch`

In Terminal 2, start map building

`roslaunch mybot_navigation tutorial.launch`


In Terminal 3, launch rviz and set the following parameters:

`roslaunch mybot_description mybot_rviz_gmapping.launch`


In Terminal 4, start teleop

`rosrun teleop_twist_keyboard teleop_twist_keyboard.py`


**Saving the Map**

In Terminal 5, save the map to some file path

`rosrun map_server map_saver -f ~/mybot_ws/src/mybot_navigation/maps/hector_map`


**Loading the Map followed by localization**

Close all previous terminals and run the following commands below. Once loaded, use rviz to set navigation waypoints and the robot should move autonomously.

In Terminal 1, launch the Gazebo world

`roslaunch mybot_gazebo mybot_world.launch`


In Terminal 2, start map building

`roslaunch mybot_navigation amcl_demo.launch`


In Terminal 3, launch rviz

`roslaunch mybot_description mybot_rviz_amcl.launch`




### *RTAB MAPPING*

**Creating the Map**

Run the following commands below. Use the teleop to move the robot around to create an accurate and thorough map.

In Terminal 1, launch the Gazebo world

`roslaunch mybot_gazebo mybot_world.launch`

In Terminal 2, start map building

`roslaunch mybot_navigation rtab.launch`


In Terminal 3, launch rviz and set the following parameters:

`roslaunch mybot_description mybot_rviz_gmapping.launch`


In Terminal 4, start teleop

`rosrun teleop_twist_keyboard teleop_twist_keyboard.py`


**Saving the Map**

Map server is not required in RTAB-MAP 


**Loading the Map followed by localization**

Close all previous terminals and run the following commands below. Once loaded, use rviz to set navigation waypoints and the robot should move autonomously.

In Terminal 1, launch the Gazebo world

`roslaunch mybot_gazebo mybot_world.launch`


In Terminal 2, start map building

`roslaunch mybot_navigation rtab.launch localization:=true`


In Terminal 3, launch rviz

`roslaunch mybot_description mybot_rviz_amcl.launch`


## STEPS FOR RUNNING REAL TIME EXPERIMENTATION

 ### *GMAPPING*
 
 **Creating the Map**

Run the following commands below. Use the teleop to move the robot around to create an accurate and thorough map.

In Terminal 1, launch the RPLidar launch file (IN RPi3 remote SLAVE PC)

`roslaunch rplidar_ros view_rplidar.launch`

In Terminal 2, launch the Arduino bridge launch file (IN RPi3 remote SLAVE PC)

`roslaunch ros_arduino_python arduino.launch`

In Terminal 3, start map building (IN MASTER PC)

`roslaunch rosbot_navigation gmapping_demo.launch`


In Terminal 4, launch rviz and set the required parameters (IN MASTER PC)

`roslaunch rosbot_urdf rviz.launch`


In Terminal 5, start teleop (IN MASTER PC)

`rosrun teleop_twist_keyboard teleop_twist_keyboard.py`


**Saving the Map**

In Terminal 6, save the map to some file path (IN MASTER PC)

`rosrun map_server map_saver -f ~/gmap_rt_ws/src/mybot_navigation/maps/test_map`


**Loading the Map followed by localization**

Close all previous terminals and run the following commands below. Once loaded, use rviz to set navigation waypoints and the robot should move autonomously.

In Terminal 1, launch the RPLidar launch file (IN RPi3 remote SLAVE PC)

`roslaunch rplidar_ros view_rplidar.launch`

In Terminal 2, launch the Arduino bridge launch file (IN RPi3 remote SLAVE PC)

`roslaunch ros_arduino_python arduino.launch`


In Terminal 3, start map building

`roslaunch rosbot_navigation amcl_demo.launch`


In Terminal 4, launch rviz and set the required parameters (IN MASTER PC)

`roslaunch rosbot_urdf rviz.launch`



### *HECTOR MAP*
 
 **Creating the Map**

Run the following commands below. Use the teleop to move the robot around to create an accurate and thorough map.

In Terminal 1, launch the RPLidar launch file (IN RPi3 remote SLAVE PC)

`roslaunch rplidar_ros view_rplidar.launch`

In Terminal 2, launch the Arduino bridge launch file (IN RPi3 remote SLAVE PC)

`roslaunch ros_arduino_python arduino.launch`

In Terminal 3, start map building (IN MASTER PC)

`roslaunch rosbot_navigation tutorial.launch`


In Terminal 4, launch rviz and set the required parameters (IN MASTER PC)

`roslaunch rosbot_urdf rviz.launch`


In Terminal 5, start teleop (IN MASTER PC)

`rosrun teleop_twist_keyboard teleop_twist_keyboard.py`


**Saving the Map**

In Terminal 6, save the map to some file path (IN MASTER PC)

`rosrun map_server map_saver -f ~/gmap_rt_ws/src/mybot_navigation/maps/hector_map`


**Loading the Map followed by localization**

Close all previous terminals and run the following commands below. Once loaded, use rviz to set navigation waypoints and the robot should move autonomously.

In Terminal 1, launch the RPLidar launch file (IN RPi3 remote SLAVE PC)

`roslaunch rplidar_ros view_rplidar.launch`

In Terminal 2, launch the Arduino bridge launch file (IN RPi3 remote SLAVE PC)

`roslaunch ros_arduino_python arduino.launch`


In Terminal 3, start map building

`roslaunch rosbot_navigation amcl_demo.launch`


In Terminal 4, launch rviz and set the required parameters (IN MASTER PC)

`roslaunch rosbot_urdf rviz.launch`




### *RTAB-MAP*
 
 **Creating the Map**

Run the following commands below. Use the teleop to move the robot around to create an accurate and thorough map.

In Terminal 1, launch the RPLidar launch file (IN RPi3 remote SLAVE PC)

`roslaunch rplidar_ros view_rplidar.launch`

In Terminal 2, launch the Arduino bridge launch file (IN RPi3 remote SLAVE PC)

`roslaunch ros_arduino_python arduino.launch`

In Terminal 3, launch the kinect depth camera  launch file (IN RPi3 remote SLAVE PC)

`sudo chmod 777 -R /dev/bus/usb` (one time use ,before running the launch file)

`roslaunch freenect_launch freenect.launch depth_registration:=true data_skip:=2`


In Terminal 4, start map building (IN MASTER PC)

`roslaunch rosbot_navigation rtab.launch`


In Terminal 5, launch rviz and set the required parameters (IN MASTER PC)

`roslaunch rosbot_urdf rviz.launch`


In Terminal 6, start teleop (IN MASTER PC)

`rosrun teleop_twist_keyboard teleop_twist_keyboard.py`


**Saving the Map**

Map server is not required in RTAB-MAP 


**Loading the Map followed by localization**

Close all previous terminals and run the following commands below. Once loaded, use rviz to set navigation waypoints and the robot should move autonomously.

In Terminal 1, launch the RPLidar launch file (IN RPi3 remote SLAVE PC)

`roslaunch rplidar_ros view_rplidar.launch`

In Terminal 2, launch the Arduino bridge launch file (IN RPi3 remote SLAVE PC)

`roslaunch ros_arduino_python arduino.launch`

In Terminal 3, launch the kinect depth camera  launch file (IN RPi3 remote SLAVE PC)

`sudo chmod 777 -R /dev/bus/usb` (one time use ,before running the launch file)

`roslaunch freenect_launch freenect.launch depth_registration:=true data_skip:=2`


In Terminal 3, start map building (IN MASTER PC)

`roslaunch rosbot_navigation rtab.launch localization:=true`


In Terminal 4, launch rviz and set the required parameters (IN MASTER PC)

`roslaunch rosbot_urdf rviz.launch`











