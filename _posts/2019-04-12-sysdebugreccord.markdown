---
layout: post
bg: 'dafu.png'
title: "Debug Record1"
crawlertitle: "About image synthesis"
summary: "记录一些问题，和调试情况"
date: 2019-04-17
tags : ['Image Synthesis']
slug: post-url
author: "711E"
categories: posts
---
2019-04-17
---
* `G_loss = tf.reduce_mean(tf.nn.sigmoid_cross_entropy_with_logits(logits=G_out, labels=tf.ones_like(G_out)))`在这样损失函数的指导下，生成图像会倾向于1，（0，1）表示由黑到白，因此图像会越来越白，这里尝试将`labels = tf.zero_loke(G_out)`，发现G_out越来越黑

***

2019-04-12
---

* 网络：生成器31层，判别器5层，单层数据量控制在6G以下
* 输入：默认(0,1]均匀分布
* 损失：交叉熵
* 优化：RMSprop，G(0.5)，D(0.1)

&nbsp;

* 输出：G由外向中心越来越白，D由外向内平滑，损失收敛
* 原因：考虑网络结构不对称或者损失计算不合适，或者学习率太大，或者编码问题
* 计划：改判别器结构，学习率，输入labelid
