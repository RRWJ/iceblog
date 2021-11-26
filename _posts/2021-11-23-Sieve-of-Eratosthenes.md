---
layout: post
title: Sieve of Eratosthenes
subtitle: 埃拉托斯特尼筛法
date: 2021-11-23
tags: [算法][Leetcode]
comments: false
---
#### 204. 计数质数
#### 参考内容：https://en.wikipedia.org/wiki/Sieve_of_Eratosthenes
#### 算法过程：
```
algorithm Sieve of Eratosthenes is
    input: an integer n > 1.
    output: all prime numbers from 2 through n.

    let A be an array of Boolean values, indexed by integers 2 to n,
    initially all set to true.
    
    for i = 2, 3, 4, ..., not exceeding √n do
        if A[i] is true
            for j = i2, i2+i, i2+2i, i2+3i, ..., not exceeding n do
                A[j] := false

    return all i such that A[i] is true.
```
#### 时间复杂度 O(n log log n)