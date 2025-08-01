



For the first section of implemetation, I am implementing vanilla policy gradient on the cartpole environemnt. The [paper](https://proceedings.neurips.cc/paper_files/paper/1999/file/464d828b85b0bed98e80ade0a5c43b0f-Paper.pdf) that introduced policy gradient for reinforcement learning is by RS Sutton et. al.

### Experiment 1
In this exeperiment I implemented four different variants. 
1. Vanilla policy gradients- I represent policy using a 2 layered network and Q fucntion is approximated by summming the discounted rewards of the whole episode. Loss function is calculated by taking the log probability of the policy output, multiplying it with the Q function and taking the mean over the whole batch. 
2. Policy gradient with reward to go- This approach is quite similar to the above implementation with the change in how the Q function is calcuated. Here, instead of summing over the discounted rewards of the whole episode I only sum the dsicounted rewards to go. In other words, rewards of past do not matter and only sum of rewards accumulated by the agent in future are used to approximate the Q function.
3. Policy gradient with advantage normalization: Here I call it adavatge but in reality it is just the Q function normalized in a way that its mean is 0 and the standard deviation is 1. This is a practical approach used to stabilize the training. 
4. Policy gradient with advantage normalization and reward to go. 
<p align="center">
<div style="display: flex; gap: 20px;">
  <img src="/assets/img/rl/Figure_1.png" width="400" vspace="5"/>
  <img src="/assets/img/rl/Figure_2.png" width="400" vspace="5"/>
</div>
</p>

These graphs plot the learning rate for the four variants of policy gradients intrduced above. This is done by plotting average episonde length with average return. Few observations are, 
1. Reward to go does initially stabilize for the samaller episode length but it does suffer from high variance as the episode length increases. However with bigger batch size thats not the case any more since more samples somewhat decreases the variance in training. 
2. Normalizing advantage (Q function here) is a powerful technique. As can be seen from the plots it stabilized the training for the cartpole environment. However, adding reward to go make it perform worse mostly because now the reward is different for every time step unlike the vanilla PG where reward fro every time step is sum of the discounted reward for the whole episode. 

### Experiment 2 
In this experiment I calculated adavtage by subtracting the Q function with a baseline. The baseline is a prediction from a 2 layered neural network which takes in observation as input. The baseline predicts the value function at a state. The update of the baseline is done during the update of the policy but learning rate and number of iterations for the baseline update is a tuanble hyperparameter. 

<p align="center">
<div style="display: flex; gap: 20px;">
  <img src="/assets/img/rl/cheetah_baseline.png" width="400" vspace="5"/>
  <img src="/assets/img/rl/baseline_explorationscheetah_.png" width="400" vspace="5"/>
</div>
</p>
The plot on the left shows the comparison of learning curve with and without baseline for the cheetah environement. Note, advatage without baseline is just discounted sum of reward-to-go. The plot on the right shows the hyperparameter tuning for learning rate and number of update steps for the baseline. 
