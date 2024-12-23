---
layout: "post.njk"
title: "LTDK"
description: "LTDK's Personal Homepage"
---

TLDR: [shorter version](https://www.overleaf.com/read/xrksrvbjptky#7a572b)

I'm currently a Senior Machine Learning Engineer at [Visenze](https://www.visenze.com/) working on [making product search better](https://github.com/dangkhoasdc/awesome-vector-database):
- Re-designed [Multisearch](https://www.visenze.com/discovery-suite/modules/multi-search/) backend, i.e., crafting the new search logic, and developing various cool features to enhance end-user experiences such as: natural filtering, boosting mechanism, rerank & recommendation services. I also lead the effort to improve search quality from implementing algorithm codebase, experimenting & finetuning text embedding, to designing virtual agents for annotation tasks.
- Vector search engine: conducted experiments on [vector search algorithms](https://github.com/dangkhoasdc/awesome-vector-database), benchmarked search quality of SIMD-based vector calculation. ^[Changing the default quantized vector quantization from SDC to ADC. It seems stupidly simple, but it was a huge pain since the engine API always assumes that both query vectors and index vectors are quantized], tuned optimal HNSW with replication settings.
- Detection Models: overhauled annotation guidelines, upgraded the training framework from Detectron to Pytorch^[the sweet old ancient time of DL], developed and released multiple detection models across all Visenze solutions (search, tagging, recommendation).

I also spent about 2 years at Visenze to develop on-device ML solutions:

1. Built a 3D object labelling solution. It comprises: (1) an AR mobile app that let users capture the object and collect all 3D information, (2) an Unity tool to import and refine raw data, (3) a DL training framework to develop a 3D object detection model.
2. Built several computer vision solutions ([a sneak peak](https://www.youtube.com/shorts/SMwoToz2V54)) on mobile devices. I developed DL models designed for low memory usage and fast inference to maintain 30 FPS constraint. I integrated [mediapipe](https://github.com/google-ai-edge/mediapipe) to the existing Unity games via [native plugins](https://docs.unity3d.com/Manual/PluginsForIOS.html). The game has more than 10M downloads in Play Store (Android), and stands at top-30 Education apps on iOS Store.

# Misc

- A collection of my [favorite books](books).

# Build Status
[![Netlify Status](https://api.netlify.com/api/v1/badges/a50de616-5c47-410a-84ec-c06112a7154f/deploy-status)](https://app.netlify.com/sites/ltdk-me/deploys)
