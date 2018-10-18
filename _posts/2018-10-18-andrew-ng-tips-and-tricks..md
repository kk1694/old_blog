---
layout: post
category: blog
author: krisztiankovacs
title:  Tips and Tricks from Andrew Ng's class
date:   2018-10-18 09:11:44 +0700
tag:
- deep learning
- tips and tricks
description: Tips and tricks from Andrew Ng's Coursera DL Specialization
---

Andrew Ng mentioned lots of tips and tricks during his [Coursera class]({%post_url 2018-10-14-review-blitzing-through-the-coursera-dl-specialization%}). Below I list a miscellaneous subset. Many are not even DL specific. They are in no particular order; some people might find them obvious (especially with hindsight). I found them helpful and interesting.

### Random Search beats Grid Search

We often have to optimize multiple hyperparameters. For example, suppose you have a standard feed-forward neural net, with 1 hidden layer. You are trying to decide on the number of hidden units, and the amount of dropout. You have resources to fit multiple models, and compare their results on your validation set.

One way to search the hyperparameter space is grid-search: run all combinations of a discrete subset of parameters. For example, you might consider a network with 50, 100, 150, and 200 hidden units; and dropout rates of 0.1, 0.2, ... 0.5. Take all combinations of these values, and you get 20 different settings to run your network with. 

Or you can just take 20 random samples from relevant parameter range: 50-200 for hidden units, and 0.1-0.5 for dropout.

Why is the second approach better? Because not all hyperparameters have the same impact. Suppose that in this case dropout doesn't make a big difference, but the number of hidden units matters. With grid-search, you have 20 runs, but only sample 4 distinct values of the parameter that matters. With random search, you take 20 samples for the number of hidden units as well.

This effect gets even more pronounced in higher dimensions. The number of runs required for grid-search explodes. Why waste runtime on parameters that might not even matter?

### Multiple minima are not an issue in deep learning

We often illustrate gradient descent with a 2 dimensional picture. In two dimensions it's easy to picture a curve with multiple minima where gradient descent (or any other optimization algorithm) finds a sub-optimal local minima. This intuition doesn't carry over to higher dimensions.

Two have a local minimum, your directional derivative has to be 0 in all directions. In very high dimensions, the probability that happens is fairly small. If you find a local minimum, chances are you hit the global one.

However, your surface will be full of (relatively) flat areas and saddle points (where your gradient is 0 in some directions, but not all). Flat surfaces and saddle points are problematic because they make your update steps tiny, and your optimization algorithm may not find a minimum in a reasonable amount of time. 

### Don't use rank 1 arrays

If you sum an (n, n) matrix in numpy, the result is a (n,) rank 1 array. This result can lead to bugs (what if you summed over the wrong axis?), and makes broadcasting unclear. It's better to avoid these rank 1 arrays for clarity.

Instead, we should sum to a (n, 1) or (1, n) vector. That makes it explicit over which dimension we are summing. We just need to use the option 'keepdims = True'.

Also, we should pepper our code with assertions that check the shape of our arrays. (Putting 'assert W.shape = (x, y)' into our code). The computational overhead is minimal, and the assertions help us find errors quickly.

### Build something quickly, iterate fast

Andrew's recurring suggestion is to quickly iterate. Instead of trying to build a hyper-complex model from scratch, build a simple one, then look at where the largest margins of improvement are. 

To facilitate quick iteration, a single number evaluation metric is extremely helpful. It's hard to iterate if we have multiple metrics, each preferring a different model. To deal with multiple metrics we have two strategies. 

First, we can combine them. For example, we can turn precision and recall into an f1 (or f2) score. 

Alternatively, we can designate satisficing metrics. Satisficing metrics only have to be over (or under) a certain threshold. For example, we might say that the memory requirement our model is a satisficing metric. We want our model to fit into memory, but after that we don't care about its size. We would have our optimizing metric, say the f1 score, with the constraint that our model fits into memory.

### Changing proportions of train/dev/test sets for big data

60/20/20 was a typical train/validation/test split proportion for machine learning in the pre-deep-learning era. However, with tens of millions of examples, this split doesn't make sense anymore. After all, the validation set is only used for monitoring performance and optimizing hyper-parameters, and the test set only serves to calculate our error. Often, 1% of our data is enough for them.

### Human error helping with bias/variance

For many deep learning tasks it is helpful to know, at least approximately, what human error is. For naturally occurring tasks, such as image classification, human error is plausibly close [Bayes optimal error](https://en.wikipedia.org/wiki/Bayes_error_rate). Knowing human/Bayes error we know how much our model can to improve.

Moreover, knowing human error helps us determine if our algorithm suffers from high bias. We normally treat the training set error as a measure of our algorithm's bias, and the difference between our trianing and validation error as the algorithms variance. 

That's not fair though, as some of the training set error might be unavoidable. For example, when doing image classification, some of our training examples might be mislabeled. Even a perfect model would have training set error.

Instead, we should focus on the avoidable bias. Knowing human error comes in handy here. If our model has a 2% training error on an image classification task, but humans also have a 2% error (maybe because of mislabeled examples), we know that reducing bias is not the best margin for improvement. However, if humans have a ~0% error, it is worth trying bias reducing techniques.

### Incorrectly labeled training examples

Not necessarily a problem, as long as there aren't too many of them, and the mislabeling isn't systematic.

### What to do if train/dev sets have different distributions

Validation and test sets should always have the same distributions, but sometimes our training set can have a different one.

For example, suppose we are building an app that classifies pictures into cats vs. non-cats. Our app will be used for images recorded on a smartphone. We have 10000 such images that we can split into a validation and test set.

Our training set is slightly different. We have 1 million pictures downloaded from the internet. These aren't exactly the same as the ones recorded on the phone: they might be higher resolution, the cat is usually in the middle, etc. But we have a lot more of them.

We fit a model. It has 2% training error, but the error on our validation set is a whopping 8%. Does our model suffer from high variance, or is it just our training and validation sets being different?

To answer this question, we can create a separate 'train-dev' set. This is data of the same distribution as our training set that isn't used for training.

In our example, we would set aside a subset of the 1 million images from the internet. We use the rest for training. Now we can compare errors.

If our model has a 8% error on this train-dev set, we know that it suffers from high variance. We could try variance reducing techniques, such as increasing regularization. On the other hand, if it scores 2% on the train-dev set (same as the training error), we know that the problem is the differing distributions for training and validation. We need to collect more mobile phone data so we can train our model on that.

### Few shot learning with Siamese network

Siamese networks look [awesome](https://www.quora.com/What-are-Siamese-neural-networks-what-applications-are-they-good-for-and-why). 

### Word embeddings don't need a complex model

A simple model like skip-grams suffices. To learn embeddings in an efficient way (avoiding the massive computations needed for a softmax classifier) we can use algorithms such as negative sampling or Glove.

