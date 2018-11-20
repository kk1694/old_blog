---
layout: post
category: blog
author: krisztiankovacs
title:  "RL Notes 6: Experience Replay"
date:   2018-11-20 09:11:44 +0700
tag: 
- reinforcement learning
description: Notes for week 6 of Siraj Raval's RL course.
---

[Previous week's notes]({%post_url 2018-11-08-rl-notes-5-augmented-random-search%})

(You can find the notebook learning a simple 2D game [here](https://github.com/kk1694/rl_course/blob/master/week6.ipynb))

Our next step in making an RL agent more intelligent: let's replace the shallow network that calculates the Q function with a deep one. A move that doesn't seem too surprising. 

We could update the weights of such a network as we did [last week]({%post_url 2018-11-08-rl-notes-5-augmented-random-search%}) using augmented random search. Let's discuss a different way.

We can transform our RL problem into a (quasi) supervised learning problem. Suppose that for each state and action combination we knew the Q (action-value) function. Then we could create a neural network that connects the inputs (the state) to the output (the Q function for every action). After defining a proper loss function (let's say MSE), running gradient descent for a few epochs, we basically solved our RL problem. After all, we have fitted a Q function that gives the value of each action in each state. Thus, we know how to act: choose the action that maximizes Q!

Of course, it's not that simple, as we don't have a dependent (Q) variable for such a supervised learning task. But just as with our [grid-world]({%post_url 2018-09-21-rl-notes-2%}) example early on, we can work iteratively. 

We start with a randomly initialized Q function. We play a couple of rounds with that Q function, and save the game history: the states, actions, rewards, next states at each point of time. Now we set up our supervised learning problem. Our independent variables are our states and actions. Our dependent variable is constructed: it is the immediate reward, plus the discounted maximum Q value of the next state. 

Our Q function is thus doing two jobs. It is used for evaluating the next state, thus providing the dependent variable for our supervised learning problem. And it is also the object that is trained. Surprisingly, such an iterative strategy works, and our Q function converges. For optimization purposes, it is better to keep two separate copies of the same network: one for evaluation, one for training. We then periodically copy the weights we learned over to our evaluation network.

Note that we should also do some exploration, and not just follow our Q function. An [epsilon-greedy]({%post_url 2018-09-30-rl-notes-3-exporation-vs-exploitation%}) strategy works: most of the time, we do the (so-far-judged-to-be) optimal action, but every now and then we take a random action instead.

Step-by-step our strategy is the following:
1. Initialize Q with random weights.
1. Make a copy of Q to serve as evaluation, call it $$Q'$$.
1. Play the game for a few rounds using Q and an epsilon-greedy strategy. Save (state, action, reward, next state) in a buffer.
1. Randomly sample mini-batches from the buffer. Construct the target to be $$y_t = reward_t + max Q'_{t+1}$$
1. Using a loss function and gradient descent, update Q.
1. Periodically, set $$Q'$$ equal to $$Q$$.

