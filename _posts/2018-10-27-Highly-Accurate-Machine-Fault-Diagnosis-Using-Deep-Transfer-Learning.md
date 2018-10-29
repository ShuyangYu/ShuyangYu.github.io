---
  \
layout:     post
title:      Highly-Accurate Machine Fault Diagnosis Using Deep Transfer Learning
subtitle:   论文笔记
date:       2018-10-27
author:     Y.
catalog: true
tags:
    - paper  
    - Fault Diagnosis
    - transfer learning
---

# Highly-Accurate Machine Fault Diagnosis Using Deep Transfer Learning  

## Main contributions  

1. 基于已有的CNN网络建立新的故障检测框架，底层CNN参数使用pre-trained参数，高层参数和整个框架参数使用部分目标数据fine-tune，网络结构超过十层，快速准确。

2. 在三个不同数据集上的表现均优于现有结果：Induction Motor Dataset，Bearings Dataset，Gearbox dataset。

## Methods  

### Time-frequency Imaging  

为了使用已有的CNN网络，使用Time-frequency Imaging技术将时间序列数据转换成时频域，通常有Short Time Fourier Transform (STFT), Continuous Wavelet Transform (CWT), Wigner-Ville distribution等方法，在这里采用了CWT，目的是将一维时序信号变为二维，以符合CNN网络的输入。

### Transfer Learning and Fine-tuning Strategy  

对于将要使用的深层次网络来说，低层次的表达是可以直接迁移的，即使用已训练好的参数，具体在第几层进行fine-tune，视两个数据集的相似性而定。

### MACHINE FAULT DIAGNOSIS USING DEEP TRANSFER LEARNING  

本文使用VGG-16预训练模型，16层。本文fine-tune了最后三层卷积层和全连接层，结构如下：

![1540628890331](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_16-30-25.png)

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_17-17-22.png)

## Experimental verification

### Induction Motor Dataset

6种Motor condition，其中每个类别1000做训练，100做测试：

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_20-31-05.png)

测试结果，从零训练了一个三层CNN网络用来作对比，本文提出模型训练时间短，准确率高：

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_20-40-54.png)

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_20-41-21.png)

### Bearings Dataset

振动数据信号的收集依据轴承载荷有4种不同的工况（load 0, 1, 2, and 3 hp），每种工况下，有三种故障类型，the rolling element, the inner raceway, and the outer bearings raceway，每种故障类型共3种故障程度（0.007 inches, 0.014 inches, and 0.021 inches），故障共9类。6组实验，前四组实验训练集每类500，共5000，测试集相同，第五组实验，每列100,4中故障程度，共4000；第六组实验每类100，三种程度共3000：

1. Training data and testing data are both from vibration signals under working load of 0 hp. 
2. Training data and testing data are both from vibration signals under working load of 1 hp. 
3. Training data and testing data are both from vibration signals under working load of 2 hp. 
4. Training data and testing data are both from vibration signals under working load of 3 hp. 
5. Training data and testing data are both from vibration signals under working loads of 0-3 hp with balanced samples. 
6. Training data come from vibration signals under working loads 0-2 horse hp while testing data are from working load of 3 hp.

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_20-41-31.png)

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_20-41-46.png)

### Gearbox dataset

5分类问题，四种故障和健康状态：

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_20-42-11.png)

训练集每类1000，共5000，测试集相同，预测结果准确率和训练时间：

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_20-42-18.png)

![](https://raw.githubusercontent.com/ShuyangYu/Picture/master/Snipaste_2018-10-27_20-42-27.png)

