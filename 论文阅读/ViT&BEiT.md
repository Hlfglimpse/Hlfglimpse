# Transformer & ViT & BERT & BEiT 原理解析
---
## Transformer ： Attention is all you need
![Transformer](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230529162515.png)
### Encoder输入：Embedding（单词+位置）
![Embedding](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230530115218.png)
**引入Positional Encoding：** 因为 Transformer 不采用 RNN 的结构，而是使用全局信息，不能利用单词的顺序信息，而这部分信息对于 NLP 来说非常重要。所以 Transformer 中使用位置 Embedding 保存单词在序列中的相对或绝对位置。
### 自注意力机制 self attention

---
## ViT : Vision Transformer