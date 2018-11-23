---
layout: post
category: blog
author: krisztiankovacs
title:  "RL Notes 7: Genetic Algorithms"
date:   2018-11-23 09:11:44 +0700
tag: 
- reinforcement learning
description: Notes for week 7 of Siraj Raval's RL course.
---

[Previous week's notes]({%post_url 2018-11-19-rl-notes-6-experience-replay%})

(You can find the notebook teaching a 2D robot to walk [here](https://github.com/kk1694/rl_course/blob/master/Week_7.ipynb))

The previous couple of posts were about optimizing RL agents, whether with [augmented random search]({%post_url 2018-11-08-rl-notes-5-augmented-random-search%}) or [an experience replay buffer]({%post_url 2018-11-19-rl-notes-6-experience-replay%}). Now let's add one more method to the list: genetic algorithms.

Before explaining genetic algorithms, there is one other major change. Last week I was learning the Q (action-value) function, then acting based on that. However, if the action space is vast (or infinite), that method wouldn't work. After all, we would need to learn an action value for every action! Instead, I'll be learning the policy, the mapping from states to actions, directly. For each state, I want to output the best action.

So what are genetic algorithms? They take inspiration from natural selection. We start with a population of different parameters, select the best performing ones (discard the rest), create cross-overs (children), mutate a subset of children, and repeat.

The main benefit of genetic algorithms is that they can be used for any optimization problem. We don't need derivates. Our objective function doesn't even have to be continuous! Therefore, we can use this method for both parameter optimization and hyperparameter search!

The specific steps:
1. Start with an initial population of different settings.
1. Calculate the fitness of each member of the population.
1. Keep the top n performing members, discard the rest.
1. Optionally, create cross-overs between selected members. Sample A and B from the population, and randomly mix their parameters to create a cross-over (their 'child'). Create k cross-overs, and add them to the population.
1. Mutate some members. To mutate a member, add random noise to its parameters.
1. Repeat from step 2.

Optionally, at step 3 we can also select some non-top-performing settings. Including them will create more interesting cross-overs.

