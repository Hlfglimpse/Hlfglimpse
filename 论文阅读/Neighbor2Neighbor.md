# CVPR 2021 | Neighbor2Neighbor：仅需噪声图像即可训练任意降噪网络的方法
---
论文地址：[Neighbor2Neighbor: Self-Supervised Denoising From Single Noisy Images](https://openaccess.thecvf.com/content/CVPR2021/html/Huang_Neighbor2Neighbor_Self-Supervised_Denoising_From_Single_Noisy_Images_CVPR_2021_paper.html)
中文解读：[Neighbor2Neighbor](https://mp.weixin.qq.com/s?__biz=MzIwMTE1NjQxMQ==&mid=2247561869&idx=2&sn=22fade50cbd95f008f1ec1794b8a75ab&scene=21#wechat_redirect)

#### 实现思路：
1. 随机邻域子采样-->生成成对的训练图像
2. 使用1生成的样本对训练网络，使用正则化作为额外的损失

#### 先导：[Noise2Noise](http://proceedings.mlr.press/v80/lehtinen18a)|已读
Noise2Noise通过对同一个场景拍摄多张独立的含噪图像即可训练降噪网络。

## 介绍
传统的图像去噪方法，如BM3D、NLM和WNNM，使用输入噪声图像的局部或非局部结构。这些方法是基于非学习的，不需要地面真实图像。

近年来，卷积神经网络(CNN)为图像去噪提供了强大的工具。许多基于CNN的图像去噪器，如DnCNN、U-Net、RED、MemNet和SGN，具有优于传统去噪器的性能。然而，基于CNN的去噪器在很大程度上依赖于大量的Noisy-Clean图像对进行训练。然而，在真实世界的摄影中，收集大量成对的Noisy-Clean训练数据是困难的。此外，由于合成噪声与真实噪声之间的域差距，使用合成Noisy-Clean图像对训练的模型会大大退化（泛化能力差）。

## 相关工作
Supervised-图像去噪：DnCNN
Unsupervised-图像去噪（Only Noisy Images）：
* 传统方法：BM3D、NLM、WNNM
* 深度学习：DIP、Self2Self、Noise as Clean、Noise2Noise、Noise2Void、Noise2Self

## Noise2Noise核心思想
