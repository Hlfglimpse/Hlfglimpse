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

### 网络输入
> 由于BERT（前身Transformer）是一个NLP模型，其应用场景的输入为句子（单词序列），参考ViT（Vision Transformer），将一张图片分为若干个patch。
> ![patch](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230602162252.png)

### $ \mu $-Encoder
> 参照Transformer，embedding包括patch本身 $ \alpha(p_t^i) $ 和位置信息$ w(i) $
> ![embedding](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230602164234.png)
> 该paper embedding结构为：centextual token $ z^{CT} $ 和 transformer embedding $ Z_t $，后续会介绍 centextual token
> Encoder Block示意图：
> ![Encoder Block](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230602170956.png)

### $ \mu $-Decoder：与 $ \mu $-Encoder结构对称

### 块交换 Blockwise Swapping
> 与BERT or BEiT所采取的策略不同的是，$ \mu $-BERT并不是采取简单的**掩码**来遮蔽图像中的部分块，而是基于在短时间 $ \delta $ 内,视频的两帧之间相似度很高的假设，用 $ p_{t+\delta}^i $ 替换掉 $ p_t^i $ ，形成新的一帧图像 $ I_{t/s} $。
> 至此，模型通过一个代理任务（从块交换后的图像 $ I_{t/s} $ 恢复 $ I_t $）来训练网络。
> **该idea是论文后续两个改进的前提**

### 对角微注意力DMA
![DMA示意](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230603153303.png)
> 参考注意力机制，paper将后一帧图像 $ P_{t+\delta}^i $ 作为查询Query，合成帧图像 $ P_{t/s} $ 作为Key和Value实现注意力机制。显然，DMA模块可以使模型更加关注 $ I_{t+\delta} $ 和 $ I_t $两帧之间的变化（即Blockwise Swapping的部分）。
![DMA公式](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230603154347.png)

### 兴趣块PoI 
> 上述的Blockwise Swapping和DMA模块使模型具有关注两帧之间微小变化的能力，同时我们希望能够排除背景部分对模型的干扰，使模型能够集中关注人脸区域。（可通过人脸检测或者语义分割得到人脸区域标签），paper使用POI模块来使模型关注人脸部分（不需额外标签）。
>
> 对于合成帧图像 $ I_{t+\delta}$，从该帧中裁剪得到 $ Crop(I_{t+\delta})$，在对图像块进行embedding时，设计了一个centextual token（ $ z^{CT}$）记录图像的上下文信息（embedding时进行，并不是PoI专用，但是仅用于PoI模块）。
![PoI结构](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230603184012.png)
> $ I_{t+\delta}$ 和 $ Crop(I_{t+\delta})$对应的centextual token分别设为 $ p_{t+\delta}^{CT}$ 和 $ p_{t+\delta/c}^{CT}$，计算这两个token的相似度作为PoI的损失。
![PoI模块loss](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230603183322.png)
> 通过计算每一个patch块与centextual token的相似度得分得到 $ S_{t+\delta}$.
> 通过 $ S_{t+\delta}$限制DMA模块关注人脸区域：
![PoI+DMA](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230603190413.png)

### 损失函数
![Loss](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230603190502.png)