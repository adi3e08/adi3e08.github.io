---
title: "Physics-Informed Model-Based Reinforcement Learning"
permalink: /research/pimbrl
date: 2022-12-05
excerpt: 'We use physics-informed neural networks to train a model-based RL algorithm.'
author_profile: False
---
This work is under review. Link to preprint [here](https://arxiv.org/abs/2212.02179){:target="_blank"}.

## Abstract
We apply reinforcement learning (RL) to robotics. One of the drawbacks of traditional RL algorithms has been their poor sample efficiency. One approach to improve it is model-based RL. We learn a model of the environment, essentially its dynamics and reward function, use it to generate imaginary trajectories and backpropagate through them to update the policy, exploiting the differentiability of the model. Intuitively, learning more accurate models should lead to better performance. Recently, there has been growing interest in developing better deep neural network based dynamics models for physical systems, through better inductive biases. We focus on robotic systems undergoing rigid body motion. We compare two versions of our model-based RL algorithm, one which uses a standard deep neural network based dynamics model and the other which uses a much more accurate, physics-informed neural network based dynamics model. We show that, in environments that are not sensitive to initial conditions, model accuracy matters only to some extent, as numerical errors accumulate slowly. In these environments, both versions achieve similar average-return, while the physics-informed version achieves better sample efficiency. We show that, in environments that are sensitive to initial conditions, model accuracy matters a lot, as numerical errors accumulate fast. In these environments, the physics-informed version achieves significantly better average-return and sample efficiency. We show that, in challenging environments, where we need a lot of samples to learn, physics-informed model-based RL can achieve better asymptotic performance than model-free RL, by generating accurate imaginary data, which allows it to perform many more policy updates. In these environments, our physics-informed model-based RL approach achieves better average-return than Soft Actor-Critic, a SOTA model-free RL algorithm. 


