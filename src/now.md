---
layout: "post.njk"
title: "Now"
description: "What am I doing"
---

# 2025

## Oct

- Experimented with [Quartz](https://quartz.jzhao.xyz). I gonna use it for my upcoming "Fun with Data Structures & Algorithms" (Definitely need a better name) series.
- Been working on Graph Neural Networks for question classification. Played with [geometric pytorch](https://github.com/pyg-team/pytorch_geometric) quite alot.
- Looking for better note-taking apps. In the past, I used the combination of UpNote, Obsidian, and RemNote.
Lately, I found [Logseq](https://logseq.com/) is a great alternative to the above apps.
- Found [sphinx_literate](https://github.com/eliemichel/sphinx_literate) which maybe the best literate tool at the moment. Look at [this beauty](https://eliemichel.github.io/LearnWebGPU/).
- Read:
  - [Linear Algebra for Data Science, Machine Learning, and Signal Processing](https://www.goodreads.com/book/show/201643974-linear-algebra-for-data-science-machine-learning-and-signal-processing)
  - [System Performance: Enterprise and the Cloud, 2nd Edition](https://www.goodreads.com/book/show/18058001-systems-performance)

## Sep

- The new requirement from Google for apps to publish to store, i.e, [supporting 16kb page size](https://developer.android.com/guide/practices/page-sizes) took me several days to figure out.
- During PR review, I need to revise the current C4 diagram & sequence diagrams of the new service. Previously I used [mermaid](https://mermaid.js.org) for drawing, but later found [planttext](https://www.planttext.com) is much better.
- Studied [spectral theory](https://en.wikipedia.org/wiki/Spectral_theory) and its applications in ML such as [spectral clustering](https://en.wikipedia.org/wiki/Spectral_clustering), Graph SVM, and recommendation.
- Studied [queueing theory](https://en.wikipedia.org/wiki/Queueing_theory) for computer system performance analysis.
- Read:
  - [Linear Algebra for Data Science, Machine Learning, and Signal Processing](https://www.goodreads.com/book/show/201643974-linear-algebra-for-data-science-machine-learning-and-signal-processing)
  - [The Art of Computer Systems Performance Analysis](https://www.goodreads.com/book/show/430782.The_Art_of_Computer_Systems_Performance_Analysis?ref=nav_sb_ss_1_31)
  - [Queueing Systems, Volume 1: Theory](https://www.goodreads.com/book/show/2298875.Queueing_Systems_Volume_1?ref=nav_sb_ss_2_15)

## August

- Spent considerable time on model deployment. I wanted to break the existing design of our ML infrastructure which is out dated and troublesome to deployed. Went to [MLServer](https://mlserver.readthedocs.io/en/latest/getting-started/index.html), simplified the deployment by removing the dependencies on other service, also removed several redudant communication between services. At the end, I still need update 4 different services.
- Started the final semester at NUS. I took 2 courses which seems unrelated to each other: [Graph Machine Learning](https://nusmods.com/courses/CS5284/graph-machine-learning), [Computer System Performance Analysis](https://nusmods.com/courses/CS5239/computer-system-performance-analysis).
- Reading:
  - [Test-driven development in Go](https://www.goodreads.com/book/show/121382396-test-driven-development-in-go).
  - [Cloud Native Go](https://www.goodreads.com/book/show/55767844-cloud-native-go).
  - [Learning Go](https://www.goodreads.com/book/show/55841848-learning-go): about to finish, good book so far. too verbose for my taste.
  - [tmux 3](https://www.goodreads.com/book/show/228141869-tmux-3): Quick read, learnt some new tricks.
  - [Systems Performance: Enterprise and the Cloud](https://www.goodreads.com/book/show/18058001-systems-performance).
  - [Graph Neural Networks in Action](https://www.goodreads.com/book/show/61397620-graph-neural-networks-in-action).

## July

- Designed and implemented an LLM-based product ingestion service. Due to the latency of LLM inference, integrating this service with the existing product indexing pipeline would violate current SLA requirements.
- The new service is implemented in Golang (previously I want to use Python - but app size may affect service startup time). Some books helped me a lot:
  - [Test-driven development in Go](https://www.goodreads.com/book/show/121382396-test-driven-development-in-go).
  - [Cloud Native Go](https://www.goodreads.com/book/show/55767844-cloud-native-go).
  - [Learning Go](https://www.goodreads.com/book/show/55841848-learning-go).

## Jun

- On-device ML deployment: Upgrade our customized Mediapipe for the latest Unity (6.1) as well as the new SDK from Android & iOS. The in-house version is way too old and has many issues, I will probably need to fork mediapipe again and re-implement our SDKs.

- Develop a product summarizer service using ChatGPT. POC is easy, developing a production-ready service is not. The main challenge is the fact that LLM is not a "real-time" service, and to save cost, we may need to use Batch API. For that, a whole new service need to be developed, focusing on batch processing and handling race condition between database updates and batch processing.

- Read:
  - [AI-Powered Search](https://www.goodreads.com/book/show/223393598-ai-powered-search).
  - [x] [Algorithmic Thinking](https://www.amazon.com/Algorithmic-Thinking-2nd-Problem-Based-Introduction).
  - [x] [Distributed Services with Go](https://www.goodreads.com/review/show/5620033205)

## May

- Read:
  - [AI-Powered Search](https://www.goodreads.com/book/show/223393598-ai-powered-search).
  - [Algorithmic Thinking](https://www.amazon.com/Algorithmic-Thinking-2nd-Problem-Based-Introduction).

## Apr

- Finished both Cloud Computing & Text Mining courses. Both are practical and I pretty like them, although I wish I can spent more times on some topics taught in lectures.
- Worked on:
  - Non-English product search: adding non-English supports to the indexing backend and autocomplete services.
  - Synonym set support: It's more about allowing merchandisers to define their our product taxonomy, the most tricky part is how to adapt vector search to the customized definition from users w/o re-training models for each customer.
- Read:
  - [AI-Powered Search](https://www.goodreads.com/book/show/223393598-ai-powered-search).
  - [Algorithmic Thinking](https://www.amazon.com/Algorithmic-Thinking-2nd-Problem-Based-Introduction).

## Mar

- Spent a considerable effort to hunt down search bad cases reported by customers. Reproducing issues is easy, but actually pinning the root cause is a completely different story. Long story short, it is due to wrong expanding terms for sparse models.
- Developed new codebase for embedding finetuning. Loved [uv](https://github.com/astral-sh/uv) after completely switching to it. I also reported some bugs to [neural-cherche](https://github.com/raphaelsty/neural-cherche/issues?q=is%3Aissue%20state%3Aopen%20author%3Adangkhoasdc). Still struggled to get good performance on Splade, SparseEmbed gave me some hope, but not much.
- Reading
  - [Introduction to Information Retrieval](https://nlp.stanford.edu/IR-book/information-retrieval-book.html)
  - [Amazon Web Services in Action](https://www.goodreads.com/book/show/60828856-amazon-web-services-in-action-third-edition): Assisted in completing assignments.
  - [AI-Powered Search](https://www.goodreads.com/book/show/223393598-ai-powered-search):  Engaging read, though some chapters were slightly disappointing.
- Traveled to Bangkok: What a journey. Much fun, best food in SEA (aside from VN), and got scammed.
- Study:
  - Tried some event detection models and implemented event deduplication. I don't like the idea of using LLM for everything, but LLM actually is the best out-of-the-box solution for event detection.
  - Lots of coding for the other project: learned more about OpenAPI, FastAPI, mongoDB …

## Feb

- A lot of coding & hacking:
  - Developing backend services for sport facility recommendation.
  - Play around with event detection and knowledge graph construction.

- Reading
  - [Speech and Language Processing](https://web.stanford.edu/~jurafsky/slp3/)
  - [x] DNF [Mastering Regular Expressions](https://www.goodreads.com/book/show/583628.Mastering_Regular_Expressions?ac=1&from_search=true&qid=8SA0b4fk0c&rank=1). [My short review](https://www.goodreads.com/review/show/4888412307)

## Jan

- ~~Working on~~ . DNF:
  - Spell checker - I'll write a post about modern design of spell checker for product search.
  - Introduce personalization to rerank.
  - Try [LoRA](https://huggingface.co/docs/peft/main/en/conceptual_guides/lora) on language models.

- study@NUS: this semester I'll take [Cloud Computing](https://nusmods.com/courses/CS5224/cloud-computing) and [Text Mining](https://nusmods.com/courses/CS5246/text-mining) courses.

- Reading
  - [Cloud Computing](https://www.goodreads.com/book/show/17133059-cloud-computing)
  - [Introduction to Information Retrieval](https://nlp.stanford.edu/IR-book/information-retrieval-book.html)
  - [Programming Pearls](https://www.goodreads.com/book/show/52084.Programming_Pearls): Will go through all exercises in the book.

- Done:
  - [DevOps, DataOps, MLOps](https://www.coursera.org/learn/devops-dataops-mlops-duke): 2/5 - NOT Recommended.
  - [GNU Make Book](https://nostarch.com/gnumake): [Review](https://www.goodreads.com/review/show/3546681067).

# 2024

## Dec

- Reading [The Silmarillion](https://en.wikipedia.org/wiki/The_Silmarillion).
- Working on [threshold optimization](/posts/adaptive_threshold).
  - [x] Accuracy is maintained while performance improves between 50-80%, the first feature is released at the start of Y25.
- Improving multi-lingual search quality by finetuning [BGE-M3](https://huggingface.co/BAAI/bge-m3).
  - [x] It was a huge pain :angry: :angry:. I stopped working on it, the training is not stable with some random spikes of gradients that completely destroys the training.
- Studying: MLOps, AWS.
- [x] Overhauled [my homepage](http://ltdk.me). I like the simplicity of [the new theme](https://github.com/CondensedMilk7/eleventy-academic-template).
  - Also added [vale](https://vale.sh/) to my workflow.
  - Decoupled the deployment of [lora](https://ltdk-lora.netlify.app/) from the homepage.
  - Upgraded to 11ty v3.
  - Added [Github comments](https://utteranc.es)
- [x] (VN) Reviewed [Dune](https://www.youtube.com/shorts/JWC_Tpqe9eE).

# 2023

## May

- Playing around with [SAM](https://segment-anything.com/).
- Reading [Designing Data-Intensive Applications](https://www.goodreads.com/en/book/show/23463279). It is wayyyy overdue. I should have read this book long before.
- Reading [The Algorithm Design Manual](https://www.goodreads.com/book/show/425208.The_Algorithm_Design_Manual?ref=nav_sb_ss_1_27). A fun read so far, most of the exercises can be practiced on Leetcode.
