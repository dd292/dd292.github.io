---
layout: page
permalink: /rl/
title: Reinforcement Learning
description: Implimenting RL algorithm
nav: true
nav_order: 2
---
This page is about tabulating some results of implementing rl algorithms on Ant, HalfCheetah, Hopper and Walker environemnts. 
This is my work from [cs285](https://rail.eecs.berkeley.edu/deeprlcourse/) Deep RL course taught by Prof. Sergey Levine.

## Behavorial Cloning

BC is supervised leanrning. Here we are leanring a policy that can predict actions given observation using data from an expert. For these experiments, the expert data was given in the form of .pkl files. 

The policy is an MLP of two layers of size 64 each.
The action and observation space are used from the respective gym env. Reward in each environement is structured as some combination of
```
reward = forward_reward - ctrl_cost + survive_reward
```
here `forward reward` is based on x velocity, `ctrl_cost` is action penalty, and `surviver reward` is `+1` per step.

Finally, reward stastics are reported here. 
### Ant-v4
Total Reward:368.2 \
Training Loss: 0.036\
<video width="480" autoplay loop muted playsinline>
  <source src="/assets/img/rl/ant_bc.mp4" type="video/mp4">
</video>

### HalfCheetah-v4
Total Reward:1223.9 \
Training Loss: 0.033\
<video width="480" autoplay loop muted playsinline>
  <source src="/assets/img/rl/cheetah.mp4" type="video/mp4">
</video>

### Hopper-v4
Total Reward:159.21 \
Training Loss: 0.031\
<video width="480" autoplay loop muted playsinline>
  <source src="/assets/img/rl/Hopper.mp4" type="video/mp4">
</video>

### Waler2d-v4
Total Reward:140.8 \
Training Loss: 0.033\
<video width="480" autoplay loop muted playsinline>
  <source src="/assets/img/rl/walker.mp4" type="video/mp4">
</video>