# hcrl_gazebo

![CI](https://github.com/hcrlab/hcrl_gazebo/workflows/CI/badge.svg)

![Gazebo01](docs/images/gazebo_01.png)

Contains a fork of [aws_robomaker_small_house_world](https://github.com/aws-robotics/aws-robomaker-small-house-world), with the ground plane swapped for something with friction parameters compatible with Fetch, and with some textures swapped out.

YCB object models are redistributed under CC BY 4.0.

[WRS objects](https://github.com/hsr-project/tmc_wrs_gazebo) are redistributed under the BSD 3.0 Clear license.

## Installation

In order to simulate the external head camera, you'll need to clone  [PAL Robotics' Gazebo plugin](https://github.com/pal-robotics/realsense_gazebo_plugin) into the workspace. Because the gripper is poorly simulated, we also use [a "grasp hack" plugin](https://github.com/JenniferBuehler/gazebo-pkgs.git) provided by another package to attach objects to the gripper. 

To make sure you have all the dependencies

    wstool init <path_to_workspace> <path_to_hcrl_gazebo>/.rosinstall

If you've already run `wstool` in your workspace, merge the new dependencies with

    wstool merge -t <path_to_workspace>/src <path_to_hcrl_gazebo>/.rosinstall
    cd src
    wstool update

## Usage

Launch one of the simulations with

    roslaunch hcrl_gazebo [house_simulation| playground_simulation].launch

then launch whatever task specific nodes you need separately. Avoid having robot code depend on this package; there are a lot of large binary files in here, and we don't want to have to clone those to the robot (where we'll certainly never use them).

### Stretch

Clone and build our fork of `stretch_ros` in your workspace. This fork includes corrected collision geometry and inertial properties, as well as functioning navigation configurations.

    roslaunch hcrl_gazebo house_simulation_stretch.launch
    
will launch the house and load "Forky", our lab's modified Stretch model, by default. You can toggle the dexwrist and teleop fisheye add-ons by modifying `spawn_stretch.xml`. If localization is performing poorly, you can enable fake localization in `stretch_navigation.launch`

### Spawning Objects

The example script shows how to add an object to Gazebo through the ROS interface.

    rosrun hcrl_gazebo house_add_table_objects

## House: How to Replace Photos in Picture Frames

Picture frames use two textures for the model:
 - `aws_portraitA_01.png` - Frame texture
 - `aws_portraitA_02.png` - Picture texture

To change a picture, one has to replace the `aws_portraitA_02.png` file. The new image will look best with same aspect ratio as the replaced image.

Below is a table showing portrait type to picture resolution data and custom images from photos/.

| Portrait Model | Resolution | Photo |
| --- | --- | --- |
| DeskPortraitA_01 | 650x1024 | |
| DeskPortraitA_02 | 650x1024 | doug |
| DeskPortraitB_01 | 650x1024 | |
| DeskPortraitB_02 | 650x1024 | |
| DeskPortraitC_01 | 1024x1024 | |
| DeskPortraitC_02 | 1024x1024 | |
| DeskPortraitD_01 | 1024x1024 | |
| DeskPortraitD_02 | 1024x1024 | |
| DeskPortraitD_03 | 1024x1024 | |
| DeskPortraitD_04 | 1024x1024 | ray |
| PortraitA_01 | 700x1024 | tim |
| PortraitA_02 | 700x1024 | anamika |
| PortraitB_01 | 700x1024 | renato |
| PortraitB_02 | 700x1024 | brandon |
| PortraitB_03 | 700x1024 | miaofei |
| PortraitC_01 | 650x1024 | sean |
| PortraitD_01 | 1024x450 | |
| PortraitD_02 | 1024x450 | |
| PortraitE_01 | 700x1024 | maggie |
| PortraitE_02 | 700x1024 | iftach |

