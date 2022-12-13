---
title: "Physics-Informed Model-Based Reinforcement Learning"
permalink: /research/pimbrl
date: 2022-12-05
excerpt: 'We use physics-informed neural networks to train a model-based RL algorithm.'
author_profile: False
---
This work is under review. Link to preprint [here](https://arxiv.org/abs/2212.02179){:target="_blank"}.

## Note : Under construction.

We apply reinforcement learning (RL) to robotics. One of the drawbacks of traditional RL algorithms has been their poor sample efficiency. One approach to improve the sample efficiency is model-based RL. In our model-based RL algorithm, 
- We learn a model of the environment (transition dynamics and reward function). 
- Use the model to generate imaginary trajectories.
- Backpropagate through the imaginary trajectories to update the policy, exploiting the differentiability of the model.

Intuitively, learning more accurate models should lead to better performance. In general, we can learn more accurate dynamics models by utilizing the structure of the underlying physics.

## Environments
We focus on robotic systems undergoing rigid body motion. In this work, we assume that there is no friction or contacts. In future work, we plan to include these effects as well. These systems follow Lagrangian mechanics.
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/envs.png" width="85%"/>
</p>

## Lagrangian Mechanics
Here, the state consists of generalized coordinates $\textbf{q}$, which describe the configuration of the system, and generalized velocities $\dot{\textbf{q}}$. Let the motor torques be $\boldsymbol\tau$. The Lagrangian is defined as $\mathcal{L}(\textbf{q},\dot{\textbf{q}},t) = \mathcal{T}(\textbf{q}, \dot{\textbf{q}})-\mathcal{V}(\textbf{q})$, where $\mathcal{T}(\textbf{q}, \dot{\textbf{q}})$ is the kinetic energy and $\mathcal{V}(\textbf{q})$ is the potential energy. The Lagrangian equations of motion are given by, 
\\[
\dfrac{d}{dt}\dfrac{\partial \mathcal{L}}{\partial \dot{\textbf{q}}}-\dfrac{\partial \mathcal{L}}{\partial \textbf{q}} = \boldsymbol\tau
\\] 

For systems undergoing rigid body motion, the kinetic energy is $\frac{1}{2} \, \dot{\textbf{q}}^{T} \, \textbf{M}(\textbf{q}) \, \dot{\textbf{q}}$, where $\textbf{M}(\textbf{q})$ is the mass matrix, which is symmetric and positive definite. Hence, the Lagrangian equations of motion become,
\\[
\textbf{M}(\textbf{q}) \, \ddot{\textbf{q}} + \underbrace{\underbrace{\frac{\partial }{\partial \textbf{q}} \bigg(\textbf{M}(\textbf{q})\, \dot{\textbf{q}} \bigg) \, \dot{\textbf{q}} - \frac{\partial }{\partial \textbf{q}} \bigg( \frac{1}{2} \, \dot{\textbf{q}}^{T} \, \textbf{M}(\textbf{q})\, \dot{\textbf{q}} \bigg)}\_{\substack{\textbf{C}(\textbf{q},\dot{\textbf{q}}) \, \dot{\textbf{q}} \\ \text{Coriolis Term}}}} + \underbrace{\underbrace{\frac{\partial \mathcal{V}(\textbf{q})}{\partial \textbf{q}}}\_{\substack{\textbf{G}(\textbf{q}) \\ \text{Gravitational Term}}}} = \boldsymbol\tau
\\]

## Dynamics Learning
Here, we want to learn the transformation $(\textbf{q}_{t}, \dot{\textbf{q}}\_{t},\boldsymbol\tau\_{t}) \rightarrow (\textbf{q}\_{t+1}, \dot{\textbf{q}}\_{t+1})$.
We consider two dynamics models,
1. A standard deep neural network (DNN) 
2. A much more accurate Lagrangian Neural Network (LNN), which utilizes the structure of the underlying physics.

<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/lnn_dnn.svg" width="85%"/>
</p>

## Behaviour Learning
We adopt an actor-critic approach. We train the critic to regress the $\lambda$-return computed using a target network. We use a stochastic actor. We train the actor to maximize the same $\lambda$-return plus an entropy term. To backpropagate through sampled actions, we use the reparameterization trick.

## Model-Based RL Algorithm
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/algo.png" width="100%"/>
</p>

## Experiments
We train two versions of our model-based RL algorithm, one which uses the DNN approach for dynamics learning and the other which uses the LNN approach. In addition, we train Soft Actor-Critic (SAC), a state-of-the-art model-free RL algorithm, to serve as a baseline. We train each method on five random seeds.



