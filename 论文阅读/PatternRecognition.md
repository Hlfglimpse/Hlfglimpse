# 模式识别平时作业
## 作业1
![题目1](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230512111515.png)

1. **求解最大后验概率判决函数，即最小错误率贝叶斯决策**
    > 根据贝叶斯公式求解 $ P\left(\omega_i \mid x\right) $
    > $$ P\left(\omega_i \mid x\right)=\frac{P\left(\omega_i, x\right)}{P(x)}=\frac{P\left(x \mid \omega_i\right) P\left(\omega_i\right)}{P(x)} $$
    > 显然，我们只需要比较 $ P\left(x \mid \omega_i\right) P\left(\omega_i\right) $ 即可：
    > $$ P\left(x \mid \omega_1\right) P\left(\omega_1\right)=\left\{\begin{array}{cc} 0.4x, & 0 \leq x<1 \\0.4\left(2-x\right), & 1 \leq x \leq 2 \\0, & \text { else }\end{array}\right. $$
    > $$ P\left(x \mid \omega_2\right) P\left(\omega_2\right)=\left\{\begin{array}{cc}0.6\left(x-1\right), & 1 \leq x<2 \\0.6\left(3-x\right), & 2 \leq x \leq 3 \\0, & \text { else }\end{array}\right. $$
    > 判决函数：
    > $$ x\in \left\{\begin{array}{cc} \omega_1, & 0 \leq x<1.4 \\ \omega_2, & 1.4 \leq x< 2 \\ \omega_1 or \omega_2, & \text {else} \end{array}\right. $$
2. **总的分类错误概率**
    > $$ \begin{aligned} P\left(e\right)&=P\left(\omega_1\right) P_1\left(e\right) + P\left(\omega_2\right) P_2\left(e\right) \\&=0.4\int_{1.4}^{2}\left(2-x\right)dx + 0.6\int_{1}^{1.4}\left(x-1\right)dx \\&=0.12 \end{aligned} $$

![题目2](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230512151054.png)
1. 最小误判概率准则
    > $$ P\left(x \mid \omega_1\right) P\left(\omega_1\right)=0.18 $$
    > $$ P\left(x \mid \omega_2\right) P\left(\omega_2\right)=0.04 $$
    > 显然 $ P\left(x \mid \omega_1\right) P\left(\omega_1\right) > P\left(x \mid \omega_2\right) P\left(\omega_2\right) $，也即 $ P\left(\omega_1 \mid x\right) > P\left(\omega_2 \mid x\right) $。
    > 
    > 综上所述，按照最小误判概率准则，该细胞正常。
2. 最小损失准则
    > $$ \begin{aligned} P\left(\omega_1 \mid x\right)&=\frac{P\left(\omega_1, x\right)}{P(x)}=\frac{P\left(x \mid \omega_1\right) P\left(\omega_1\right)}{P(x)} \\&=\frac{P\left(x \mid \omega_1\right) P\left(\omega_1\right)}{P\left(x \mid \omega_1\right) P\left(\omega_1\right)+P\left(x \mid \omega_2\right) P\left(\omega_2\right)} \\&=\frac{9}{11} \end{aligned} $$
    > 同理：
    > $$ P\left(\omega_2 \mid x\right)=\frac{P\left(x \mid \omega_2\right) P\left(\omega_2\right)}{P\left(x \mid \omega_1\right) P\left(\omega_1\right)+P\left(x \mid \omega_2\right) P\left(\omega_2\right)} =\frac{2}{11} $$
    > 损失函数：
    > $$ \begin{aligned} R\left(\alpha_i \mid x\right) &=\left\{\begin{array}{cc} \lambda_{11}P(\omega_1 \mid x) + \lambda_{12}P(\omega_2 \mid x), & x \in \omega_1 \\ \lambda_{21}P(\omega_1 \mid x) + \lambda_{22}P(\omega_2 \mid x), & x \in \omega_2 \end{array}\right. \\&= \left\{\begin{array}{cc} 2/11, & x \in \omega_1 \\ 54/11, & x \in \omega_2 \end{array}\right. \end{aligned} $$
    > 根据最小损失准则：$ x \in \omega_1 $，即该细胞应为正常细胞。