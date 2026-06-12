# Drone Trajectory Tracking - DJI Mavic 2 + OptiTrack

Indoor drone trajectory tracking and analysis using OptiTrack motion capture 
system, ROS, and MATLAB.

## Overview

Real-time 6DOF pose tracking of a DJI Mavic 2 UAV in an indoor lab environment.
Pose data was streamed via VRPN protocol into ROS, recorded with rosbag, and 
analysed in MATLAB using ROS Toolbox.

## System

- DJI Mavic 2 with reflective markers (rigid body)
- OptiTrack (4 cameras, Motive software)
- VRPN → ROS bridge (`vrpn_client_ros`)
- ROS topic: `/vrpn_client_node/mavic/pose`
- Data recording: `rosbag`
- Analysis: MATLAB ROS Toolbox

## ROS Setup

```bash
roslaunch vrpn_client_ros sample.launch server:=<VRPN_SERVER_IP>
rosbag record -O mavic_trajectory.bag /vrpn_client_node/mavic/pose
```

## MATLAB Analysis

```matlab
bag = rosbag('mavic_trajectory.bag');
poseBag = select(bag,'Topic','/vrpn_client_node/mavic/pose');
msgs = readMessages(poseBag,'DataFormat','struct');
```

## Results

- Total trajectory length: 7.217 m
- Flight duration: 6 s
- Mean stable altitude: 0.947 m (std: 0.028 m)

## Authors

Irma Salkić, Ajla Topalović  
Faculty of Electrical Engineering, University of Sarajevo, 2026
