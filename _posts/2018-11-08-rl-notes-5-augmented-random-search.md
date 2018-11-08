---
layout: post
category: blog
author: krisztiankovacs
title:  "RL Notes 5: Augmented Random Search"
date:   2018-11-08 09:11:44 +0700
tag: 
- reinforcement learning
description: Notes for week 5 of Siraj Raval's RL course.
---

[Previous week's notes]({%post_url 2018-10-07-rl-notes-4-temporal-differences%})

(You can find the notebook teaching a 2D robot to walk [here](https://github.com/kk1694/rl_course/blob/master/Midterm.ipynb))

Suppose we want to teach a robot how to walk. Each time-step, we have to tell it how much to rotate each joint, with what velocity, etc. In other words, we have to give it a vector that controls its joint movements. Each moment we also receive some information from the environment: where our robot is at, what speed it is going, etc.

A shallow neural net is a simple architecture that maps the input vector to the necessary outputs. However, we have to choose appropriate weights. 

Normally we train a neural net with gradient descent. But gradient descent may not always be possible: we might not have a gradient of our loss function, or it may simply be computationally expensive. Augmented random search is an alternative.

The basic algorithm for augmented random search is similar to finite differences:
1. Create a random perturbation $$\delta$$ of the same shape as our parameter matrix $$\theta$$ (small positive or negative random amounts).
1. Make two copies of our parameter matrix, one in which we add $$\delta$$, on in which we subtract it (resulting in $$\theta^+$$ and $$\theta^-$$).
1. Simulate our agent with these two new matrices, and record the rewards ($$r^+$$ and $$r^-$$).
1. Update our parameter matrix by $$\theta_{new} = \theta + \alpha(r^+ - r^-)\delta$$, where $$\alpha$$ is the learning rate.

The algorithm is quite simple. To make it more effective, we can take a couple of additional steps:
- Normalizing inputs before feeding it into the neural net.
- Instead of simulating one perturbation, simulating *n*. Then keeping the top *k* performing ones and averaging them.

