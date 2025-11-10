---
layout: "post.njk"
title: "Some Quicksort Variants"
date: 2018-01-04
tags:
    - algorithms
---

First, let's review quicksort a bit. Below is a (simple) implementation of this famous algorithm:

```cpp
// quicksort implement
template<typename T>
int partition(vector<T>& a, int lo, int hi) {
    int i = lo, j = hi;
    T v = a[lo];
    while (true) {
        while (a[++i]<=v) if (i == hi) break;
        while (v<=a[--j]) if (j == lo) break;
        if (i >= j)  break;
        swap(a[i], a[j]);
    }
    swap(a[lo], a[j]);
    return j;
}

template<typename T>
void quicksort(vector<T>& a, int lo, int hi) {
    if (lo >= hi-1) return;
    int j = partition(a, lo, hi);

    quicksort(a, lo, j);
    quicksort(a, j+1, hi);
}
```

### Analysis

The complexity is evaluated through the function:

$$ C(N) = n-1 + {1\over n}\sum_{i=0}^{n-1} ( C(i) + C(n-i-1)) $$

In the `partition` part, $n-1$ comparisons are performed, then quicksort is called twice with sizes $i$ and $n-i-1$, the probability for each element in the array is uniformly distributed as ${1\over n}$, so we get the above expression.

The solution method is detailed in books like Introduction to Algorithms, Concrete Mathematics, Introduction to Analysis of Algorithms. Briefly:

1. Multiply both sides by $n$.
2. Write the expression for $n-1$.
3. Calculate $C(n) - C(n-1)$ to get a linear recurrence relation, which can be solved.

## Limiting the Worst-case

One famous method to avoid quicksort's worst-case is to shuffle the input array before using quicksort.
Using [Knuth shuffle](https://en.wikipedia.org/wiki/Fisher-Yates_shuffle) with complexity $\mathcal{O}(N)$ ensures the algorithm's efficiency.
Moreover, shuffling the input makes this improvement, often called randomized quicksort, a classic example in analyzing randomized algorithms.
I have a [post](/vi/randalgs) discussing the analysis of randomized quicksort.

>[!caution]
> Link above is in Vietnamese.

Besides shuffling, there are other approaches:

* Instead of choosing the pivot at the beginning or end, choose the median value.
* Another worst-case is when all values are the same; in this case, use 3way-quicksort.

## Removing Recursion for Small Arrays

This is a trick usable for any divide-and-conquer algorithm: when the recursion gets small enough that the input array is below a certain threshold (10-15 elements), using `insertion sort` will significantly improve performance. Just add this to the quicksort function:

```cpp
///...
if (hi-lo < CUTOFF) {
 insertion_sort(a, lo, hi);
 return;
}
///...
```

## Eliminating Boundary Value Comparisons

With the implementation above, you can remove the `if` statement in the `while` as follows:

* You can remove the `if` when checking `j` because a[lo] < a[lo] never happens.
* To remove the `if` in `i`, before calling quicksort, set a flag value like `MAX_INT`. This always ensures there is a value greater than a[lo].

## Median-of-three and Median-of-five

A classic trick to avoid worst-case: sample 3 or 5 elements, take the median value, and use that as the pivot.

### Tukey ninther quicksort

Use 9 elements instead of 3/5.

## 3way Quicksort

This is the famous algorithm proposed by Dijkstra along with the [Dutch flag problem](https://en.wikipedia.org/wiki/Dutch_national_flag_problem). Used to avoid cases with too many duplicate values in the array. Interestingly, this quicksort version is optimal in terms of entropy. A brief proof is mentioned in Algorithms, R. Sedgewick.

If anyone wonders why Sedgewick is mentioned so much in this post, it's simply because his PhD thesis is titled: "[Quicksort](http://searchworks.stanford.edu/view/870273)".

A rather magical version by Jon Bentley (author of Programming Pearls, collaborated with Sedgewick to prove the entropy-optimal quicksort):

```c
void quicksort(int l, int u){
    int i, m;
    if(l >= u) return;
    m = l;
    for(i = l+1; i<= u; i++)
        if(x[i] < x[l])
            swap(++m, i); //this is where I'm lost. Why the heck does it preincrement?

    swap(l, m);

    quicksort(l, m-1);
    quicksort(m+1, u);
}
```

## Non-recursive Version

Also an improvement proposed by Sedgewick, using a stack instead of recursion. A very detailed C implementation is described [here](http://www.cs.columbia.edu/~hgs/teaching/isp/hw/qsort.c). This version includes the improvements mentioned above:

* CUTOFF
* Median-of-three
* Non-recursive and optimized stack size.

This is also the version of `qsort` in GNU C.

Sedgewick's Java version is also worth exploring: [source code QuickX](https://algs4.cs.princeton.edu/23quicksort/QuickX.java.html).

## Samplesort

This is a modified version of quicksort to run in parallel algorithms.
The idea is to use quicksort to find pivots for each process, then run quicksort on each distributed pivot.
[This article](http://users.atw.hu/parallelcomp/ch09lev1sec5.html) describes and analyzes the algorithm's complexity.

# References

1. Cormen, Thomas H. Introduction to algorithms. MIT press, 2009.
2. Graham, Ronald L., et al. "Concrete mathematics: a foundation for computer science." Computers in Physics 3.5 (1989): 106-107.
3. Sedgewick, Robert, and Philippe Flajolet. An introduction to the analysis of algorithms. Pearson Education India, 1996.
4. Sedgewick, Robert, and Kevin Wayne. Algorithms. Addison-Wesley Professional, 2011.
5. Bentley, Jon. Programming pearls. ACM, 1986.
