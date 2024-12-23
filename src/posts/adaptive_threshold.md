---
layout: "post.njk"
title: "Adaptive Threshold" 
description: "or when I should stop reading the rank list."
eleventyNavigation:
    key: Adaptive Threshold
    parent: Posts
---

Adaptive threshold (or Ranked List Truncation) has been developing since the 2000s. Prior to Deep Learning era, the approach is to model the score distribution:

- The similarity score is the mixture of distribution.
- Commonly, it is formed from 2 distributions: (1) distribution of relevant score, and (2) distribution of irrelevant score. 
    - For relevant score: commonly modelled as Gaussian distribution.
    - For irrelevant score: modelled as (truncated) exponential distribution.

To learn the parameters of those distributions, an EM algorithm is applied with labelled training data. A recent attempt uses [extreme value theory](https://towardsdatascience.com/extreme-value-theory-in-a-nutshell-with-various-applications-3260b6a84316) to model the score ([paper](https://dl.acm.org/doi/pdf/10.1145/3539618.3592066)).

Now comes the DL era when we can model a DL model as a discriminative network to determine if the score belongs to relevant/irrelevant products. [BiCut](https://dl.acm.org/doi/abs/10.1145/3341981.3344234) forms the problem as whether the current product is a good terminal point given the ranked list and trains a network to predict whether to continue or stop. [Choppy](https://dl.acm.org/doi/pdf/10.1145/3626772.3657864) on the other hand, went back to the traditional approach: model the score distribution given the ranked list using a DL network.

Despite recent novel approaches to truncated rerank list, this [benchmark](https://dl.acm.org/doi/pdf/10.1145/3626772.3657864) gives some noteworthy insights:

-   DL-based approaches aren't significantly better than unsupervised/simpler approaches (top-K cut off). 
-   Incorporating query embedding to the network also doesn't show any advantages. 
-   Distribution-based approaches are generally better than sequence-based approaches.
-   With good retrievers (stage-1 retrievers), even a simple approach like retrieving top-K can yield good trade-off between effectiveness/efficiency.

Note that the authors use NDCG@10 to evaluate, which is a bit different from our current setting (precision).

What we gather from those findings: 

-   Good embedding is still the key even with/without adaptive threshold.
-   The greedy approach is already good enough. More complicated methods (DL-based) may not be worth it due to negligible improvement and high latency tax.
