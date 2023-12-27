# Docker-Image-for-ROS-Noetic-with-Kinect-GUI

This Docker image is tailored for running ROS1 Noetic with support for GUI applications and the Xbox 360 Kinect Depth Camera. It includes tools such as RViz, Gazebo, and the ability to view the Kinect's depth camera feed using RViz.

## Usage

#### Build the Docker Image

```bash
 docker build -t noetic_working -f Dockerfile-ros-noetic .
```
#### Run the Docker Container
```bash
 docker run -it --name noetic-container --user vipul --ipc=host --privileged -v /dev:/dev -v /sys:/sys -v /tmp/.X11-unix:/tmp/.X11-unix:rw --env=DISPLAY noetic_working
```
> Change vipul with --> your_user_name

#### To Start an exited Docker container 
```bash
docker start -ai noetic-container
```

#### To access another Docker Container Shell
```bash
docker exec -it noetic-container /bin/bash
```
<br/>

## Some Common Problems & their Solutions:

#### 1. bash: rviz: command not found
  This error occurs when bash cannot find RViz. To solve this, source the underlay:
  ```bash
   source /opt/ros/noetic/setup.bash
  ```
 #### 2. catkin_make Permission Denied
  This occurs as non-root doesn't have access to our workspace
  To give access to non-root users, enter the following command
  ```bash
   sudo chown -R vipul:vipul /home/vipul/catkin_ws
  ```
  >  Change vipul with --> your_user_name

  
 #### 3. RLException: [freenect.launch] is neither a launch file in package [freenect_launch] nor is [freenect_launch] a launch file name. The traceback for the exception was written to the log file
	
  Source the catkin workspace setup file:
  
  ``` bash
  source ~/catkin_ws/devel/setup.bash
  ```
  Note: This works only if the non-root user has access to the catkin workspace.


#### 4. Error building freenect_stack - Resource not found: rgbd_launch
  
  > Resource not found: rgbd_launch <br/>
	  ROS path [0]=/opt/ros/noetic/share/ros <br/>
	  ROS path [1]=/home/inaciose/catkin_ws/src <br/>
	  ROS path [2]=/opt/ros/noetic/share <br/>
	  The traceback for the exception was written to the log file <br/>
  ```bash
   sudo apt-get install ros-noetic-rgbd-launch
  ```

#### 5: If the packages are not found, update the package list:

  ```bash
   sudo apt-get update
  ```

## Credits
Special thanks to [Articulated Robotics](https://www.youtube.com/@ArticulatedRobotics) for their valuable insights and guidance on Docker using ROS.

