---
layout: "post.njk"
title: "Libra-RCNN" 
description: "Review and Re-implement"
eleventyNavigation:
    key: Libra-RCNN
    parent: Posts
date: 2019-06-13
tags:
    - object detection
---

Pang, Jiangmiao, et al. "[Libra r-cnn: Towards balanced learning for object detection.](https://openaccess.thecvf.com/content_CVPR_2019/papers/Pang_Libra_R-CNN_Towards_Balanced_Learning_for_Object_Detection_CVPR_2019_paper.pdf)" Proceedings of the IEEE/CVF conference on computer vision and pattern recognition. 2019.

# Introduction
Regarding the object detection problem, it seems like the community pays less
attention to training pipeline than other tasks such as network design,
inference improvement. This paper investigates the current problem of the
CNN detection models. They consider the imbalance phenomenon, which is composed
of 3 levels:

1. Sample level.
2. Feature level.
3. Objective level.

They basically are 3 corresponding major components of a detection model:
feature extraction, region proposals, and predictors. Based on such categorization,
they propose the following improvements:

1. IoU-balanced sampling.
2. Balanced feature pyramid.
3. Balanced L1 loss.

So, everything is balanced now.

![](/assets/images/libra_rcnn/balance_force.jpg)


The authors draw a pretty nice figure to demonstrate their points.
![](/assets/images/libra_rcnn/imbalance_level.jpg)

# Review and Analysis
![](/assets/images/libra_rcnn/libra_rcnn.jpg)

Now, let take a look at 3 aspects of imbalance training from the point of view
of this paper.

## Sample level Imbalance

There are many circumstances in which the training data, especially the easy samples, becomes imbalance:

- Data distribution: it becomes severe if the training data is bias to certain
viewpoints, pose or object shape. The model needs to focus on the hard positive
samples in order to gain more gradient, and thus it is able to learn and
generalize. Otherwise, it keeps learning from easy samples, which make the
gradient is almost 0. These cases are considered as *hard positives*, which
is not examined in this paper.

- Data sampling: two-stage detectors use data sampling in order to train the
model. Even though the number of images is small (2 or 4) and the number of
grouthtruth is also relatively small. Considering the COCO dataset, even though
we have 80 labels, not all of the images has a large number of boxes. Meanwhile,
the sampler usually generates thousands of regions, hence the easy negative samples
dominate the whole set.

- This is the well-known problem in object detection, hence many papers tried to
tackle this problem. There are 2 methods worth mentioning:

    * OHEM: Instead of freezing the network, computing the hard negative examples,
    adding them to the training set and continuing training the model, OHEM directly
    computes all the ROIs in a batch and selects the hard negatives from them.

    * Focal loss takes a whole different approach. It reshapes the standard
    cross entropy loss such that it down-weights the loss assigned to
    well-classified examples. The authors argue that Focal Loss shows little
    improvement in R-CNN. It may be true, I only tested this loss on one-stage
    detection models. However, Yolov3's authors also mentioned Focal Loss does
    not work well on their model.

## Feature level imbalance

This quote is interesting when they talk about FPN and PANet - region proposal
methods that use multi-scale feature mapping:

> The methods inspire us that the low-level and high-level information are complementary
> for object detection. The approach that how they are utilized to integrate
> the pyramidal representations determines the detection performance. ...
> Our study reveals that the integrated features should possess balanced information from each resolution.
> But the sequential manner in the aforementioned methods will make integrated feature focus more on adjacent resolution but less on others.
> The semantic information contained in non-adjacent levels would be diluted once per fusion during the information flow.

This section of the paper is quite weak and not convincing. They do not mention
any experiments to justify their arguments. In addition, they said they inspired
from the aforementioned methods but did not elaborate on how they come up with
the proposed method.

## Objective level imbalance

Nowadays, a typical object detection model carries two tasks: label classification
and box regression. Depend on the difficulty and the distribution of training data,
the ultimate objective may not be integrated well from two separate losses.
For example, the box regression is compromised, hence it leads to the high
performance on box results but poor on concept results.

Imbalance easy-hard samples also affect the gradient of the model. If the easy
samples make up the majority of the batch, the gradient is dominated by
the hard examples and thus the model learns nothing from the easy samples.
Despite being called "easy samples", it does not mean that there is nothing
to learn from the easy samples. The reason is that once the model is able
to spot the "easy" feature in the image, it discards the remaining visual
features remaining in the image. In other words, it only looks at some
particular position/feature in the image which makes it easy to learn.

---

In my opinion, sample imbalance and feature imbalance are the most important
aspects we have to deal with. It seems like CNN can learn different viewpoints
as long as we provide proper training data. Nonetheless, we can not feed
a huge amount of data of every object of every single angle. Secondly, the
annotation quality dramatically changes because of the quality, characteristic
of the image. For example, stock images, product images get clear, accurate
bounding box label. Photos that are taken from smartphones, random images on Internet,
on the other hand, are completely different stories. By looking at the annotation
of COCO dataset, you know what I mean.

# Proposed Methods

## Balanced Feature Pyramid

![](/assets/images/libra_rcnn/balance_fpn.jpg)

The algorithm for this method is described as the following:

1. *Rescaling*: Resize all feature map into 1 size (intermediate size) using interpolation and max-pooling.
2. *Integrating*: Sum all rescaled feature and normalize it.
3. *Refining*: Directly use convolutions or use non-local module such as Gaussian non-local attention.
4. *Strengthening*: Rescale the obtained feature to the original resolutions.

We can interpret those steps as applying a Pooling layer to form high-level
feature, which resembles the final pooling of image retrieval. Hence, it means
to improve the abstract level of the feature.

## Balanced L1 Loss

The whole formulation of the loss can be seen in the paper. In summary, the authors want to: (1) cap the gradient of the box regression in order to balance with the classification gradient and (2) improve the gradient of the easy samples.

# Experiment results

From the result of ablation experiments in Table 2, there are some interesting observations:

* In general, combining 3 methods dramatically improves the average precision
of large objects. However, there is not much effect shown in the small objects.
In my opinion, small objects still are the most difficult aspect to improve detection models.
* IoU balanced Sampling and Balanced L1 Loss clearly help to improve the Average
Precision at IoU=0.75. It means they produce boxes closer to the ground truth.
* The same trend also can be seen on RetinaNet in which the authors only two
methods (Balanced Feature Pyramid and Balanced L1 Loss). Again, the proposed methods
improve the overall performance with quite a large margin (+5%), especially on
the large objects.


## Implementation

In the next two weeks, I will implement the balanced feature pyramid and
the balanced L1 loss. I am not sure if I have time for IoU sampler since my
focus is on RetinaNet which naturally does not use sampler (but we can trick it
a bit and utilize the component). Even though the authors have already released
source code using Pytorch, I have to rewrite the whole things through caffe2
and Detectron. It may take a while.

---

### Weighted Component Loss

In couple of experiments, I have found that there is a big gap between box
precision and concept precision. So, my hypothesis is that the box regression
loss actually dominates the whole loss of the model. From the that, I halve
the weight of the box regression and train the model. Here is the results:

| Model | Concept Recall | Concept Precision|
|-------|----------------|-------------------|
|resnet36_tiny12_v0800 (baseline, size 256)| 0.4000| 0.4445|
|resnet36_tiny15_v0900 | 0.4122 (+3.05%) | 0.4685 (+5.40%) |
|resnet36_tiny14_v0800 (baseline, size 320)| 0.4194 | 0.4651|
|resnet36_tiny16_v0800| 0.3906 (-6.8%)| 0.4984 (+7.16)|

`tiny12` and `tiny15` are basically the same except `tiny15` uses smaller loss weight for box regression (0.5 instead of 1.0). The same settings are applied for `tiny14` and `tiny16`, respectively. From the result, we can see by balancing the loss component, even with the naive approach, it indeed helps the overall performance. However, the second setting is difficult to observe the performance gain. I better use the mAP instead.
