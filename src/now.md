---
layout: "post.njk"
title: "Now"
description: "What am I doing" 
---

# 2025
## April 

- Finished both Cloud Computing & Text Mining courses. Both are practical and I pretty like them, although I wish I can spent more times on some topic taught in lectures.
- Working on:
    - Non-English product search, i.e., adding supports to the indexing backend and autocomplete services.
    - Synonym supports. It's more about allowing merchandisers to define their our product taxonomy, the most tricky part is how to adapt vector search to the customized definition from users w/o re-training models for each customer.

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
