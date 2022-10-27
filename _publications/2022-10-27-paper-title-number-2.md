---
title: "Lagrangian Model Based Reinforcement Learning"
permalink: /publications/mbrl-lnn
date : 2022-10-27
venue: 'Deep Reinforcement Learning Workshop, NeurIPS 2022'
excerpt: 'We utilize the structure of rigid body dynamics to learn a Lagrangian Neural Network and use it to train a model-based RL algorithm.'
---
# Abstract

We apply reinforcement learning (RL) to robotic systems undergoing rigid body motion. One of the drawbacks of traditional RL algorithms has been their poor 
sample efficiency. In robotics, collecting large amounts of training data using actual robots is not practical. One approach to improve the sample 
efficiency of RL algorithms is model-based RL. In our model-based RL algorithm, we learn a model of the environment, essentially its transition dynamics 
and reward function, use it to generate imaginary trajectories and then backpropagate through them to update the policy, exploiting the differentiability 
of the model. Intuitively, learning better dynamics models should improve model-based RL performance. Recently there has been growing interest in 
developing better deep neural network based dynamics models for physical systems, through better inductive biases. We utilize the structure of rigid body 
dynamics to learn a Lagrangian Neural Network and use it to train our model-based RL algorithm. To the best of our knowledge, we are the first to explore 
such an approach. While it is intuitive that such physics-informed dynamics models will improve model-based RL performance, it is not apparent in which 
environments we will significantly benefit from such an approach. We show that, in environments with underactuation and high inherent sensitivity to 
initial conditions, characterized by a large maximal Lyapunov exponent under freefall, we are likely to significantly benefit from learning 
physics-informed dynamics models. In such environments, our Lagrangian model-based RL approach achieves better average-return and sample efficiency 
compared to a version of our model-based RL algorithm that uses a standard deep neural network based dynamics model, as well as Soft Actor-Critic, a 
state-of-the-art model-free RL algorithm.

Link to full paper [here](https://adi3e08.github.io/files/Lagrangian_Model_Based_RL.pdf){:target="_blank"}.
