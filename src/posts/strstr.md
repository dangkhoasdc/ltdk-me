---
layout: "post.njk"
title: "strstr" 
description: "or how to do exact match on string"
eleventyNavigation:
    key: strstr
    parent: Posts
---
## Problem
Retuning the index of the first occurrence of `needle` string in `haystack` string, or `-1` if there is no occurrence.
## Brute Force Approach

Andrei has [a thread on Twitter](https://x.com/incomputable/status/1664347304399126528) about `strstr`, his favorite interview question.com](https://x.com/incomputable/status/1664347304399126528).
His solution:
```cpp
const char* mystrstr(const char* haystack, const char* needle) {
    const char* h = haystack;
    const char* n = needle;

    for (;;) {
        if (!*n) return haystack;
    ehm:
        if (!*h) return nullptr;
        if (*n++ != *h++) {
            h = ++haystack;
            n = needle;
            goto ehm;
        }
    }
}
```
It is concise, cool and use some intriguing optimization:
- Increment operators make 5 operators (2 dereferences, 1 comparison, and 2 increments) compresses into just 1 LOC.
- `goto` helps remove the redundant check of `needle` every time we see a new mismatched character.

This is my Python implementation, one can use [this problem on LeetCode](https://leetcode.com/problems/find-the-index-of-the-first-occurrence-in-a-string) to test the correctness:

```python
def strStr(self, haystack: str, needle: str) -> int:
    i, j = 0, 0
    ni, nj = len(haystack), len(needle)
    while i < ni:
        if haystack[i] == needle[j]:
            j += 1
            if j == nj: return i + 1 - nj
        else:
            i -= j
            j = 0
        i += 1
    return -1
```

Python does not use NULL-terminated string, so we need to get the length of each strings to determine when to stop. Plus, additional optimization via `goto` can not be replicated in Python^[To me, `goto` is just cool, imperative PLs should always has it].

An even smaller version uses `for-else`:

```python
def strStr(self, haystack: str, needle: str) -> int:
    ni, nj = len(haystack), len(needle)
    for i in range(ni - nj + 1):
        for j in range(nj):
            if needle[j] != haystack[i+j]: break
        else: return i
    return -1
```


## References
- Charras, Christian, and Thierry Lecroq. "Handbook of exact string matching algorithms." (2004).
