---
layout: "post.njk"
title: "Object Detection on Mobile Devices" 
description: ""
eleventyNavigation:
    key: Object Detection on Mobile Devices
    parent: Posts
date: 2019-01-01
tags:
    - object detection
---
# Introduction

I have been working on image detection on mobile devices for the last 6 weeks,
which is not long enough to delve into some research papers on model compression
or pruning techniques but adequate to get into and conduct some experiments
on some detection models.

Firstly, let look at the detection model and make some terms. A detection
usually (and from some of the state-of-the-art model: RetinaNet) is composed
of 3 components, from bottom to top:
1. Backbone: feature extractions.
2. Region Proposal Module: produce proposals based on feature maps of the backbone
and feed them into the last component.
3. Head predictor: Predict the bounding boxes and label.

In this note, I will talk about all 3 components when we develop an detection
model for mobile devices. Let assume that we are working on Android devices
and the deep learning frameworks on mobiles support some common layers, but
it is not identical to any other frameworks such as Tensorflow, Pytorch. Therefore,
we also have to deal with one more step, namely converting the model trained
from the workstation/servers into the model for mobile devices.

## Backbones

Here is the list of backbone I have been trying:

- Resnet50.
- Resnet36.
- MobileNetv1
- MobileNetv2
- SqueezeNet.

# Conclusions and Takeaways

1. If you have to deal with training dataset, make sure that the 
annotations are consistent and correct because small networks do not have
large capacity to learn from label noise.
2. Lightweight networks behave different between classification and
detection tasks. Make sure that you have proper experiments to justify the
model.
3. [GroupNorm](/posts/groupnorm) is good for detection, use it if it is available.
4. Sometimes, the FPN and head predictor are pretty heavy compared to the
backbone. Some tricks to reduce memory and improve the inference time are:
    * Remove certain octave scales, especially FPN 3.
    * Replace normal Conv layers in FPN branches with Depthwise layer.
    * Reduce anchor scales, aspect ratios or even number of classes if necessary.
5. In general, Depthwise conv is a good choice to replace the normal conv layer.
However, the performance depends on the underlying implementations. You may not
gain any improvements because of it.
6. Different frameworks uses different settings, implementations even with
some de facto layers. While converting the model, make sure that the logic is
correct. You may have to retrain the model to the final settings based on
the mobile framework.


# References
- [MobileNetv2](https://machinethink.net/blog/mobilenet-v2/): Pretty good post about MobileNetv2. The author also mentions the implementation on iOS.

