---
layout: post
title:  "RL Notes 4: Temporal Differences"
date:   2018-10-07 09:11:44 +0700
categories: reinforcement_learning
---

[Previous week's notes]({post_url 2018-09-30-rl-notes-3-exporation-vs-exploitation})

(You can find the notebook containing the code [here](https://github.com/kk1694/rl_course/blob/master/rl_notes_4.ipynb))

One drawback of the MC methods covered [last week](https://krisztiankovacs.com/reinforcement_learning/2018/09/30/rl-notes-3-exporation-vs-exploitation.html) is that they need to simulate complete episodes of an environment (start to finish) before updating our policy. That's fine if individual episodes are short. However, usually we don't want to wait until the end of an episode to update our policy. Also, some environments are continuous.

Why not update the policy as we go through the task? That's the essence of temporal difference methods (TD). TD is to Monte Carlo what stochastic gradient descent is to batch gradient descent. Update after each round, don't wait until the end. One TD method is Q-learning. It is really simple, but is often described in an overcomplicated way.

Reminder: the Q function is a mapping that gives the value of state-action combinations. To obtain the best action in a state, look up the maximum Q value in that state (among available actions).

We start with randomly initializing Q. After every action, we update it according to:

$$Q(s_t, a_t) = (1 - \alpha)Q(s_t, a_t) + \alpha (r_t + \gamma * \max_{a} Q(s_{t+1}, a) ) $$

Or, equivalently:

$$Q(s_t, a_t) = Q(s_t, a_t) + \alpha (r_t + \gamma * \max_{a} Q(s_{t+1}, a)  - Q(s_t, a_t)) $$

where
- $$Q(., .)$$ is the value of an action in a given state,
- $$\alpha$$ is the learning rate (how quickly we update values,
- $$r_t$$ is the immediate reward at time *t*,
- $$\gamma$$ is the discount factor

In English: after every action we update our Q function. We update it with the immediate reward, plus the discounted value of the best action in the next time-step.

The learning rate controls to what degree we update vs. keep the old value. A learning rate of 0 means no updating at all, a learning rate of 1 means perfect replacement. We don't want perfect replacement, as the reward can be stochastic.

One trick: we should decrease the learning rate over time. The more often we take an action in a given state, the more certain we are about its reward distribution. In the example below, I apply the following learning rate schedule:

$$\alpha_{t} = \frac{\alpha_0}{1 + \alpha_{taper} * count(s_t, a_t)}$$

where $$count(s, a)$$ gives the number of times the agent did action *a* in state *s*. The hyper-parameters $$\alpha_0$$ and $$\alpha_{taper}$$ give the initial learning rate, and how fast I taper it to 0.

## Cheating Roulette again

I'm going to use the same [cheating roulette](https://github.com/kk1694/rl_course/blob/master/rl_notes_3.ipynb) environment as last week. 

I'll only implement the *$$\epsilon$$-greedy* policy, but the other ones are easy to adopt as well.

![png](/assets/img/rl_notes_4/output_12_1.png)


    Actions taken by agent in different rounds

![png](/assets/img/rl_notes_4/output_13_1.png)


The agent learns remarkably fast. That's no surprise, as we update after each action instead of waiting for the end of the episode.
