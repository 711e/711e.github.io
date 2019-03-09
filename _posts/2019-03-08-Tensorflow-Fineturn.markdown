---
layout: post
title:  "Tensorflow Fineturn VGG16"
crawlertitle: "Tensorflow Fineturn VGG16"
summary: "Tensorflow 迁移学习"
date:   2019-03-09 13:04:00 +0700
categories: posts
tags: 'tensorflow'
author: 711E
---

VGG16权重文件：VGG16.npy
![vgg16](http://711e.github.io/assets/images/vgg16.png)

##### 1.dataset.py - 读数据集
###### (1)从csv或者文件路径里读图片的地址和标签
输入:file_dir
输出:images_path,labels
###### (2)从图片地址读图片
输入:images_path
输出:images
```
def read_images(images_path):
    # 读取图片
    images = []
    # images = tf.placeholder(dtype=tf.float32)
    for i in range(N):
        image = tf.read_file(images_path[i])
        # 解码
        image = tf.image.decode_jpeg(image, 3)
        image = tf.image.resize_images(image, (256, 512))
        # 正则化，将数值[0,255]转化为[-1,1]
        image = image * 1.0 / 127.5 - 1.0
        images.append(image)
        if i % 1 == 0:
            print(i)
    return images
```

###### (3)迭代器
输入:images,labels,batch_size
输出:data_batch
```
def get_batch(images, labels, batch_size):
    labels = tf.cast(labels, dtype=tf.string)
    images = tf.cast(images, dtype=tf.float32)
    data = tf.data.Dataset.from_tensor_slices({'image': images, 'label': labels})
    data_batch = data.batch(batch_size)
    data_batch = data_batch.make_one_shot_iterator()
    data_batch = data_batch.get_next()
    return data_batch
```

##### 2.构建model
###### (1)原生Tensorflow

###### (2)slim引入
