---
layout: post
bg: 'dafu.png'
title: "Debug Record2"
crawlertitle: "Debug Record"
summary: "记录一些问题，和调试情况"
date: 2019-04-20
tags : ['Debug Record']
slug: post-url
author: "711E"
categories: posts
---

#### 2019-04-20:Image Synthesis
尽量不要在Session()里放任何tf操作，容易导致内存溢出。
