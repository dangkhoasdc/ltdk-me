---
layout: "post.njk"
title: "LTDK"
description: "LTDK's Personal Homepage"
---

## Résumé

**TLDR**: [shorter version](/assets/cv.pdf)

---

## Experiences

### Now

I'm currently a Senior Machine Learning Engineer at [Visenze](https://www.visenze.com/) working on [making product search better](https://github.com/dangkhoasdc/awesome-vector-database):
- Re-designed [Multisearch](https://www.visenze.com/discovery-suite/modules/multi-search/), i.e., crafting the new search logic, and developing various features to enhance end-user experiences: rerank & recommendation services, natural filtering, boosting mechanism, [adaptive threshold](/posts/adaptive_threshold/), autocompletion service. 
I also lead the effort to improve search quality: from implementing algorithm codebase, experimenting & finetuning text embedding, to designing virtual agents for annotation tasks.

- Vector search engine: conducted experiments on [vector search algorithms](https://github.com/dangkhoasdc/awesome-vector-database), benchmarked search quality of SIMD-based vector calculation. ^[Changing the default quantized vector quantization from SDC to ADC. It seems stupidly simple, but it was a huge pain since the engine API always assumes that both query vectors and index vectors are quantized], tuned optimal HNSW with replication settings.
- [Object Detection](/detect): overhauled annotation guidelines, upgraded the training framework from Detectron to Pytorch^[the sweet old ancient time of DL], developed and released multiple detection models across all Visenze solutions (search, tagging, recommendation).

I also spent about 2 years at Visenze developing on-device ML solutions:

1. Built a 3D object labelling solution. It comprises: (1) an AR mobile app capturing objects and collect 3D data, (2) an Unity tool for importing and refining raw data, and (3) a 3D object detection codebase for training, evaluation and visualization.
2. Delivered virtual try-on ([a sneak peak](https://www.youtube.com/shorts/SMwoToz2V54)), object tracking, and hand gesture recognition solutions on mobile devices.
I developed DL models designed for low memory usage and fast inference to maintain 30 FPS constraint and integrated it to the existing Unity games via native plugins.
The game has more than 10M downloads on Play Store (Android), and stands at top-30 Education apps on iOS Store.

Other projects I got involved:

- Re-designed the sequential recommendation algorithm.
- Improved exact product search via new a re-rank logic & advanced data augmentations^[While doing this, I anticipated [Meta's competition](https://www.drivendata.org/competitions/80/competition-image-similarity-2-dev/leaderboard/) and got #12 on the leaderboard].

### Past

Before joining Visenze, I spent 2.5 years as a research assistant in [Prof Ngai-Man Cheung](https://sites.google.com/site/mancheung0407/) lab at [SUTD](https://www.sutd.edu.sg/) focusing on:
- **Hashing-based image retrieval**: We were the one of the first tried to jointly learning hashing and vector embedding in end-to-end manner for retrieval task. I [implemented](https://github.com/dangkhoasdc/sah) most of the proposed methods on Caffe and Torch (not Pytorch)^[The good old day when DL engineers code a model in Lua] and contributed to [10 publications](https://scholar.google.com/citations?user=jdYVIZwAAAAJ&hl=en).
- [Vision-based localization](https://temasek-labs.sutd.edu.sg/research/tl-projects-completed/telamon-urban-area-scene-based-localization-usbl/): We built a 3D model of Singapore from Google Maps to infer user location based on building photos.
I was responsible for re-implementing the inference framework (originally in MATLAB) to Android devices.
The most challenging task is to implement *fast* SIFT features on Android devices using shader programs while maintaining the accuracy.

## Education

### Now

Since 2023, I have been pursuing [Master of Computing (Artificial Intelligence Specialisation)](https://www.comp.nus.edu.sg/programmes/pg/mai/) (part-time courseworks) at NUS. 
This program allows me to delve into AI topics that I don’t encounter in my daily work. I've completed several projects:
- Menu Recommendation using Deep Learning Critic-Actor Framework [[Github](https://github.com/CS5446-BCKR/RLRS), [Report](/assets/docs/CS5446.pdf)]: Thanks to our team member, we have access to order history of a F&B franchise in Singapore. I led implementation and model training. It helps me realize training RL model is painful :sob::sob:.
- Predicting HDB Rental Price in Singapore [[Github](https://github.com/cs5228-group-1/cs5228-final-project), [Report](/assets/docs/CS5228.pdf)]: we studied rental price increases in Singapore using 2021-2023 HDB data and developed several prediction models, achieving [Top #1](https://www.kaggle.com/competitions/cs5228-2310-final-project/leaderboard?) on the private leaderboard of the competition.
- [Blood Cell Identification](/assets/docs/CS5242.pdf): I proposed an U-Net variant which utilizes segmentation masks to classify 5 leukocytes. It achieves 92.59% accuracy^[TBH, the dataset seems too easy.] on [the CAM16 dataset](https://camelyon16.grand-challenge.org/Data/).
- [LightningCat](/assets/docs/CS5224.pdf): a cloud-based SaaS platform that provides real-time updates on Singapore's sporting facilities, including operational status, capacity, weather-related closures, booking slots, 
through an intuitive map interface to optimize facility usage and foster community engagement.
- [TemporalLens](/assets/docs/CS5246.pdf): an AI-driven pipeline tracking emerging topics, constructs event timelines & knowledge graphs, analyzes sentiment shifts.


### Past

I completed my undergraduate degree at [HCMUS](https://en.hcmus.edu.vn/), where I had the opportunity to engage in several internships:

- I have 1 paper at ICIP on [compact PCA component](https://projet.liris.cnrs.fr/imagine/pub/proceedings/ICIP-2014/Papers/1569902105.pdf)^[My first paper ever.].
- At [JAIST](https://www.jaist.ac.jp/english/), I conducted research on background subtraction methods. 
- At [University of Saskatchewan](https://www.usask.ca/), I derived a new method for [white cell counting problem](https://github.com/dangkhoasdc/CellCounter).

## Skills 
### Programming Languages
- Professions: Python, Go, C++, Java, C#.
- Hobbies: Julia, D, Crystal, Nim, Racket.

### Tools
- Professions: PyTorch, HuggingFace, Mediapipe, OpenCV, Sklearn, Unity, Docker, Latex, XGBoost.
- Hobbies: Raylib, ImGui. 

## Misc

- A collection of my [favorite books](books).

## Build Status
[![Netlify Status](https://api.netlify.com/api/v1/badges/a50de616-5c47-410a-84ec-c06112a7154f/deploy-status)](https://app.netlify.com/sites/ltdk-me/deploys)
