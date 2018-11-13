# blue_simulator
ROS package for simulating blue

### Requirements
First download the blue_core package in your ROS workspace.
```bash
https://github.com/berkeleyopenrobotics/blue_core.git
```

Next you can clone the blue simulator package into your workspace.
```bash
https://github.com/berkeleyopenrobotics/blue_simulator.git
```

Then navigate to the root of your workspace and run
```bash
catkin_make
```

### Instructions for use
To launch the gazebo simulator
```bash
roslaunch blue_gazebo blue_world.launch
```

To load the joint computed torque controller for the right arm run
```bash
rosservice call /right_arm/controller_manager/load_controller "blue_controllers/joint_ctc"
```
You can then switch to using the joint computed torque controller

```bash
rosservice call /right_arm/controller_manager/switch_controller "start_controllers:
- 'blue_controllers/joint_ctc'
stop_controllers:
- ''
strictness: 1"
```

You can now publish to the `/right_arm/blue_controllers/joint_ctc/command` topico to control the arm. For example you can use the ```rqt_ez_publisher```.
```
rosrun rqt_ez_publisher rqt_ez_publisher
```
* Select the `/right_arm/blue_controllers/joint_ctc/command` topic.
* Add data[*] to the topic until you have a total of seven (should be up to data[6]).
* You can now publish topic by dragging the sliders.

### Notes
* only tested for ROS kinetic
* the gripper is not physically modeled but can be controlled similarly with the ```gripper_controller```
