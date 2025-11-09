---
layout: "post.njk"
title: "MobileOne"
eleventyNavigation:
    key: MobileOne
    parent: Posts
date: 2022-08-06
tags:
    - deep learning
---
Right now I'm working on lightweight detection models for mobile devices.
Just recently, Apple has just released a new backbone called MobileOne
([paper](https://arxiv.org/abs/2206.04040), [code](https://github.com/apple/ml-mobileone)),
and it looks promising.
Although adapting a completely new backbone at the very end of the project is a bit tricky,
their performance (at least from the paper) convinces me to give it a try.

## Main Ideas

- Decoupling train-time and inference-time architectures
using a linearly over-parameterized model at train-time
and re-parameterizing the linear structures at inference.
  - Introduce a trivial **over-parameterization branches**.
- Relaxing regularization throughout training
to prevent the small capacity of lightweight models being over-regularized.

## Observations & Proposed methods

### Model Design
>
> [!info]
> Latency is moderately correlated with FLOPs and weakly correlated with parameter counts.

- No surprise to me at all.
- Good old RELU is still a good choice for designing lightweight models.

> [!info]
> Two key factors that affect runtime performance are memory access cost and degree of parallelism.

- Memory access increases in multi-branch architectures
as activations from each branch have to be stored to compute the next tensor in the graph.
- Avoid using Squeeze-Excite block because it forces synchronization.

- MobileOne block is a residual block consisting:
  - $k$ blocks of depthwise convolutional layer.
  - A pointwise layer.

- The main point is that during inference, the model is re-parameterized so that
there is no branch in the model. Detail of the method is described in the MobileOne Block section.

### Training

- Apply the cosine annealing scheduler to weight decay.

Other techniques mentioned:

- Progressive learning curriculum.
- Auto augmentation.
