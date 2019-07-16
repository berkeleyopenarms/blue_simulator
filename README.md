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
- Get the mimic joint plugin:
  ```bash
  cd blue_simulator
  git submodule update --init
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
To launch the simulator (`full.launch` corresponds to the full, two-arm setup; `right.launch` or `left.launch` can also be used):
```bash
roslaunch blue_gazebo full.launch
```

Running rviz afterwards is the same as with the physical robot:
```bash
roslaunch blue_bringup rviz.launch
```

### Notes
* The gripper can be controlled using the `/(right/left)_arm/blue_controllers/gripper_controller` controller, but the URDF currently relies on [mimic joints](http://wiki.ros.org/urdf/XML/joint) and will cause Gazebo to crash if the gripper grasps an object. This is because the mimic joint plugin used to implement mimic joints in Gazebo will exert instantaneous forces which crashes the simulation.
