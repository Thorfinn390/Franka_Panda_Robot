# Franka Panda Color Detection & Pick-and-Place

An autonomous ROS 2 and MoveIt 2 workspace for a Franka Emika Panda robot arm. This project integrates computer vision (`panda_vision`) with motion planning (`panda_moveit` and `pymoveit2`) to detect colored objects and execute a precise pick-and-place pipeline.

## Repository Structure

* **`panda_bringup`**: Launch files to spin up the entire simulation/hardware pipeline.
* **`panda_controller`**: High-level control logic and state machines for the task execution.
* **`panda_description`**: URDF/Xacro files and meshes for the Franka Panda arm.
* **`panda_moveit`**: MoveIt 2 configuration package for motion planning, collision avoidance, and kinematics.
* **`panda_vision`**: OpenCV/camera integration for color segmentation and pose estimation.
* **`pymoveit2`**: Python bindings or utilities interface to simplify MoveIt 2 motion commands.

---

## Setup & Installation

### Prerequisites

* **OS**: Ubuntu 22.04 LTS (Jammy Jellyfish)
* **ROS 2**: Humble Hawksbill
* **MoveIt**: MoveIt 2

Ensure your ROS 2 environment is sourced before proceeding:
```bash
source /opt/ros/humble/setup.bash

```

### Installation Steps

1. **Clone the Repository**
Create a colcon workspace, clone this repository into the `src` directory, and navigate into it:
```bash
mkdir -p ~/panda_ws/src
cd ~/panda_ws/src
git clone https://github.com/Thorfinn390/Franka_Panda_Robot.git
cd ~/panda_ws

```


2. **Install Dependencies**
Use `rosdep` to automatically fetch required system dependencies:
```bash
sudo apt update
rosdep update
rosdep install --from-paths src --ignore-src -r -y

```


3. **Build the Workspace**
```bash
colcon build --symlink-install

```



---

## How to Run

Always remember to source the workspace after building:

```bash
source install/setup.bash

```

### 1. Launch Simulation, MoveIt, Vision, and MoveIt Color Picker Nodes


```bash
ros2 launch panda_bringup pick_and_place.launch.py

```

Note: You can run each node indivitually in different terminals but this is a compact way


### 2. Run the MoveIt2 Pick & Place for a certain color

Pick and place node combining Cartesian and joint-space moves with smooth joint transitions.
Locks the detected color coordinates before starting the motion.

``bash


ros2 run pymoveit2 pick_and_place.py --ros-args -p target_color:=R
ros2 run pymoveit2 pick_and_place.py --ros-args -p target_color:=G
ros2 run pymoveit2 pick_and_place.py --ros-args -p target_color:=B
ros2 run pymoveit2 pick_and_place.py (default is red)

```
