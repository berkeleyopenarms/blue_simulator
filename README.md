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

To load the joint position controller for the right arm run
```bash
rosservice call /right_arm/controller_manager/load_controller "blue_controllers/joint_position_controller"
```
You can then switch to using the joint_position_controller

```bash
rosservice call /right_arm/controller_manager/switch_controller "start_controllers:
- 'blue_controllers/joint_position_controller'
stop_controllers:
- ''
strictness: 1"

```

### Notes
* only tested for ROS kinetic
