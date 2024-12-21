---
layout: "post.njk"
title: "LTDK"
description: "LTDK's Personal Homepage"
---

Ta da ta da, something about myself.

I'm currently a Senior Machine Learning Engineer at [Visenze](https://www.visenze.com/) working on [making product search better](https://github.com/dangkhoasdc/awesome-vector-database).
My noticeable projects:

- Low-level optimization: change the default quantized vector quantization from SDC to ADC.^[It seems stupidly simple, but it was a huge pain since the API in the engine always assumes that both query vectors and index vectors are quantized].
- [Multisearch](https://www.visenze.com/discovery-suite/modules/multi-search/): completely re-design the search backend. From design the architecture, select backend, derive the algorithm and logic flow, to develop various cool features to enhance end user experiences such as: natural filtering, boosting mechanism, rerank services, adaptive threshold.

I also spent about 2 years at Visenze to develop on-device ML solutions:

1. Built a 3D object labelling solution. It comprises: (1) a AR mobile app that let users capture the object, save all 3D information, (2) an Unity tool to import and refine raw data, (3) a DL training framework to develop a 3D object detection model.
2. Built several computer vision solutions ([a sneak peak](https://www.youtube.com/shorts/SMwoToz2V54)) on mobile devices. I built DL models designed for low memory usage and fast inference to maintain 30 FPS constraint. I integrated [mediapipe](https://github.com/google-ai-edge/mediapipe) to the existing Unity games via [native plugins](https://docs.unity3d.com/Manual/PluginsForIOS.html). 

# Misc

- A collection of my [favorite books](books).

# Build Status
[![Netlify Status](https://api.netlify.com/api/v1/badges/a50de616-5c47-410a-84ec-c06112a7154f/deploy-status)](https://app.netlify.com/sites/ltdk-me/deploys)
