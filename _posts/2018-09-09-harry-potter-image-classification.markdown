---
layout: post
category: blog
author: krisztiankovacs
title:  "Harry Potter Image Image Classification"
date:   2018-09-09 09:11:44 +0700
tag:
- deep learning
- deep learning journey
description: Explaining image classification with images downloaded from Google.
---

As an exercise, I decided to try fast.ai's image classification algorithms on a new dataset: ten Harry Potter characters. I used [this](https://github.com/hardikvasa/google-images-download) python script to automatically download images from google. Even though it can only download 100 images per keyword (without additional installations), it is still quite a handy tool.

The benefit of using google images is that it gives you images on any arbitrary topic. The downside is that also contains totally random pictures along with the ones you search for. You can either sort through them manually - which takes time - or you can train your algorithm on the partially corrupted data and hope that the algorithm learns to ignore the occasional mistaken image. I decided to do the latter and it worked quite well on this dataset.

So I downloaded 100 images for the 10 most common Harry Potter characters. Altogether, this resulted in a dataset with somewhat less than 1000 examples (some files were corrupted), spread through 10 classes. 20% was used as a validation set.

For example, here are five images of Hagrid. You can see the mistakes mentioned above: the second image also features Karl Marx, the 5th has nothing to do with Hagrid.

![png](/assets/img/output_7_0.png)

I fit a pretrained image model (resnet34). After some rounds of training, adding data augmentations and using learning rate annealing, I got a final accuracy of around 77%. 

    epoch      trn_loss   val_loss   accuracy                 
        0      1.070325   0.919543   0.757895  
        1      0.882374   0.890763   0.768421                  
        2      0.799392   0.873331   0.768421                  
        3      0.708437   0.842542   0.773684                  
        4      0.62373    0.843961   0.778947                  

After test time augmentation, the accuracy jumped to 82%. 

Looking at the validation images, many of them were falling in two categories: either not depicting the character in question, or showing multiple characters at once. For example, here are the 'Hagrids' the model misclassified:

![png](/assets/img/output_43_0.png)

Only one of these images shows Hagrid, the others are not mistakes in the learning algorithm. Excluding these 'misclassifications', the model's accuracy jumped to 95%. Not bad for only 1000 images and 10 classes!

Just for fun, I used the model to classify this image of me:

![png](/assets/img/output_49_1.png)

Which character would the classifier assign to me?


    The most resembling character is  Draco Malfoy with probability 0.8458218


![png](/assets/img/output_51_0.png)

The associated Jupyter notebook is [here](https://github.com/kk1694/fastai_projects1/blob/master/Harry_Potter_Classification.ipynb)

