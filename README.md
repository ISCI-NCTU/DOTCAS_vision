# Dynamic Object Tracking

#### Build status
[![Build Status](https://travis-ci.org/kuka-isir/kinects_human_tracking.svg?branch=master)](https://travis-ci.org/kuka-isir/kinects_human_tracking)

## Introduction
- This package was originally based on [kinects_human_tracking](https://github.com/kuka-isir/kinects_human_tracking) develop by [JimmyDaSilva](https://github.com/JimmyDaSilva), Perception research engineer at ISIR, Paris

- Maintainer : [Howard Chen](https://github.com/s880367), Robotic vision researcher, NCTU-ISCI, Taiwan

- This package is meant to be used for tracking a humans carrying stuff and moving around a robot. We strongly recommend to use several RGBD-sensors, "kinects", (mainly to deal with occlusion from the robot) but this package can be used with a single sensor. Obviously all the sensors intrinsics and extrinsics need to be properly calibrated. First, for all kinects, we remove the robot from the pointcloud so we won't be tracking the robot moving around instead of humans. Secondly, the static background is then removed by substracting a photo of the current view without any humans in it. Then I create a pointcloud for each background&robot-subtracted depth image, downsample the resulting pointClouds and merge all these points together in a single cloud. Finally, we create clusters from the merged pointCloud and use only the closest cluster to the robot.


## TODOs
- Adopt other clustering algorithm
- Adopt other point cloud merging algorithm 
- Allow the use of a particle filter
- Add more rules to detect humans
- Improve even more the code by using nodelets


## Instructions(This instructions are executing under kinectV2)
```
roslaunch kinects_human_tracking kinect_merge.launch topic_name1:=/kinectV2/depth_registered/downsampled_filtered_points topic_name2:=/kinect2/depth_registered/downsampled_filtered_points
```
or
```
roslaunch kinects_human_tracking kinect_merge.launch topic_name1:=/kinectV2/depth_registered/downsampled_filtered_points  
roslaunch kinects_human_tracking closest_pt_tracking.launch end_eff_frame:=base_link
```
