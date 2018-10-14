---
layout: post
category: blog
author: krisztiankovacs
title:  "Review: Blitzing Through the Coursera DL Specialization"
date:   2018-10-14 09:11:44 +0700
tag:
- deep learning journey
- reviews
description: Reviewing Andrew Ng's coursera class.
---

I recently completed Andrew Ng's [deep learning specialization](https://www.coursera.org/specializations/deep-learning) on Coursera.

**TLDR;** it's a great resource. If you are familiar with 'vanilla' machine learning and would like to understand deep learning, it's the perfect place to start. The course teaches both basic DL theory, and tips and tricks on how to optimize your workflow. The lectures are really easy to understand and follow (great), and the coding assignments are also extremely simple (not so great). Coursera says that the course takes between 4-5 months to complete, but if you're dedicated it should take less than one month.

## Overview

The specialization consists of 5 courses. 

1. **Neural Networks and Deep Learning.** Covers basic feedforward networks. Explains shallow & deep networks, parameter initialization, gradient descent, backpropagation, but doesn't dwell too much on the math and proofs. 
1. **Improving Deep Neural Networks: Hyperparameter tuning, Regularization and Optimization.** This module explains the ideas that make NNs work well in practice. One such topic is regularization: weight decay, dropout, batch norm. Enhanced optimization algorithms are also covered: momentum, RMSprop, ADAM. Plus some miscallenous topics: hypterparameter tuning, exploding/vanishing gradients, and gradient checking, etc.
1. **Structuring Machine Learning Projects.** A short module about overall DL project strategy and practical tips and tricks. Topics are cover different aspects of what to focus on and how analyze the errors of your algorithm.  
1. **Convolutional Neural Networks.** A big overview of computer vision. Goes over building blocks like convolutions, padding, strides, pooling; covers common CNN architectures; and also explains topics such as object-detection, Siamese networks, or neural style transfer.
1. **Sequence Models.** Exactly what you would expect: RNNs, GRUs, LSTMs. This course also goes into the different ways to create word embeddings. At the end, it explains attention models.

## Prerequisites

The first course assumes no background, but to get most out of it, you should know some machine learning and linear algebra. 

Each subsequent course builds on the knowledge of the previous, it's best to take them as a sequence.

## Lectures

I don't have much to say about them; they are fantastic. Andrew's explanations are simple, even for somewhat advanced concepts. He doesn't shy away from using math, but limits it to where it makes a practical difference (we are spared the proof of backpropagation). Sometimes he discusses code, but not too often; that is left to the assignments. The lectures are made up of ~10min long videos - the perfect length.

## Programming

Programming assignments start with numpy in the first course; no DL frameworks just yet. I find that great: coding networks up from scratch really makes you understand the building blocks. 

Starting course 2 you are introduced first to tensorflow, then to keras. You will still need to implement numpy code from time to time, but coding in the frameworks will take more and more of the emphasis. I think the timing of the transition is well-placed.

I found the assignment topics also interesting. For example, classifying cats vs non-cats (of course), transferring the impressionistic style of Monet to a picture of the Louvre, generating new dinosaur names, generating jazz music, and more.

I do have a beef with the assignments: they are way too easy, involving too much hand-holding. Usually, you are given an empty function that you have to fill in based on instructions and pseudo-code. Very often you only have to write a few lines of code, and much of the assignments can be completed by someone with no knowledge of DL who just reads the pseudo-code carefully.

## Blitzing through the Course

You can audit the course for free. Auditing means you can watch all the videos, but can't take the quizzes and programming assignments. If you want to do those, you have to sign up. You get 7 days for free, after that you'll have to pay.

I was inclined to finish the course quickly, so I decided to first audit the class and watch most of the lectures. Then I signed up, and aimed to complete quizzes plus programming in a week. It wasn't too hard to do that, most assignments take 2 hours tops. 

Once you complete everything you get a lovely certificate:

![png](/assets/img/dl_certificate.jpg)

I don't think the certificate is worth much, but it feels good to have completed this course. As Andrew's (now somewhat aged) machine learning course, I expect it to become the standard go-to beginner's tutorial.
