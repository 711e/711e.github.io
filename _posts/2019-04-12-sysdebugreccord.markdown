---
layout: post
bg: 'dafu.png'
title: "Debug Record"
crawlertitle: "About SYS"
summary: "记录记录一些问题，和调试情况"
date: 2019-04-12
tags : ['Markdown']
slug: post-url
author: "711E"
categories: posts
---

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
