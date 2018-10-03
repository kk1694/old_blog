---
layout: post
title:  "Deep Learning Journey 1 Month Review"
date:   2018-10-03 09:11:44 +0700
categories: deep learning
---

It has been a busy month. After planning out [how to approach deep learning]({%post_url 2018-09-01-dl-journey-overview%}), I dove straight into it. 

I started with reviewing math and Python syntax. For the needed math, I skimmed through the first part of [Goodfellow's deep learning book](http://www.deeplearningbook.org/), and for Python syntax I went through [Udemy's Python for data science](https://www.udemy.com/python-for-data-science-and-machine-learning-bootcamp) course. 

After that I started completing the excellent fast.ai course (part 1). For each topic, I tried to recreate the notebook from the lectures on a different dataset (such as [this]({%post_url 2018-09-09-harry-potter-image-classification%}) Harry Potter image classification example). I was progressing faster than scheduled, having almost finished the course by the end of week 2.

Making good progress, I decided to commit to additional projects that popped up right around this time. 

The first is the [Inclusive Images](https://www.kaggle.com/c/inclusive-images-challenge) Kaggle competition. Besides being a giant image classification challenge, it has the interesting property of evaluating the submitted models on geographically distinct test data (relative to the training set). I'm looking forward to testing out some of my ideas on how to make image models generalize better.

Google generously donated $1000 worth of computing credits to all participants in this challenge. I obviously wanted to take advantage of this offer, so I spent a good amount of time navigating their cloud options to set up a virtual machine. Getting the machine ready took a surprisingly long amount of time (setting up the VM, configuring SSH, figuring out their network settings to access Jupyter notebooks, downloading the 500+ GB dataset, etc.).

A second unexpected development I decided to take advantage of is Siraj Raval's [Move 37](https://www.youtube.com/watch?v=fRmZck1Dakc) course on reinforcement learning (RL). Originally, I planned to study RL sometime between week 5 to 10, but since this new course just started I thought I would front-load learning the topic.

I am also changing some of my plans going forward. Jeremy Howard recently announced a fresh version of their fast.ai course (the one I just completed) starting in October. A lot of the content is expected to be change, so I'll definitely tag along. However, I don't plan to commit too much to part 2 of their current version (as the library will change), and wait until the next iteration. I plan to watch the lectures for ideas though.

Overall, I'm quite happy with how this month turned out. My greatest improvement has been with pytorch - a library I knew nothing about a month ago, and by now I feel quite confident using it to implement most of the basic DL models.







