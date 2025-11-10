---
layout: "post.njk"
title: "Review: Selected Papers on Computer Science"
date: 2018-01-15
tags:
    - books
---

Book Info:

|           | Description                                    |
| --------- | ---------------------------------------- |
| Title   | Selected Papers on Computer Science [[Amazon](https://www.amazon.com/Selected-Papers-Computer-Science-Lecture/dp/1881526917)] |
| Author  | Donald Knuth                             |
| Pages  | 276                                      |

This is the most accessible book from Don Knuth. Although it was published
nearly 20 years ago, it still is a classic computer science book. On Amazon,
there is an [interesting comment](https://www.amazon.com/gp/customer-reviews/R2BNAZLQDF5NI8/ref=cm_cr_arp_d_rvw_ttl?ie=UTF8&ASIN=1881526917) about the book from Peter Norvig (Director
of Google Research). The major topic in the book is the origination of
computer science in the period in which the discipline is a new thing. Through
chapters, we can see there were many debates and struggles among scientists
about whether computer science is truly a "science" and not a branch of
mathematics [Chapter 1, 2, 3].

This makes me think about the current state of Deep Learning. Maybe 5 or 10
years later, Deep Learning will become a separate discipline as Computer
Science segregated from mathematics several decades ago.

There are especially interesting chapters in the book which I can describe
as below:

- Chapter 0: a general overview about Computer Science.
- Chapter 1: Computer Science and its relation to mathematics: the difference
between modern mathematics and computer science. Besides, the author also mentioned
the analysis of the classic algorithm: hashing.
- Chapter 2 and 3: The overview about algorithms as well as the approach by
which the author solves algorithmic problems. Although the chapter is published
long time ago (1976-77) which maybe quite new at that time, in my opinion these
mentioned algorithm, namely the shortest paths, searching and
combinatorial optimizations, become classic research in CS nowadays.
- Chapter 6-9: Theory and Practice: the whole book is distilled into these chapters.
Historic text actively discuss the most important aspects in CS.
- Chapter 11-13: The history of Computer Science: From ancient civilization uses
*algorithms* to solve practice problems to the very first analysis of John von
Neumann about merge sort.

# History of Computer Science and Deep Learning

While reading the book, I had the feeling that the period of 1950-1975 perhaps
exploded into computer science research, which is pretty much similar to Deep
Learning nowadays. That was the time when there were few universities opened
Computer Science department and people still debated about the name of this
science, whether its name is "Computer Science", "Information Technology",
or "Information Processing". That is also the time when people thought that
the problem which can only be solved on $\mathcal{O}(N^2)$ actually can be solved
in $\mathcal{O}(N \lg N)$, the time when there were not any mathematical tools
for analyzing algorithms.

How about Deep Learning?

Nowadays, people remain skeptical about Deep Learning in many aspects. Somebody
compared it to [alchemy](https://www.amazon.com/Selected-Papers-Computer-Science-Lecture/dp/1881526917) because of the lack of rigorous analysis and mathematical fundamentals.
However, according to the current development of Deep Learning and avoiding
the media hype, I am confident about the future of Deep Learning. At least,
in my opinion, it will become an interdisciplinary field and completely transform
into "chemistry". In retrospect, perhaps Computer Science was compared to
"alchemy" in the period of 1940-50 due to its lack of rigor.

# Study about History of Computer Science

I was fascinated by the analyses in detail about "ancient" algorithms as well
as the elaborate way to discuss the draft of merge sort from John von Neumann.
IMO, this really is the way people should study about the history of Computer
Science. It is not about memorizing who and when algorithms were created, it
is about the motivation and approach which the inventor tackled the problem
as well as analyzing the methods in the circumstances in which the technology is
limited. Through these insights, we will respect the contribution from algorithms
and their authors. In addition, we can gain more methods, approaches for other
problems.

Don Knuth is especially interested in this particular subject, there are
many videos and documents in which he discussed exhaustively:

- [Let's Not Dumb Down the History of Computer Science](https://www.youtube.com/watch?v=gAXdDEQveKw):
it is worth every minute watching. I love this comment from Youtube: "Discover how discoveries are discovered".
- History of pattern generation algorithms: [[fasc4b](http://www.cs.utsa.edu/~wagner/knuth/fasc4b.pdf)]
- Hamiltonian path: [[fasc8a](http://www-cs-faculty.stanford.edu/~knuth/fasc8a.ps.gz)].
