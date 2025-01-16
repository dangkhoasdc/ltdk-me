---
layout: "post.njk"
title: "Adaptive Threshold" 
description: "or when I should stop reading the rank list."
eleventyNavigation:
    key: Adaptive Threshold
    parent: Posts
---

# Survey

Adaptive threshold (or Ranked List Truncation) has been developing since the 2000s. Prior to Deep Learning era, the approach is to model the score distribution:

- The similarity score is the mixture of distribution.
- Commonly, it is formed from 2 distributions: (1) relevant score, and (2) irrelevant score. 
    - Relevant score: commonly modelled as Gaussian distribution.
    - Irrelevant score: modelled as (truncated) exponential distribution.

![Pre-DL approach to adaptive threshold](/assets/images/thres/classic.png)

To learn the parameters of those distributions, an EM algorithm is applied with labelled training data. A recent attempt uses [extreme value theory](https://towardsdatascience.com/extreme-value-theory-in-a-nutshell-with-various-applications-3260b6a84316) to model the score ([paper](https://dl.acm.org/doi/pdf/10.1145/3539618.3592066)).

Now comes the DL era when we can model a DL model as a discriminative network to determine if the score belongs to relevant/irrelevant products. [BiCut](https://dl.acm.org/doi/abs/10.1145/3341981.3344234) forms the problem as whether the current product is a good terminal point given the ranked list and trains a network to predict whether to continue or stop. [Choppy](https://dl.acm.org/doi/pdf/10.1145/3626772.3657864) on the other hand, went back to the traditional approach: modelling the score distribution given the ranked list using a DL network.

Despite recent novel approaches to truncated rerank list, this [benchmark](https://dl.acm.org/doi/pdf/10.1145/3626772.3657864) gives some noteworthy insights:

-   DL-based approaches aren't significantly better than unsupervised/simpler approaches (top-K cut off). 
-   Incorporating query embedding to the network also doesn't show any advantages. 
-   Distribution-based approaches are generally better than sequence-based approaches.
-   With good retrievers (the recall stage), even a simple approach like retrieving top-K can yield good trade-off between effectiveness/efficiency.

![Recent benchmark](/assets/images/thres/benchmark.png)

Note that the authors use NDCG@10 to evaluate.

What we gather from those findings: 

-   Good embedding is still the key even with/without adaptive threshold.
-   The greedy approach is already good enough. More complicated (DL-based) methods may not be worth due to negligible improvement and high latency tax.

# Design

My idea is much simpler: whenever the score drops dramatically (due to the fact that one of the embedding has negligible score), we stop returning results.
Then, the problem becomes [finding the peak](https://github.com/MicahParks/peakdetect)^[I also spotted [a bug](https://github.com/MicahParks/peakdetect/issues/4).] of the change in the stream of scores. 

Below is one example - it shows the score value of top 1000 results with the blue color indicating positive, red as negative and black is unannotated; the leftmost dashed red line shows where the cutoff point.

| Score Visualization | Score Gradient |
|--|--|
|![](/assets/images/thres/1.png)|![](/assets/images/thres/1-change.png)|
|![](/assets/images/thres/2.png)|![](/assets/images/thres/2-change.png)|

For product search, recall is an important factor, hence we don't want the cutoff to be applied prematurely. 
In my implementation, I always return top 50 results with the assumption that it will includes all exact matches and relevant products. 
Beyond the 50th result, there tends to be a mix of relevant/partial relevant results, which can be safely trimmed. 
Plus, using an adaptive threshold helps prevent the reranker from pushing irrelevant products to the top of the list.
The 2nd example shows when my approach does not help, i.e., the cutoff is applied too late and the final results contains a large amount of irrelevant results.
This probably is an exact match search, where users copy product title to the search bar.

Why not use a mixture model approach? 
It needs data to train although ChatGPT can surely annotate them, it would complicate the release timeline. 
Meanwhile, DL-based approach seems too excessive and hasn't shown significant improvement.

# References

1. Arampatzis, Avi, Jaap Kamps, and Stephen Robertson. "Where to stop reading a ranked list? Threshold optimization using truncated score distributions." Proceedings of the 32nd international ACM SIGIR conference on Research and development in information retrieval. 2009.
2. Bahri, Dara, et al. "Choppy: Cut transformer for ranked list truncation." Proceedings of the 43rd International ACM SIGIR Conference on Research and Development in Information Retrieval. 2020.
3. Bahri, Dara, et al. "Surprise: Result List Truncation via Extreme Value Theory." Proceedings of the 46th International ACM SIGIR Conference on Research and Development in Information Retrieval. 2023.
4. Meng, Chuan, et al. "Ranked List Truncation for Large Language Model-based Re-Ranking." Proceedings of the 47th International ACM SIGIR Conference on Research and Development in Information Retrieval. 2024.
5. Brakel, J.P.G. van (2014). "Robust peak detection algorithm using z-scores". Stack Overflow. Available at: https://stackoverflow.com/questions/22583391/peak-signal-detection-in-realtime-timeseries-data/22640362#22640362 (version: 2020-11-08).
