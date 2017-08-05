---
title: LeetCode刷笔(1)Hamming Distance
layout: post
date: 2017-08-05 14:20:30
tags: LeetCode
categories: OJ
comments: true
---

为什么开始刷题，细想来也说不清是什么莫名的内心悸动，若多年后回顾，确实留下了可观的积累，想必估计是此题在心中引发的嘲讽。笨拙的思路，臃肿的逻辑，以及不堪入目的长度，真不好意思说自己会写Python。先看看这道题吧：

## Problem
The Hamming distance between two integers is the number of positions at which the corresponding bits are different.

Given two integers `x` and `y`, calculate the Hamming distance.

**Note:**
\\(0 \leq x, y \leq {2}^{31}\\)

**Example:**
```
**Input:** x=1, y=4
**Output:** 2
**Explanation:**
1 (0 0 0 1)
4 (0 1 0 0)
     ?   ?
The above arrows point to positions where the corresponding bits are different
```
也不知是怎样的内心源头，每开始做一件新事时，我总会怀有小心翼翼，惴惴不安的忐忑，尽可能多地获取相关信息，便造成了起步缓慢的必然，然而我以为大多的路都是长跑，故对现状安之若素，虽偶有心急，但未有优化契机。

## 背景介绍
在信息论中，汉明距离指的是等长的两个字符序列中，对应位置不同字符数的最小值。换句话说，就是若将一个字符序列修改成与另一个相同，需要替换的最小字符数。其主要应用在编码理论中，更具体的是分组码中，其中将等长字符串看做有限域上的向量。

*   "karolin" 和 "kathrin" 的汉明距离为 3.
*   "karolin" 和 "kerstin" 的汉明距离为 3.
*   1011101 和 1001001 的汉明距离为 2.
*   2173896 和 2233796 的汉明距离为 3.

汉明距离是根据[Richard Hamming](https://en.wikipedia.org/wiki/Richard_Hamming)的名字命名的，他在1950发表一篇关于错误检测与纠错码的论文中提出这个概念。如今此概念被广泛应用于信息论、编码理论以及密码学中。
比如在电信中，通过计数一段固定长度二进制字符翻转位，对错误进行估计，因此有时也称作信号距离。

## 算法实现
Wikipedia上对于更一般情况下汉明距离的Python实现：
``` python
def hamming_distance(s1, s2):
  if len(s1) != len(s2):
    raise ValueError("Undefined for sequences of unequal length")
  return sum(el1 != el2 for el1, el2 in zip(s1, s2))
```
而就本题目而言，字符序列的来源仅为十进制整数转换为的二进制数组，所以更简单的方法是利用二进制按位异或操作。对应的Python实现如下：
``` python
def hamming_distance_for_number(x, y):
  return bit(x^y).count("1")
```

## 总结
在做题目时，坦白地讲我并未想出如此简单的写法，归结原因如下：
*   对Python基础API的不熟悉
*   对仅有数字参与的运算而考虑到效率更高的位操作
