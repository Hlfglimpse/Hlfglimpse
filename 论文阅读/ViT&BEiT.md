# Transformer & ViT & BERT & BEiT 原理解析
---
## Transformer ： Attention is all you need

### 中文解析：[Transformer](https://zhuanlan.zhihu.com/p/338817680)
![Transformer](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230529162515.png)

### Encoder
#### Encoder输入：Embedding（单词+位置）
![Embedding](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530115218.png)
**引入Positional Encoding：** 因为 Transformer 不采用 RNN 的结构，而是使用全局信息，不能利用单词的顺序信息，而这部分信息对于 NLP 来说非常重要。所以 Transformer 中使用位置 Embedding 保存单词在序列中的相对或绝对位置。

#### 自注意力机制：self-attention
![self attention](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530210001.png)
![self attention输出](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530210311.png)
矩阵 Q,K,V 是将输入乘上线性变换矩阵（权重矩阵）得到的

#### 多头注意力机制：Multi-Head Attention
![Multi-Head Attention](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530210729.png)
![Multi-Head Attention输出](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530212325.png)

#### Add & Norm
![Add & Norm](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530212446.png)

#### Feed Forward
![Feed Forward](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530212525.png)

### Decoder
![Decoder](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530212804.png)
通过 Masked 操作可以防止第 i 个单词知道 i+1 个单词之后的信息

### 总结
Transformer与RNN 不同，可以比较好地并行训练。
Transformer本身是不能利用单词的顺序信息的，因此需要在输入中添加位置Embedding，否则Transformer就是一个词袋模型了。
Transformer的重点是 Self-Attention 结构，其中用到的 Q, K, V矩阵通过输出进行线性变换得到。
Transformer中 Multi-Head Attention 中有多个 Self-Attention，可以捕获单词之间多种维度上的相关系数attention score。

---
## ViT : Vision Transformer
wait