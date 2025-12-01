---
layout: "post.njk"
title: "Generating Inversion Table"
date: 2018-01-16
tags:
    - vi
    - algorithms
    - taocp
eleventyNavigation:
    key: Inversion Table
    parent: Posts
---

The programming exercise is from TAoCP, Vol3, 5.1.1-6:

> Design an algorithm that computes the inversion table $b_1, b_2 \cdots b_n$
> corresponding to a given permutation $a_1a_2 \cdots a_n$ of ${1, 2, \cdots , n}$,
> where the running time is essentially proportional to $n\ log n$ on typical
> computers.

I was really stuck on the solution Knuth given in the book. The author also
mentioned another approach which actually is a modifination of merge sort. But
let first understand the algorithm using bitwise.

# Implementation

The C++ implementation has a bit different from the original one. I used 0-index
array instead of 1-index array as Knuth's version. Frankly, it is not the best
version, I just want to convert the pseudo code to an executable one.

```cpp
#include <iostream>
#include <vector>

using namespace std;

int main(int argc, char const* argv[])
{
    // input
    int n; cin >> n;
    vector<int> v(n, 0);
    for (auto& vi: v) cin >> vi;

    // algorithm: TAoCP vol 3. 5.1.1-6
    // init
    vector<int> b(n, 0);
    vector<int> x((n>>1)+1, 0);
    int k = 0, r, s;
    for (int nn=n; nn>1; nn >>= 1) k++; // compute floor(lg(n))

    for (; k >= 0; k--) { // traversal through bits 0 -> \floor(\lg N)
        for (int s = 0; s <= n>>(k+1); s++) // init array x = 0 \forall elements
            x[s] = 0;

        for (int j = 0; j < n; ++j) {
            r = (v[j] >> k) & 1;
            s = v[j] >> (k+1);

            if (r) x[s] += 1;
            else b[v[j]-1] += x[s];
        }
    }

    // output
    for (auto bi: b) cout << bi << " ";
    cout << endl;

    return 0;
}

```

# Analysis

About the running time, it is discernible since the outer loop of $k$ costs
$\lfloor\lg N\rfloor$ and two inner cost $k+2$ and $N$, respectively.

But how on earth does the algorithm work? It is too subtle to be understand
at the first time we saw the solution.

Given the index of bitstring $k$, we consider 2 strings having the forms
$\overline{s1T}$ and $\overline{s0T}$. Given a fixed $\overline{s}$, $T$ and
any $T'$, we always know that $\overline{s1T'}$ > $\overline{s0T}$. `x[]` plays
a role as a counter which checks how many elements of $\overline{s1T'}$ we have
browsed and the inversion $b[\overline{s0T}]$ updates
its value by $x[\overline{s}]$.

For example, let input be $5, 9, 1, 8, 2, 6, 4, 7, 3$, we have the following
binary codes:

```
5: 0101
9: 1001
1: 0001
8: 1000
2: 0010
6: 0110
4: 0100
7: 0111
3: 0011
```

Let run the algorithm step by step:

1. `k=3`. $\overline{s} = \overline{0}$, `x[0] = 2`. `b = 1 2 2 2 0 2 2 0 0`.
2. `k=2`. Array `x` have two items $x[\overline{0}]$, and $x[\overline{1}]$ whose
values are 4, 0, respectively. `b = 2 3 6 2 0 2 2 0 0`.
3. `k=1`. There are 3 posibilities of $x[s]$, namely $x[\overline{00}]$,
$x[\overline{01}]$, $x[\overline{10}]$ whose values are 2, 2, 0, respectively.
Eventually, b is `2 3 6 3 0 2 2 0 0`.
4. `k=0`, There are 5 items in `x`: $x[\overline{000}] = 1$,
$x[\overline{001}]=1$, $x[\overline{010}]=1$ ,$x[\overline{011}]=1$, $x[\overline{100}]=1$,
we get the final output `b = 2 3 6 4 0 2 2 1 0`.

<!--
The main idea is based on the current index $k$, the algorithm divides the set
of $n$ elements into many subsets based the binary prefix of each number. Later,
it updates the inversion value from the total number of candidates of subsets whose
element is larger than the value that we are currently considering.

For example, given the sequence from the book: $5, 9, 1, 8, 2, 6, 4, 7, 3$.

Firstly, we divide the input into 2 sets: $1, 2, 3, 4, 5, 6, 7$ and $8, 9$.
`x[s]` only counts the candidates of the set whose `r=1`, namely the larger
set. Specifically, when `k=3`, `x = [2]`. `b` is updated based on contemporary
`x`.

Next when `k=2`, we categorize the input into 3 subsets: $1, 2, 3$, $4, 5, 6, 7$ and
$8. 9$. Since we already count the set $8, 9$, we know only check the size
of $4, 5, 6,7 $ and update the inversion of $1, 2, 3$.

When `k=1`, we have 4 subsets: $1$, $2, 3$,

Finally, `k=0` we get $\{1\}$; $\\{2, 3\\}$; $\\{4, 5\\}$, $\\{6, 7\\}$, and $\\{8, 9\\}$.
The algorithms will count candidates on set elements $1, 3, 5, 7, 9$
-->

# The mergesort-based algorithm

Instead of constructing an inversion table, this algorithm count the total
number of inversions in a permutation which utilize merging procedures from
the renowned mergesort.

```cpp
class inversion {
    private:
        vector<int> x, aux;
        long long int cnt;
    public:
        inversion(const vector<int>& x_): x(x_), aux(x_.size()), cnt(0) {
            merge_sort(x, 0, x.size());
        } //ctor

        void merge_sort(vector<int>& a, int low, int high) {
            if (low >= high-1) return ;

            int mid = low + (high-low)/2;

            merge_sort(a, low, mid);
            merge_sort(a, mid, high);

            merge(a, low, mid, high);

        }

        void merge(vector<int>& a, int low, int mid, int high) {
            int subidx_1  = low;
            int subidx_2  = mid;

            for (int j = low; j < high; ++j) {
                if       (subidx_1 >= subidx_2)       aux[j] = a[subidx_2++];
                else if  (subidx_2 >= high)           aux[j] = a[subidx_1++];
                else if  (a[subidx_1] <= a[subidx_2]) aux[j] = a[subidx_1++];
                else {
                    cnt += (mid-subidx_1); // (1)
                    aux[j] = a[subidx_2++];
                }
            }

            // copy back to a
            copy(aux.begin()+low, aux.begin()+high, a.begin()+low);
        }

        inline long long int count() const { return cnt;}
};
```

This is the exercise 5.2.5-21 in TAoCP. Unfortunately, Knuth did not mention
the solution. The only modification is to add `(1)` to the merging step which
counts the number of inversions of `a[subidx_2]`, the item in the second
array we consider while merging two arrays. Since from `mid` to `subidx_2`, all
items are less than or equal to `a[subidx_2]`, so there are 0 inversions. However,
since `a[subidx_1] > a[subidx_2]` it means that all items from `subidx_1` to `mid`
are greater than `a[subidx_2]` given the invariant that two arrays are already
sorted. Therefore, there are `mid-subidx_1` inversions of `a[subidx_2]`.

# Reference

- [gywangmtl's post](http://gywangmtl.blogspot.sg/2013/03/n-log-n.html): the
post trully helps me understand the algorithm. Also, thank you, Google Translates.
