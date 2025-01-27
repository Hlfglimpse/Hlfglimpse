# 用于高光谱图像去噪的单模型CNN（TGARS | IEEE Transactions on Geoscience and Remote Sensing）

#### 论文地址：[HSI-SDeCNN](https://ieeexplore.ieee.org/document/8913713)

## 主要思路
对于一个数据立方体h\*w\*B（h\*w为空间维度，B为光谱维度），去噪第n个光谱维度，选取K+1个波段的数据输入去噪网络（第n个和K邻域）


## 方法流程
![网络架构](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230420231307.png)
1. **频谱延伸**
    > 为了使得所有的波段都能够得到去噪，对于开头和末尾的波段，将其前and后 $\frac{1}{2}K $ 个波段反向拼接，频谱拼接后的波段为 $\left[ \frac{1}{2}K, ···, 2, \mathbf{1, 2, ···, B-1, B}, B-1, ···, B-\frac{1}{2}K \right] $，即：$h*w*(B+K)$的数据立方体。对于要去噪的第n个光谱维度，选取K+1个波段的数据，即$h*w*(K+1)$的数据立方体。
2. **下采样**
    > ![下采样中分块方法](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230420151853.png)
    > 
    > 将每一个波段的数据按照上图的方式下采样之后进行级联,
    > $$\hat{\mathbf{X}}_n(i, j, t)=\tilde{\mathbf{X}}_n\left(2 i+(t \bmod 2), 2 j+\left\lfloor\frac{t}{2}\right\rfloor,\left\lfloor\frac{t}{4}\right\rfloor\right)$$
    > **该公式仅仅是对每一个波段而言**
    > 
    > 这样上一步的数据立方体将变为$\frac{h}{2}*\frac{w}{2}*4(K+1)$
3. **噪声水平图级联**
    > 在下采样的基础上添加噪声（**添加一个与子采样大小相同的噪声水平图**），使得输入网络的数据立方体大小变为$\frac{h}{2}*\frac{w}{2}*(4(K+1)+1)$，即上图中的灰色区域。

    > 按原文意思，主要就是通过调整这里添加的噪声水平图来使模型可以在不同数据集上取得好的效果（**调参侠？**）。当添加噪声与真实噪声相匹配时，能达到最好的去噪效果。
4. **非线性映射**
    > 所谓的非线性映射即卷积神经网络，下面两个公式就是正常的卷积公式（权重*输入+偏置）
    > ![卷积网络公式](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230420222824.png)

    > CNN的最后输出为$\frac{h}{2}*\frac{w}{2}*4$的数据立方体。
5. **上采样和级联**
    > 所谓的上采样就是下采样的逆过程，将四个块拼接成一幅去噪后的波段图像。
    
    > 所有波段的数据降噪完成后，将其级联叠加到一起得到输入数据的去噪版本。

## 网络各层参数
![网络参数](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230420231205.png)


## 启发思考
![总结](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/41df4b76ec500383ffba95b6333c3c8.jpg)
对于MDDM+（多尺度去摩尔纹网络）的网络来说，这显然是一个针对于RGB三通道图像的的去噪/去摩尔纹网络，网络的每一个输入都为1024\*1024\*3。
对于高光谱数据而言，其通道数显然不止3（对于我们的任务来说，光谱维度为640），修改网络输入的通道数，选取合适（干净）的高光谱数据（噪声可以合成）训练网络。测试在合成噪声数据和真实数据上进行。
> **噪声合成**
> 1. 每个光谱维度添加的噪声完全相同（至少类别相同 e.g. 添加高斯白噪声AWGN）
> 2. 每个光谱维度添加的噪声（类别）随机/多噪声 