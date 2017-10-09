---
layout: photo
title: numpy的附加教程
date: 2017-10-09 21:11:00
categories: skimage教程
description: scikit-image是一个工作在numpy数组上的python图像处理模块
---

## 关于numpy的附加教程 ##
scikit-image通过简单的numpy数组来操作图片，因此，很大一部分对于图片的操作都会用到numpy：

    >>> from skimage import data
    >>> camera = data.camera()
    >>> type(camera)
    <type 'numpy.ndarray'>

查看图片的几何长度和像素大小：
    
    >>> camera.shape
    (512, 512)
    >>> camera.size
    262144
    
查看灰度值的统计信息：

    >>> camera.min(), camera.max()
    (0, 255)
    >>> camera.mean()
    118.31400299072266

numpy数组将图片表示为不同的整数或者浮点数值类型，scikit-image如何处理这些数值和更多其它的信息请看[图片数据类型和含义](http://scikit-image.org/docs/dev/user_guide/data_types.html#data-types)。

