# FFDNet:DnCNN的改进

### 网络架构
![FFDNet](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230524155917.png)

#### 1. 预处理Layer：输入图像$ I \rightarrow F^0 $
![Preprocessing layer](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230525161426.png)

预处理层主要负责将输入图片降采样为四张小图片，并在降采样之后的图片上增加一个噪声map
降采样方法：
![](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230525163442.png)

#### 2. 非线性mapping：卷积层 $ F^1 ··· F^D $
![Conv Layers](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230526095741.png)
每次卷积都会进行zero-padding，使得每次卷积后的空间大小保持一致

#### 3. 后处理Layer：卷积后的输出 $ F^{D+1} \rightarrow O $
![Postprocessing layer](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230526154954.png)