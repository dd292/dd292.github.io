---
layout: page
permalink: /rl/
title: Reinforcement Learning
description: Implementing RL algorithms
nav: false
nav_order: 2
---
This page is about tabulating some results of implementing rl algorithms on Ant, HalfCheetah, Hopper and Walker environmnts. 
This is my work from [cs285](https://rail.eecs.berkeley.edu/deeprlcourse/) Deep RL course taught by Prof. Sergey Levine.
<!-- Tabs Start -->
<div class="nav-tabs-custom">
  <ul class="nav nav-tabs rl-tab-bar">
  <li class="active"><a href="#bc" data-toggle="tab">Behavioral Cloning</a></li>
  <li><a href="#gail" data-toggle="tab">GAIL (soon)</a></li>
  <li><a href="#ppo" data-toggle="tab">PPO (soon)</a></li>
</ul>
  <div class="tab-content">
    <div class="tab-pane active" id="bc">
    <div style="margin-top: 40px;"></div>
      {% capture bc_content %}
      {% include rl_behavioral_cloning.md %}
      {% endcapture %}
      {{ bc_content | markdownify }}
    </div>
    <div class="tab-pane" id="gail">
      <p>Content for GAIL will go here.</p>
    </div>
    <div class="tab-pane" id="ppo">
      <p>Content for PPO will go here.</p>
    </div>
  </div>
</div>