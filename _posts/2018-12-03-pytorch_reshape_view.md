---
layout: post
title: Pytorch-reshape与view的区别
date: 2018-12-03 11:00 +0800
tags: Pytorch, 笔记
---

- Pytorch中`reshape()`与`view()`都可以改变Tensor的shape但是有略微的区别.
- `reshape()`可以由`torch.reshape()`,也可由`torch.Tensor.reshape()`调用
- `view()`只可以由`torch.Tensor.view()`来调用
- `view()`:
    - 不改变Tensor数据，改变Tensor的size(即shape)
    - 对于一个将要被view的Tensor，新的size必须与原来的size与stride兼容,即新的维度必须是以下两种情况:
        -是原有维度的一个子空间
        - 只跨越原有满足邻接条件$stride[i]=stride[i+1]\times size[i+1]$的原有维度$d,d+1,\dots,d+k$\
    - 否则，在view之前必须调用`contiguous()`方法，对于该方法的讨论，见[StackOverflow](https://stackoverflow.com/questions/48915810/pytorch-contiguous)
- `reshape()`:
    - 同样也是返回与input数据量相同，但形状不同的tensor
    - 若满足view的条件，则不会copy，若不满足，则会copy