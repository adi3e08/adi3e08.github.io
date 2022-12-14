---
title: "Physics-Informed Model-Based Reinforcement Learning"
permalink: /research/pimbrl
date: 2022-12-05
excerpt: 'We use physics-informed neural networks to train a model-based RL algorithm. We show that, in model-based RL, model accuracy mainly matters in environments that are sensitive to initial conditions.'
author_profile: False
---
We apply reinforcement learning (RL) to robotics. One of the drawbacks of traditional RL algorithms has been their poor sample efficiency. One approach to improve the sample efficiency is model-based RL. Our model-based RL algorithm iterates over three steps,
- Environment Interaction : Interact with the environment and gather data. 
- Model Learning : Use the gathered data to learn a model of the environment (transition dynamics and reward function).
- Behaviour Learning : Use the learned model to generate imaginary trajectories. Backpropagate through the imaginary trajectories to update the policy, exploiting the differentiability of the model.

Intuitively, learning more accurate models should lead to better performance. In general, we can learn more accurate dynamics models by utilizing the structure of the underlying physics.

## Environments
We focus on robotic systems undergoing rigid body motion. In this work, we assume that there is no friction or contacts. In future work, we plan to include these effects as well. 
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/envs.png" width="100%"/>
</p>

## Lagrangian Mechanics
These systems obey Lagrangian mechanics. The state consists of generalized coordinates $\textbf{q}$, which describe the configuration of the system, and generalized velocities $\dot{\textbf{q}}$. Let the motor torques be $\boldsymbol\tau$. The Lagrangian equations of motion for these systems are given by,
\\[
\underbrace{\textbf{M}(\textbf{q})}\_{\substack{\\\ \text{Mass} \\\ \\\ \text{Matrix}}} \, \ddot{\textbf{q}} + \underbrace{\frac{\partial }{\partial \textbf{q}} \bigg(\textbf{M}(\textbf{q})\, \dot{\textbf{q}} \bigg) \, \dot{\textbf{q}} - \frac{\partial }{\partial \textbf{q}} \bigg( \frac{1}{2} \, \dot{\textbf{q}}^{T} \, \textbf{M}(\textbf{q})\, \dot{\textbf{q}} \bigg)}\_{\substack{\\\ \textbf{C}(\textbf{q},\dot{\textbf{q}}) \, \dot{\textbf{q}} \\\ \\\ \text{Coriolis} \\\ \\\ \text{Term}}} + \underbrace{\frac{\partial \mathcal{V}(\textbf{q})}{\partial \textbf{q}}}\_{\substack{\\\ \textbf{G}(\textbf{q}) \\\ \\\ \text{Gravitational} \\\ \\\ \text{Term}}} = \boldsymbol\tau
\\]

## Dynamics Learning
We want to learn the transformation $(\textbf{q}_{t}, \dot{\textbf{q}}\_{t},\boldsymbol\tau\_{t}) \rightarrow (\textbf{q}\_{t+1}, \dot{\textbf{q}}\_{t+1})$.
We consider two dynamics models,
1. A standard deep neural network (DNN) 
2. A much more accurate Lagrangian Neural Network (LNN). Here, we utilize the structure of the underlying Lagrangian mechanics to estimate $\ddot{\textbf{q}}$ and then numerically integrate $(\dot{\textbf{q}}, \ddot{\textbf{q}})$ over one time step, using second-order Runge-Kutta, to compute the next state.

<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/lnn_dnn.svg" width="80%"/>
</p>

## Behaviour Learning
We adopt an actor-critic approach. We train the critic to regress the $\lambda$-return computed using a target network. We use a stochastic actor. We train the actor to maximize the same $\lambda$-return, plus an entropy term. To backpropagate through sampled actions, we use the reparameterization trick.

## Model-Based RL Algorithm
We summarize our overall model-based RL algorithm below.
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/algo.png" width="100%"/>
</p>

## Experiments
We train two versions of our model-based RL algorithm, one which uses the DNN approach for dynamics learning and the other which uses the LNN approach. In addition, we train Soft Actor-Critic (SAC), a state-of-the-art model-free RL algorithm, to serve as a baseline. We train each method on five random seeds.

## Results
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/all_return.png" width="100%"/>
</p>
- We show that, in model-based RL, model accuracy mainly matters in environments that are sensitive to initial conditions. In these environments, the physics-informed version of our algorithm achieves significantly better average-return and sample efficiency. In environments that are not sensitive to initial conditions, both versions of our algorithm achieve similar average-return, while the physics-informed version achieves better sample efficiency. We measure the sensitivity to initial conditions using the finite-time maximal Lyapunov exponent. 

- We also show that, in challenging environments, where we need a lot of samples to learn, physics-informed model-based RL can achieve better average-return than state-of-the-art model-free RL algorithms such as Soft Actor-Critic, by generating accurate imaginary data.

## Videos
We show the behaviours learnt by our physics-informed model-based RL approach below.
<div align="center"> 
 <video title="Reacher" style="outline:none; width:22.5%;" controls>
  <source src="https://adi3e08.github.io/files/research/pimbrl/reacher.mp4" type="video/mp4">
</video> 
 <video title="Pendulum" style="outline:none; width:22.5%;" controls>
  <source src="https://adi3e08.github.io/files/research/pimbrl/pendulum.mp4" type="video/mp4">
</video> 
 <video title="Cartpole" style="outline:none; width:22.5%;" controls>
  <source src="https://adi3e08.github.io/files/research/pimbrl/cartpole.mp4" type="video/mp4">
</video> 
 <video title="Cart2pole" style="outline:none; width:22.5%;" controls>
  <source src="https://adi3e08.github.io/files/research/pimbrl/cart2pole.mp4" type="video/mp4">
</video> 
</div>

<div align="center"> 
 <video title="Acrobot" style="outline:none; width:22.5%;" controls>
  <source src="https://adi3e08.github.io/files/research/pimbrl/acrobot.mp4" type="video/mp4">
</video> 
 <video title="Cart3pole" style="outline:none; width:22.5%;" controls>
  <source src="https://adi3e08.github.io/files/research/pimbrl/cart3pole.mp4" type="video/mp4">
</video> 
 <video title="Acro3bot" style="outline:none; width:22.5%;" controls>
  <source src="https://adi3e08.github.io/files/research/pimbrl/acro3bot.mp4" type="video/mp4">
</video> 
</div>

## Preprint
This work is under review. Preprint can be accessed [here](https://arxiv.org/abs/2212.02179){:target="_blank"}.

## Code
Coming soon.
