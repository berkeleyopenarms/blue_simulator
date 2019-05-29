# blue_simulator
(Experimental) ROS package for simulating Blue via Gazebo.

### Install instructions

- Install Ubuntu 16.0.4
- [Install ROS Kinetic](http://wiki.ros.org/kinetic/Installation/Ubuntu)
  - Start from 1.2 to 1.7, just copy paste into terminal 
  - For step 1.4, use Desktop-Full if unsure
- Create a workspace:
  ```bash
  mkdir -p ~/blue_ws/src && cd "$_"
  ```
- Clone the required packages:
  ```bash
  git clone https://github.com/berkeleyopenarms/blue_core.git
  git clone https://github.com/berkeleyopenarms/blue_simulator.git
  ```
- Install dependencies:
  ```bash
  cd ~/blue_ws
  rosdep install --from-paths src --ignore-src -r -y
  ```
- Build:
  ```bash
  catkin_make install
  ```
- Source:
  ```bash
  echo "source ~/blue_ws/devel/setup.bash" >> ~/.bashrc
  source ~/blue_ws/devel/setup.bash
  ```

### Instructions for use
To launch the simulator (and rviz):
```bash
roslaunch blue_gazebo blue_world.launch
```

To load the joint computed torque controller for the right arm:
```bash
rosservice call /right_arm/controller_manager/load_controller "blue_controllers/joint_ctc"
```

You can then switch to using the joint computed torque controller:

```bash
rosservice call /right_arm/controller_manager/switch_controller "start_controllers:
- 'blue_controllers/joint_ctc'
stop_controllers:
- ''
strictness: 1"
```

You can now publish to the `/right_arm/blue_controllers/joint_ctc/command` topic to control the arm. We like to use `rqt_ez_publisher`:
```
sudo apt-get install ros-kinetic-rqt-ez-publisher
rosrun rqt_ez_publisher rqt_ez_publisher
```
* Select the `/right_arm/blue_controllers/joint_ctc/command` topic.
* Add data[*] to the topic until you have a total of seven (should be up to data[6]).
* You can now publish to the topic by dragging the sliders.

### Notes
* The gripper can be controlled using the `/(right/left)_arm/blue_controllers/gripper_controller` controller, but the URDF relies on [mimic joints](http://wiki.ros.org/urdf/XML/joint) and though it works on both rviz and Gazebo, will result in crashes in Gazebo if the gripper grasps an object. This is because the mimic joint plugin used to implement mimic joints in Gazebo will exert instantaneous forces which crashes the simulation.
