---
layout: post
title:  "MobileNet-SSD"
crawlertitle: "MobileNet-SSD"
summary: "MobileNet-SSD"
date:   2019-04-29 10:37:00 +0700
categories: posts
tags: ['Target detection']
author: 711E
---

#### 一、MobileNet-SSD
主要使用了深度可分离卷积Depthwise Separable Convolution 将卷积核进行分解计算来减少计算量,*MobileNet使用的是3x3的卷积核，所以计算量可以减少8-9倍 (因为比率是1/N+1/9)*

#### 二、深度可分离卷积（Depthwise Separable Convolution）
**引入了两个超参数减少参数量和计算量:**
 * 宽度乘数（Width Multiplier）:[减少输入和输出的 channels ]
 * 分辨率乘数（Resolution Multiplier):[减少输入输出的 feature maps 的大小]
**分为两个步骤**
 * 深度卷积：卷积核的大小是[Dk×Dk×1×M]，所以总的计算量是：Dk⋅Dk⋅M⋅DF⋅DF
 * 逐点卷积：卷积核大小是[1×1×M×N]，所以总的计算量是：M⋅N⋅DF⋅DF

#### 三、网络结构
>MobileNet共有28层（深度卷积和逐点卷积分开来算），标准的卷积结构是卷积层之后跟上Batch Normalization层和Relu激活函数，这里引入Depthwise separable convolution之后，每一层都跟上了BN层和激活函数

![显示图片](http://711e.github.io/assets/images/18_structure.png)

#### 四、宽度乘数
**引入超参数α:**
    目的是使模型变瘦,即输入层的channels个数M，变成αM，输出层的channels个数N变成了αN，所以引入宽度乘数后的总的计算量是：[Dk⋅Dk⋅αM⋅DF⋅DF+αM⋅αN⋅DF⋅DF],一般α∈(0,1]，常取的值是1, 0.75, 0.5, 0.25,大约可以减少参数量和计算量的α2

#### 五、分辨率乘数
**引入超参数ρ:**
    目的是降低图片的分辨率，作用在输入的feature map上，所以再引入分辨率乘数后总的计算量是：[Dk⋅Dk⋅αM⋅ρDF⋅ρDF+αM⋅αN⋅ρDF⋅ρDF],一般输入图片的分辨率是224,192,160,128,大约可以减少计算量的ρ2
