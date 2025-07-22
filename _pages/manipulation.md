---
layout: page
permalink: /manipulation/
title: manipulation
description: Implimenting manipulation algorithms
nav: false
nav_order: 2
---
## Manipulation on LeRobot
Hey welcome to my manipualtion project page. 
The overall goal for this project is to implement cool algorithms on a pretty afforable and available hardware platform. 
Perhaps making it easier for the robotics community to understand and implement complicated research work themselves. 

I am using [LeRobot](https://github.com/huggingface/lerobot) by Hugging Face as my implementation platform. 

First things first lets setup the environment. Hugging Face already has a pretty good repository with documentation on the Le Robot environemnt.
The mujoco environemnt I got form the [mujoco mehangrie](https://github.com/google-deepmind/mujoco_menagerie/tree/main/low_cost_robot_arm).

Once the Environemnt is installed it can be launched using 

`python -m  mujoco.viewer --mjcf=scene_box.xml`

The mujoco rendor looks like this. 

![Initial screen](/assets/img/manipulation_proj/init_mujoco.png)

You can see it has 6 joints including the gripper.
No next part is to build a gym env out of this model. 


We will use pretty simple taks here to pick up a piece of puzzle in front of the robot and place it in the matching spot on the board. Her the policy has to determine the best way to pick uo the puzzle piece, has to maintain a stable grasp through the lift and place and then dropt eh piece on the board and align it with the given spot. 

The reward function is specifically made to make this possible in sim. The task at first is to make the robot lean this in sim. 
We will use the algorithm 
#### Insert algorithm
to achieve this task because (1), (2) and (3). We can also choose other approached like --- which would be future work. 

The other interestign piece of the puzzle. (pun inteded) here is using human data to help with training. 
The work I am implementing here is using human in the loop Reinforcement Learning for manipulation [[1]](https://arxiv.org/abs/2410.21845).

[1] Luo, Jianlan, et al. "Precise and dexterous robotic manipulation via human-in-the-loop reinforcement learning." arXiv preprint arXiv:2410.21845 (2024).