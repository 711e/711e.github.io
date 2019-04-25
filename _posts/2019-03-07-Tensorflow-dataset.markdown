---
layout: post
title:  "Tensorflow Dataset 读取"
crawlertitle: "Tensorflow Dataset 读取"
summary: "Dataset的batch读取"
date:   2019-03-07 12:11:10 +0700
categories: posts
tags: ['tensorflow']
author: 711E
---

>Dataset是存储Tensor结构的类，它可以保存一批Tensor结构，以供模型来训练或者测试
##### 1.首先将数据读入内存，然后使用`tf.data.Dataset`

```
images =
labels =
data = tf.data.Dataset.from_tensor_slices((images, labels
# type(data):<class 'tensorflow.python.data.ops.dataset_ops.TensorSliceDataset'>
data = data.shuffle(1000)
data = data.batch(batch_size)
print(data.output_shapes)
print(data.output_types)
iterator = tf.data.Iterator.from_structure(data.output_types, data.output_shapes)
# 构建迭代器
data = interator.make_initializer(data)
# 初始化迭代器
with tf.Session() as sess:
  sess.run(data)
  try:
    images, labels = iterator.get_next()
  except tf.errors.OutOfRangeError:
  # 迭代器iterator只能往前遍历，如果遍历完之后还调用get_next()的话，会报tf.errors.OutOfRangeError错误，因此需要使用try-catch
    sess.run(data)
```

***
>接口说明：
`tf.data.Dataset.from_tensor_slices`
* 这个接口允许我们传递一个或多个Tensor结构给Dataset因为默认把Tensor的第一个维度作为数据数目的标识，所以要保持数据结构中第一维的一致性
* 第一维被认为是数据的数量
* 该接口可以接受任何Iterator，包括字典
