# Setting Up Workspace (Step 1)
## [Rethink Robotics Intera Workspace Setup](https://sdk.rethinkrobotics.com/intera/Workstation_Setup#Create_Development_Workspace)


1. Began by running commands, replacing `kinetic` with `melodic`:
    ```
    $ sudo apt-get update

    $ sudo apt-get install git-core python-argparse python-wstool python-vcstools python-rosdep ros-melodic-control-msgs ros-melodic-joystick-drivers ros-melodic-xacro ros-melodic-tf2-ros ros-melodic-rviz ros-melodic-cv-bridge ros-melodic-actionlib ros-melodic-actionlib-msgs ros-melodic-dynamic-reconfigure ros-melodic-trajectory-msgs ros-melodic-rospy-message-converter
    ```
2. Created new melodic workspace:
    ```
    $ mkdir -p ~/h2h/src
    $ cd ~/h2h
    $ source /opt/ros/melodic/setup.bash
    $ catkin_make
    ```