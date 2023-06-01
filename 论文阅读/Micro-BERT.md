# Micron-BERT: BERT-based Facial Micro-Expression Recognition (CVPR 2023)
---
## 创新点
1. **对角微注意力Diagonal Micro-Attention（DMA）**：
检测视频两帧之间的微小差异
2. **兴趣点模块Patch of Interest （PoI）**： 
定位和突出微表情兴趣区域，同时减少背景噪声和干扰。
**可以引入到FER中去**

## 网络结构
![Micro-BERT](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230601151002.png)
> $ \mu $-BERT 五个核心块：
> > **$ \mu $-Encoder：** 将给定的输入图像 $ I_t, I_{t+\delta}$ 编码成向量表示
> 
> > **PoI（Patch of Interest）：** 使 $ \mu $-BERT模型关注微表情区域，减少无关区域的影响
> 
> > **块交换（Blockwise Swapping）：** 使模型专注于主要由帧之间的微差异组成的面部区域
> 
> > **DMA（Diagonal Micro-Attention）：** 使模型专注于主要由帧之间的微差异组成的面部区域
> 
> > **$ \mu $-Decoder：** 将网络内部的向量表示重建为图像