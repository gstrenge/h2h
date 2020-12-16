# Setting Up Workspace (Step 1)
## [Rethink Robotics Intera Workspace Setup](https://sdk.rethinkrobotics.com/intera/Workstation_Setup#Create_Development_Workspace)


1. Began by running commands, replacing `kinetic` with `melodic`:
    ```
    $ sudo apt-get update

    $ sudo apt-get install git-core python-argparse python-wstool python-vcstools python-rosdep ros-melodic-control-msgs ros-melodic-joystick-drivers ros-melodic-xacro ros-melodic-tf2-ros ros-melodic-rviz ros-melodic-cv-bridge ros-melodic-actionlib ros-melodic-actionlib-msgs ros-melodic-dynamic-reconfigure ros-melodic-trajectory-msgs ros-melodic-rospy-message-converter
    ```
    **NOTE:** If you have issues installing `ros-melodic-rospy-message-converter`, the uncomment the install for `rospy-message-converter` in the `.rosinstall` file to compensate.

2. Created new melodic workspace:
    ```
    $ mkdir -p ~/h2h/src
    $ source /opt/ros/melodic/setup.bash
    ```

3. Use `wstool` to install dependencies from `h2h` repository:

   **NOTE:** For ROS Melodic, no need to download and edit .rosinstall file. If using ROS kinetic, you should change two versions in the .rosinstall file:
     - `sawyer_moveit` `version: melodic_devel` --> `version: release-5.3.0`
     - `sns_ik` `version: melodic_devel` --> `version: kinetic-devel`
    ```
    $ cd ~/h2h/src
    $ wstool init .
    $ wstool merge https://raw.githubusercontent.com/gstrenge/h2h/master/src/.rosinstall
    $ wstool update
    ```
4. Run `catkin_make` again:
   ```
   $ cd ~/h2h
   $ catkin_make
   ```

# Next Steps:
## [Configuring `intera.sh`](https://sdk.rethinkrobotics.com/intera/SDK_Shell)
1. Update `~/h2h/src/intera_sdk/intera.sh` to with the following changes:
   - `your_ip="192.168.XXX.XXX"` <-- Update with your IP Address
     - Obtain from running `ifconfig` and should be the `inet` address
   - `ros_version="melodic"` <-- Change `ros_version` to `melodic`
   - `robot_hostname="localhost"` <-- Change to proper host address (will be set to `localhost` when running with `sim` command, so for the time being while we are just using gazebo sim, this value does not matter)
     - ["Your robot's hostname is defaulted as the Controller's Serial Number and NOT the Robot's Serial Number. The serial number can be located on the back of the robot's controller box. Unless you intend to modify the default Networking configuration, leave the ".local" suffix on the end of the Controller's Serial Number in the robot_hostname.local field."](https://sdk.rethinkrobotics.com/intera/Workstation_Setup#Create_Development_Workspace)
 - Move `intera.sh` file to `h2h` directory for easier access (will be running this shell script in many terminals)
    ```
    $ cp ~/h2h/src/intera_sdk/intera.sh ~/h2h
    ```


## Run Examples: [Link](https://sdk.rethinkrobotics.com/intera/Gazebo_Tutorial)
Joint TOrque Springs Example:
```
$ ./intera.sh sim
$ roslaunch sawyer_gazebo sawyer_world.launch
*in a new terminal*
$ ./intera.sh sim
$ rosrun intera_examples joint_torque_springs.py
```

Simulated Pick and Place Example:
```
$ ./intera.sh sim
$ roslaunch sawyer_sim_examples sawyer_pick_and_place_demo.launch
```