# 从单一图像中盲目去除视觉图案 (Blind Visual Motif Removal from a Singal Image) | CVPR 2019

## 创新点
> 盲去视觉图案/水印：视觉图案/水印的位置、大小、结构均未知

## 相关工作
### 去水印 Watermark removal
> 一般流程：
> 1. 水印检测
> 2. 底层图像重建
> 现有的方法重建单一水印，(指定水印位置)使用算法将水印与原图像分开
### 图像绘画 Image inpainting
> 根据缺失像素的掩码（指定位置）进行图像绘画
> 与去水印不同的是，图像绘画不会考虑半透明水印下包含的原图信息
### 图像恢复 Image restoration
> 去雨，去雾，去反射等都属于图像恢复

## 具体实现








## arxiv论文  Visual Watermark Removal Based on Deep Learning