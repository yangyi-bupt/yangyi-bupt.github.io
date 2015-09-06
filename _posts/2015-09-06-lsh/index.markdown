---
layout: post
title:  局部敏感哈希(Local Sensitive Hashing，LSH)总结
date:   2015-08-28 15:19:12
categories: test
---
# 局部敏感哈希(Local Sensitive Hashing，LSH)总结

### 什么是局部敏感哈希(Local Sensitive Hashing，LSH)
说到Hash，大家都很熟悉，是一种典型的Key-Value结构，最常见的算法莫过于MD5。其设计思想是使Key集合中的任意关键字能够尽可能均匀的变换到Value空间中，不同的Key对应不同的Value，即使Key值只有轻微变化，Value值也会发生很大地变化。这样特性可以作为文件的唯一标识，在做下载校验时我们就使用了这个特性。但是有没有这样一种Hash呢？他能够使相似Key值计算出的Value值相同或在某种度量下相近呢？甚至得到的Value值能够保留原始文件的信息，这样相同或相近的文件能够以Hash的方式被快速检索出来，或用作快速的相似性比对。局部敏感哈希（Local Sensitive Hashing，LSH）正好满足了这种需求，在大规模数据处理中应用非常广泛，例如已下场景

> - **近似检测（Near-duplicate detection）**：通常运用在网页去重方面。在搜索中往往会遇到内容相似的重复页面，它们中大多是由于网站之间转载造成的。可以对页面计算LSH，通过查找相等或相近的LSH值找到Near-duplicate。
> - **图像、音频检索**：通常图像、音频文件都比较大，并且比较起来相对麻烦，我们可以事先对其计算LSH，用作信息指纹，这样可以给定一个文件的LSH值，快速找到与其相等或相近的图像和文件。
> - **聚类**：将LSH值作为样本特征，将相同或相近的LSH值的样本合并在一起作为一个类别。
