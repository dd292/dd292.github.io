Implementation: Policy Gradient on CartPole
For the first part of the implementation, I applied vanilla policy gradient (PG) to the CartPole environment. The foundational policy gradient paper was introduced by R. S. Sutton et al. (1999).

#### Experiment 1 – Vanilla PG and Reward-to-Go
In this experiment, I implemented four variants of the policy gradient method:
<ol>
  <li>Vanilla Policy Gradient</li>
  <ol>
    <li>The policy is represented by a two-layer neural network.</li>
    <li>The Q-function is estimated by summing all discounted rewards over the episode.</li>
    <li>The loss is computed as the mean of log-probabilities multiplied by Q-values across the batch.</li>
  </ol>
  <li>Policy Gradient with Reward-to-Go</li>
  <ol>
    <li>Similar to the vanilla implementation but modifies the Q-function.</li>
    <li>Instead of summing the entire episode’s discounted rewards, it only sums future rewards from the current timestep. In other words, past rewards do not contribute to the return for that timestep.</li>
  </ol>
<li>Policy Gradient with Advantage Normalization</li>
  <ol>
    <li>Here, the “advantage” is simply the normalized Q-values (zero mean, unit variance).</li>
    <li>This normalization helps stabilize training by reducing variance in gradient estimates.</li>
  </ol>

<li>Policy Gradient with Advantage Normalization + Reward-to-Go</li>
Combines the two variance-reduction techniques above.
</ol>
<p align="center"> <div style="display: flex; gap: 20px;"> <div style="text-align:center;"> <img src="/assets/img/rl/Figure_1.png" width="400" vspace="5"/> <div>Performance of Vanilla PG and Reward-to-Go variants.</div> </div> <div style="text-align:center;"> <img src="/assets/img/rl/Figure_2.png" width="400" vspace="5"/> <div>Comparison of normalized vs unnormalized advantages.</div> </div> </div> </p>
Observations:

<ol>
<li>Reward-to-go stabilizes early training for shorter episodes but can exhibit higher variance in longer episodes. Increasing the batch size mitigates this effect by averaging over more trajectories.</li>

<li>Advantage normalization is a powerful stabilization method. As shown in the plots, it improves convergence for CartPole.</li>

<li>Combining reward-to-go with advantage normalization can sometimes perform worse because each timestep’s reward is now unique, unlike vanilla PG where every timestep shares the full discounted return.</li>
</ol>

#### Experiment 2 – Advantage with Baseline
In this experiment, the advantage is computed by subtracting a baseline from the Q-function. The baseline is predicted using a two-layer neural network that takes the state observation as input and outputs the value function. The baseline is updated alongside the policy, but its learning rate and the number of update steps per iteration are tunable hyperparameters.

<p align="center"> <div style="display: flex; gap: 20px;"> <div style="text-align:center;"> <img src="/assets/img/rl/cheetah_baseline.png" width="400" vspace="5"/> <div>Learning curve with and without baseline in advantage estimation.</div> </div> <div style="text-align:center;"> <img src="/assets/img/rl/baseline_explorationscheetah_.png" width="400" vspace="5"/> <div>Effect of baseline learning rate and number of update steps.</div> </div> </div> </p>
Observations:
<ol>
<li>Without baseline, the advantage is simply the discounted sum of reward-to-go.</li>

<li>Adding a baseline significantly reduces variance and improves training stability.</li>

<li>Tuning the baseline learning rate and update steps impacts convergence speed.</li>
</ol>

#### Experiment 3 – Generalized Advantage Estimation (GAE)
In this experiment, I used the Generalized Advantage Estimation (GAE) method introduced in Schulman et al., 2015.

GAE computes the advantage as a weighted combination of Monte Carlo returns and baseline estimates, controlled by a hyperparameter λ.

<ol>
<li>Lower λ → lower variance but higher bias (closer to value function).</li>

<li>Higher λ → lower bias but higher variance (closer to Monte Carlo).</li>

<li>Properly tuning λ achieves a bias-variance tradeoff that accelerates learning.</li>
</ol>

<p align="center"> <div style="display: flex; gap: 20px;"> <div style="text-align:center;"> <img src="/assets/img/rl/Lundar_lander_GAE.png" width="400" vspace="5"/> <div>Learning curves using GAE with different λ values.</div> </div> </div> </p>
Observation:

GAE provides a flexible interpolation between high-variance Monte Carlo and low-variance value-function approaches, resulting in more stable and efficient training.
<div style="text-align:center;">
  <video width="480" autoplay loop muted playsinline>
    <source src="/assets/img/rl/humanoid.mp4" type="video/mp4">
    Your browser does not support the video tag.
  </video>
  <div style="margin-top: 5px; font-size: 14px; color: gray;">
    Video of implementing GAE with policy gradient on the humanoid environment.
    The policy is trained for 1000 iterations with a batch size of 2000.
  </div>
</div>
