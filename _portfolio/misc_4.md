---
title: 'Notes on Soft Actor-Critic'
project_type: others
permalink: /blog/sac/
date: 2021-12-17
excerpt : 'A short blog post explaining how SAC works. We also implement SAC from scratch and train on a few tasks.'
author_profile : False
---
Soft Actor-Critic (SAC) [[1]](#1) [[2]](#2) is a state-of-the-art model-free RL algorithm for continuous action spaces. It adopts an off-policy actor-critic approach and uses stochastic policies. It uses the maximum entropy formulation to achieve better exploration.

## Maximum Entropy RL
In maximum entropy RL, the objective is to maximize the expected return while acting as randomly as possible. By doing so, the agent can explore better and capture different modes of optimality. This also improves robustness against environmental changes.
<p align="center">
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/max_ent_rl_3.gif" width="50%" height="50%"/>
<br>
<br>
An agent trained using the maximum entropy RL objective explores both passages during training.
</p>

The entropy of a random variable is defined as, $H(X) = \underset{x \sim P}{\mathbb{E}}[-\log P(x)] $. The maximum entropy RL objective is given by,
\\[ \pi^{\*} = \underset{\pi}{\arg\max} \underset{\tau \sim \pi}{\mathbb{E}} \big[\sum_{t=0}^{\infty}\gamma^{t}\big(\;r(s_{t},a_{t},s_{t+1})+\alpha H(\pi(\cdot|s_{t}))\;\big)\big] \\]

Here $\alpha > 0$ , is the weightage given to the entropy term in the objective. $\alpha$ is also referred to as "temperature". We define the value function to include the entropy bonuses from every timestep,
\\[ V^\pi(s) = \underset{\tau \sim \pi}{\mathbb{E}}\big[\sum_{t=0}^{\infty}\gamma^{t}\big(\;r(s_{t},a_{t},s_{t+1})+\alpha H(\pi(\cdot|s_{t}))\;\big)\;\big|\;s_{0}=s\,\big] \\]

We define the action-value function to include the entropy bonuses from every timestep except the first,
\\[ Q^\pi(s,a) = \underset{\tau \sim \pi}{\mathbb{E}}\big[\sum_{t=0}^{\infty}\gamma^{t} r(s_{t},a_{t},s_{t+1}) + \alpha \sum_{t=1}^{\infty} \gamma^{t} H(\pi(\cdot|s_{t})) \;\big|\;s_{0}=s,a_{0}=a\,\big] \\]

Thus,
\\[ V^\pi(s) = \underset{a \sim \pi}{\mathbb{E}}[Q^\pi(s,a)] + \alpha H(\pi(\cdot|s)) \\]

## SAC
In SAC we have,
- a single policy network, $ \pi_{\theta} $
- two Q networks $Q_{w_{1}} \; , \; Q_{w_{2}}$
- two target Q networks $Q_{w_{1}^{'}} \; , \; Q_{w_{2}^{'}}$

Both Q-functions are learned with Mean Squared Bellman Error minimization, by regressing to a single shared target y.
\\[L(w_{i}) = \underset{(s,a,r,s')\sim \mathcal{D}}{\mathbb{E}}[\;( Q_{w_{i}}(s,a)-y )^{2}\;]\\]

The shared target y is computed using target Q-networks and makes use of the clipped double-Q trick.
\\[y = r + \gamma \; (\; \underset{i=1,2}{\min} Q_{w_{i}^{'}}(s',a') - \alpha \log \pi_{\theta}(a'|s') \;)\\]

The next-state actions used in the target come from the current policy instead of the target policy.

In policy learning, the objective is to maximize,
\\[ V^\pi(s) = \underset{a \sim \pi}{\mathbb{E}}[Q^\pi(s,a)] + \alpha H(\pi(\cdot|s)) \\]

The policy is stochastic, therefore actions are sampled. To be able to backprop through sampled actions, we use the reparameterization trick, 
\\[ a = a_{\theta}(s,\epsilon) = \text{tanh}(\mu_{\theta}(s)+\sigma_{\theta}(s)\cdot \epsilon) \\]

The policy outputs mean $\mu$ and standard deviation $\sigma$ of a Gaussian distribution. We then sample a gaussian noise $\epsilon \sim \mathcal{N}(0,\mathbb{I})$. We combine the noise with the policy outputs and use tanh to squash the action to [-1,1]. Thus, we can rewrite the expectation over actions into an expectation over noise,
\\[ \underset{a\sim \pi_{\theta}}{\mathbb{E}}[\; Q^{\pi_{\theta}}(s,a) - \alpha \log \pi_{\theta}(a|s) \;] = \underset{\epsilon \sim\mathcal{N}}{\mathbb{E}}[\; Q^{\pi_{\theta}}(s,a_{\theta}(s,\epsilon)) - \alpha \log \pi_{\theta}(a_{\theta}(s,\epsilon)|s) \;] \\]

Thus, the final objective becomes,
\\[ \underset{\theta}{\max} \underset{\epsilon \sim\mathcal{N}}{\underset{s\sim \mathcal{D}}{\mathbb{E}}} [\; (\; \underset{i=1,2}{\min} Q_{w_{i}}(s,a_{\theta}(s,\epsilon)) - \alpha \log \pi_{\theta}(a_{\theta}(s,\epsilon)|s) \;] \\]

## Algorithm
<p align="center">
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_algo.png" width="85%"/>
</p>

In SAC v1, the temperature $\alpha$ is a hyperparameter. However it was found that the algorithm is brittle to the choice of $\alpha$. In SAC v2, the temperature $\alpha$ is learnt by minimizing the loss,
\\[ L(\alpha) = \alpha \; (-\log\pi(a|s)-\widetilde{H}) \\] 

where $\widetilde{H}$ is the entropy target. Typically, $\widetilde{H}$ is set to be equal to the negative of the action space dimension i. e. $\widetilde{H} = - \; \text{dim}(\mathcal{A})$.

## Implementation
You can find my Pytorch implementation of SAC for continuous action spaces [here](https://github.com/adi3e08/SAC){:target="_blank"}. 

## Results
I trained SAC on a few continuous control tasks from [Deepmind Control Suite](https://github.com/deepmind/dm_control/tree/master/dm_control/suite). Results are below.

* Cartpole Swingup : Swing up and balance an unactuated pole by applying forces to a cart at its base.
<p align="center">
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_cartpole_swingup.png" width="40%"/>
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_cartpole_swingup.gif" width="31%"/>
</p>

* Reacher Hard : Control a two-link robotic arm to reach a random target location.
<p align="center">
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_reacher_hard.png" width="40%"/>
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_reacher_hard.gif" width="31%"/>
</p>

* Cheetah Run : Control a planar biped to run.
<p align="center">
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_cheetah_run.png" width="40%"/>
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_cheetah_run.gif" width="31%"/>
</p>

* Walker Run : Control a planar biped to run.
<p align="center">
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_walker_run.png" width="40%"/>
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_walker_run.gif" width="31%"/>
</p>

* Humanoid Walk : Control a simplified humanoid to walk.
<p align="center">
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_humanoid_walk.png" width="40%"/>
<img src="https://adi3e08.github.io/files/blog/soft-actor-critic/imgs/sac_humanoid_walk.gif" width="31%"/>
</p>

### References
<a id="1">[1]</a>
Tuomas Haarnoja, Aurick Zhou, Pieter Abbeel, and Sergey Levine. Soft actor-critic: Off-policy maximum entropy deep reinforcement learning with a stochastic actor. In International conference on machine learning, pages 1861–1870. PMLR, 2018a. [Link](https://arxiv.org/abs/1801.01290)

<a id="2">[2]</a>
Tuomas Haarnoja, Aurick Zhou, Kristian Hartikainen, George Tucker, Sehoon Ha, Jie Tan, Vikash Kumar, Henry Zhu, Abhishek Gupta, Pieter Abbeel, et al. Soft actor-critic algorithms and applications. arXiv preprint arXiv:1812.05905, 2018b. [Link](https://arxiv.org/abs/1812.05905)
