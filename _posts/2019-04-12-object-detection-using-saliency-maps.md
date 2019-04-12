---
layout: post
category: blog
author: krisztiankovacs
title:  "Object Localization Using Saliency Maps"
date:   2019-04-12 09:11:44 +0700
tag: 
- external articles
description: How to use saliency maps for object localization.
---

I'm participating in [fellowship.ai](https://fellowship.ai/); and one the projects I was working on involved object localization. Specifically, how to do it if we only have class labels (no bounding box or segmentation info).

Turns out we can use class activation maps, using techniques such as [GradCAM](https://arxiv.org/abs/1610.02391) or [GradCAM++](https://arxiv.org/abs/1710.11063) to obtain a map from any classifier; which can then be converted into a bounding box. 

See our [team's article](https://platform.ai/blog/page/9/attention-cropping-in-platform-ai/) describing the approach in more detail.
