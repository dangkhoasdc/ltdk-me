---
layout: "post.njk"
title: "LTDK"
description: "LTDK's Personal Homepage"
---

## Résumé
### Experiences
**TLDR**: [shorter version](https://www.overleaf.com/read/xrksrvbjptky#7a572b)

I'm currently a Senior Machine Learning Engineer at [Visenze](https://www.visenze.com/) working on [making product search better](https://github.com/dangkhoasdc/awesome-vector-database):
- Re-designed [Multisearch](https://www.visenze.com/discovery-suite/modules/multi-search/) backend, i.e., crafting the new search logic, and developing various cool features to enhance end-user experiences such as: natural filtering, boosting mechanism, rerank & recommendation services. I also lead the effort to improve search quality from implementing algorithm codebase, experimenting & finetuning text embedding, to designing virtual agents for annotation tasks.
- Vector search engine: conducted experiments on [vector search algorithms](https://github.com/dangkhoasdc/awesome-vector-database), benchmarked search quality of SIMD-based vector calculation. ^[Changing the default quantized vector quantization from SDC to ADC. It seems stupidly simple, but it was a huge pain since the engine API always assumes that both query vectors and index vectors are quantized], tuned optimal HNSW with replication settings.
- Detection Models: overhauled annotation guidelines, upgraded the training framework from Detectron to Pytorch^[the sweet old ancient time of DL], developed and released multiple detection models across all Visenze solutions (search, tagging, recommendation).

I also spent about 2 years at Visenze developing on-device ML solutions:

1. Built a 3D object labelling solution. It comprises: (1) an AR mobile app capturing objects and collect 3D data, (2) an Unity tool for importing and refining raw data, and (3) a DL training framework for 3D object detection.
2. Built several computer vision solutions ([a sneak peak](https://www.youtube.com/shorts/SMwoToz2V54)) on mobile devices. I developed DL models designed for low memory usage and fast inference to maintain 30 FPS constraint. I integrated [mediapipe](https://github.com/google-ai-edge/mediapipe) to the existing Unity games via [native plugins](https://docs.unity3d.com/Manual/PluginsForIOS.html). The game has more than 10M downloads in Play Store (Android), and stands at top-30 Education apps on iOS Store.

There are other projects I got involved:

- Re-designed the sequential recommendation algorithm.
- Improved exact product search via new a re-rank logic & advanced data augmentations^[While doing this, I anticipated [Meta's competition](https://www.drivendata.org/competitions/80/competition-image-similarity-2-dev/leaderboard/) and got #12 on the leaderboard].

#### Past

Before joining Visenze, I spent 2.5 years as a research assistant in [Prof Ngai-Man Cheung](https://sites.google.com/site/mancheung0407/) lab at [SUTD](https://www.sutd.edu.sg/) focusing on:
- **Hashing-based image retrieval**: We were the one of the first tried to jointly learning hashing and vector embedding in end-to-end manner for retrieval task. I [implemented](https://github.com/dangkhoasdc/sah) most of the proposed methods on Caffe and Torch (not Pytorch)^[The good old day when DL engineers code a model in Lua] and contributed to [10 publications](https://scholar.google.com/citations?user=jdYVIZwAAAAJ&hl=en).
- [Vision-based localization](https://temasek-labs.sutd.edu.sg/research/tl-projects-completed/telamon-urban-area-scene-based-localization-usbl/): We built a 3D model of Singapore from Google Maps to infer user location based on building photos.
I was responsible for re-implementing the inference framework (originally in MATLAB) to Android devices.
The most challenging task is to implement *fast* SIFT features on Android devices using shader programs while maintaining the accuracy.

## Education

I have been taking [Master of Computing (Artificial Intelligence Specialisation)](https://www.comp.nus.edu.sg/programmes/pg/mai/) at [NUS](https://www.comp.nus.edu.sg). 

## Misc

- A collection of my [favorite books](books).

## Build Status
[![Netlify Status](https://api.netlify.com/api/v1/badges/a50de616-5c47-410a-84ec-c06112a7154f/deploy-status)](https://app.netlify.com/sites/ltdk-me/deploys)
