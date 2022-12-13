---
title: "Physics-Informed Model-Based Reinforcement Learning"
permalink: /research/pimbrl
date: 2022-12-05
excerpt: 'We use physics-informed neural networks to train a model-based RL algorithm.'
author_profile: False
---
This work is under review. Link to preprint [here](https://arxiv.org/abs/2212.02179){:target="_blank"}.

# Note : Under construction.

We apply reinforcement learning (RL) to robotics. One of the drawbacks of traditional RL algorithms has been their poor sample efficiency. One approach to improve the sample efficiency is model-based RL. In our model-based RL algorithm, we learn a model of the environment, use it to generate imaginary trajectories and backpropagate through them to update the policy, exploiting the differentiability of the model. The model essentially consists of the transition dynamics and reward function. Intuitively, learning more accurate models should lead to better model-based RL performance. 

We focus on robotic systems undergoing rigid body motion. In this work, we assume that there is no friction or contacts. In future work, we plan to include these effects as well.
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/reacher.jpg" width="12%"/>
<img src="https://adi3e08.github.io/files/research/pimbrl/pendulum.jpg" width="12%"/>
<img src="https://adi3e08.github.io/files/research/pimbrl/cartpole.jpg" width="12%"/>
<img src="https://adi3e08.github.io/files/research/pimbrl/cart2pole.jpg" width="12%"/>
<img src="https://adi3e08.github.io/files/research/pimbrl/acrobot.jpg" width="12%"/>
<img src="https://adi3e08.github.io/files/research/pimbrl/cart3pole.jpg" width="12%"/>
<img src="https://adi3e08.github.io/files/research/pimbrl/acro3bot.jpg" width="12%"/>
</p>

## Model-Based RL
We summarize our model-based RL algorithm below. It essentially iterates over three steps : environment interaction, model learning and behaviour learning. 
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/algo.png" width="75%"/>
</p>

We discuss the model learning and behaviour learning steps in detail below. 

### Model Learning
Here, we learn the dynamics and reward models. In dynamics learning, we want to predict the next state, given the current state and action.
We model these systems using Lagrangian mechanics. Hence, the state consists of generalized coordinates $\textbf{q}$, which describe the configuration of the system, and generalized velocities $\dot{\textbf{q}}$, which are the time derivatives of $\textbf{q}$. The action is the motor torque $\boldsymbol\tau$. So, in dynamics learning, we essentially want to learn the transformation $(\textbf{q}_{t}, \dot{\textbf{q}} _{t},\boldsymbol\tau _{t}) \rightarrow (\textbf{q}_{t+1}, \dot{\textbf{q}} _{t+1})$. The most straightforward solution is to train a standard deep neural network. We refer to this approach as DNN. This is shown in the figure below.
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/dnn.svg" width="15%"/>
</p>

Another approach is to utilize the structure of the underlying Lagrangian mechanics. This approach builds upon recent work such as Deep Lagrangian Networks [[1]](#1) and Lagrangian Neural Networks [[2]](#2). We detail this approach here. In Lagrangian mechanics, the Lagrangian is a scalar quantity defined as $\mathcal{L}(\textbf{q},\dot{\textbf{q}},t) = \mathcal{T}(\textbf{q}, \dot{\textbf{q}})-\mathcal{V}(\textbf{q})$, where $\mathcal{T}(\textbf{q}, \dot{\textbf{q}})$ is the kinetic energy and $\mathcal{V}(\textbf{q})$ is the potential energy. The Lagrangian equations of motion are given by, $\dfrac{d}{dt}\dfrac{\partial \mathcal{L}}{\partial \dot{\textbf{q}}}-\dfrac{\partial \mathcal{L}}{\partial \textbf{q}} = \boldsymbol\tau$. For systems undergoing rigid body motion, the kinetic energy is $\frac{1}{2} \, \dot{\textbf{q}}^{T} \, \textbf{M}(\textbf{q}) \, \dot{\textbf{q}}$, where $\textbf{M}(\textbf{q})$ is the mass matrix, which is symmetric and positive definite. Hence, the Lagrangian equations of motion become,
\\[
\textbf{M}(\textbf{q}) \, \ddot{\textbf{q}} + \underbrace{\frac{\partial }{\partial \textbf{q}} \bigg(\textbf{M}(\textbf{q})\, \dot{\textbf{q}} \bigg) \, \dot{\textbf{q}} - \frac{\partial }{\partial \textbf{q}} \bigg( \frac{1}{2} \, \dot{\textbf{q}}^{T} \, \textbf{M}(\textbf{q})\, \dot{\textbf{q}} \bigg)}\_{\textbf{C}(\textbf{q},\dot{\textbf{q}}) \, \dot{\textbf{q}}} + \underbrace{\frac{\partial \mathcal{V}(\textbf{q})}{\partial \textbf{q}}}\_{\textbf{G}(\textbf{q})} = \boldsymbol\tau
\\]

Here, $\textbf{C}(\textbf{q},\dot{\textbf{q}}) \, \dot{\textbf{q}}$ represents the centripetal / Coriolis forces and $\textbf{G}(\textbf{q})$ represents the conservative forces (e. g., gravity). We use one network to learn the potential energy function $\mathcal{V}(\textbf{q})$ and another network to learn a lower triangular matrix $\textbf{L}(\textbf{q})$, using which we compute the mass matrix as $\textbf{M}(\textbf{q}) = \textbf{L}(\textbf{q})\;\textbf{L}^{T}(\textbf{q})$. We then compute $\textbf{C}(\textbf{q},\dot{\textbf{q}}) \, \dot{\textbf{q}}$ and $\textbf{G}(\textbf{q})$ as shown in Equation \ref{eq-1}. Rearranging Equation \ref{eq-1}, we get the acceleration as $\ddot{\textbf{q}} = \textbf{M}^{-1}(\textbf{q})\,(\boldsymbol\tau - \textbf{C}(\textbf{q},\dot{\textbf{q}}) \, \dot{\textbf{q}} - \textbf{G}(\textbf{q}))$. We then numerically integrate the state derivative $(\dot{\textbf{q}}, \ddot{\textbf{q}})$ over one time step using second-order Runge-Kutta to compute the next state. We refer to this approach as LNN, short for Lagrangian Neural Network. The entire process is shown in the figure below.
<p align="center">
<img src="https://adi3e08.github.io/files/research/pimbrl/lnn.svg" width="52%"/>
</p>

In reward learning, we want to learn the reward function. In general, the reward is a function of the current state, action and the next state. In our case, the reward only depends on the next state. Hence, we train a network to map the next state to the reward.

### Behaviour Learning
Here, we use the learned model to generate imaginary trajectories and backpropagate through them to update the policy. We build upon the Dreamer algorithm [[3]](#3) [[4]](#4). We adopt an actor-critic approach. The critic aims to predict the expected discounted return from a given state. We train the critic to regress the $\lambda$-return. We stabilize the critic training by computing the $\lambda$-return using a target network that is updated every 100 critic updates. The critic loss function is given by $L(w)  = \mathbb{E}\:[\sum_{t=0}^{T-1} \frac{1}{2} ( \: V(s_{t};w) - \text{sg}\,(V'_{\lambda}(s_{t})) \: ) ^{2}]$, where,
\\[
V'_{\lambda}(s_{t}) = \begin{cases} \; r_{t} + \gamma \, (\,
(1-\lambda)V'(s_{t+1};w') + \lambda V'_{\lambda}(s_{t+1}) \,) & \text{if} \; t < T\\
\; V'(s_{t};w') & \text{if} \; t = T
\end{cases}
\\]

We stop the gradients around the target (denoted by the $\text{sg}(.)$ function), as is typical in the literature. We use a stochastic actor. The actor aims to output actions that lead to states that maximize the expected discounted return. We train the actor to maximize the same $\lambda$-return that was computed to train the critic. We add an entropy term to the actor objective to encourage exploration. The overall actor loss function is given by $L(\theta)  = - \; \mathbb{E}\:[\sum_{t=0}^{T-1} [\:V'_{\lambda}(s_{t}) - \eta \log \pi (a_{t}|s_{t};\theta) \:]]$. To backpropagate through sampled actions, we use the reparameterization trick~\citep{kingma2013auto}. The actor network outputs the mean $\mu$ and standard deviation $\sigma$ of a Gaussian distribution, from which we obtain the action as $a_{t} = \text{tanh}(\mu_{\theta}(s_{t})+\sigma_{\theta}(s_{t})\cdot \epsilon)$, where $\epsilon \sim \mathcal{N}(0,\mathbb{I})$.


### References
<a id="1">[1]</a>
M. Lutter, C. Ritter, and J. Peters. Deep lagrangian networks: Using physics as model prior for deep learning. In International Conference on Learning Representations (ICLR), 2019a.

<a id="2">[2]</a>
Miles Cranmer, Sam Greydanus, Stephan Hoyer, Peter Battaglia, David Spergel, and Shirley Ho. Lagrangian neural networks. In ICLR 2020 Workshop on Integration of Deep Neural Models and Differential Equations, 2020.

<a id="3">[3]</a>
Danijar Hafner, Timothy Lillicrap, Jimmy Ba, and Mohammad Norouzi. Dream to control: Learning behaviors by latent imagination. arXiv preprint arXiv:1912.01603, 2019.

<a id="4">[4]</a>
Danijar Hafner, Timothy Lillicrap, Mohammad Norouzi, and Jimmy Ba. Mastering atari with discrete world models. arXiv preprint arXiv:2010.02193, 2020.
