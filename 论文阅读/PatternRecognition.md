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

## 作业2
![题目1](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230522150210.png)
> 构造似然函数 $ L(\alpha) $：
> $$ L(\alpha)=\prod_{i=1}^n\left[\left( \alpha+1 \right)x_i^ \alpha \right]=(\alpha+1)^n \prod_{i=1}^n x_i^ \alpha $$
> 对似然函数 $ L(\alpha) $ 取对数得：
> $$ \ln(L( \alpha))=n \ln( \alpha+1)+ \alpha \sum_{i=1}^n \ln(x_i) $$
> 令 $ \frac{d \ln L(\alpha)}{d \alpha}=0 $，即：
> $$ \frac{d \ln L(\alpha)}{d \alpha}=\frac{n}{\alpha+1}+\sum_{i=1}^n \ln x_i =0$$
> 得到 $ \alpha $ 的最大似然估计为：
> $$ \alpha=-(1+\frac{n}{\sum_{i=1}^n \ln x_i}) $$

## 作业3
![题目](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230522154445.png)
1. **题目1**
    > 第四个观测是白球：
    > > 第四个观测白球来自1号盒：$ \beta_{white}(1)=1$
    > > 第四个观测白球来自2号盒：$ \beta_{white}(2)=1$
    > > 第四个观测白球来自3号盒：$ \beta_{white}(3)=1$
    >
    > 第三个观测是红球：
    > > 第三个观测红球来自1号盒：$$ \begin{aligned} \beta_{red}(1) &=\alpha_{11}b_{while}(1)\beta_{white}(1)+ \alpha_{12}b_{while}(2)\beta_{white}(2) +\alpha_{13}b_{while}(3)\beta_{white}(3) \\&=0.5*0.5+0.2*0.6+0.3*0.3 \\&=0.46 \end{aligned} $$
    > > 第三个观测红球来自2号盒：$$ \begin{aligned} \beta_{red}(2) &=\alpha_{21}b_{while}(1)\beta_{white}(1)+ \alpha_{22}b_{while}(2)\beta_{white}(2) +\alpha_{23}b_{while}(3)\beta_{white}(3) \\&=0.3*0.5+0.5*0.6+0.2*0.3 \\&=0.51 \end{aligned} $$
    > > 第三个观测红球来自3号盒：$$ \begin{aligned} \beta_{red}(3) &=\alpha_{31}b_{while}(1)\beta_{white}(1)+ \alpha_{32}b_{while}(2)\beta_{white}(2) +\alpha_{33}b_{while}(3)\beta_{white}(3) \\&=0.2*0.5+0.3*0.6+0.5*0.3 \\&=0.43 \end{aligned} $$
    >
    > 第二个观测是白球：
    > > 第二个观测白球来自1号盒：$$ \begin{aligned} \beta_{white}(1) &=\alpha_{11}b_{red}(1)\beta_{red}(1)+ \alpha_{12}b_{red}(2)\beta_{red}(2) +\alpha_{13}b_{red}(3)\beta_{red}(3) \\&=0.5*0.5*0.46+0.2*0.4*0.51+0.3*0.7*0.43 \\&=0.2461 \end{aligned} $$
    > > 第二个观测白球来自2号盒：$$ \begin{aligned} \beta_{white}(2) &=\alpha_{21}b_{red}(1)\beta_{red}(1)+ \alpha_{22}b_{red}(2)\beta_{red}(2) +\alpha_{23}b_{red}(3)\beta_{red}(3) \\&=0.3*0.5*0.46+0.5*0.4*0.51+0.2*0.7*0.43 \\&=0.2312 \end{aligned} $$
    > > 第二个观测白球来自3号盒：$$ \begin{aligned} \beta_{white}(2) &=\alpha_{31}b_{red}(1)\beta_{red}(1)+ \alpha_{32}b_{red}(2)\beta_{red}(2) +\alpha_{33}b_{red}(3)\beta_{red}(3) \\&=0.2*0.5*0.46+0.3*0.4*0.51+0.5*0.7*0.43 \\&=0.2577 \end{aligned} $$
    >
    > 第一个观测是红球：
    > > 第一个观测红球来自1号盒：$$ \begin{aligned} \beta_{red}(1) &=\alpha_{11}b_{while}(1)\beta_{white}(1)+ \alpha_{12}b_{while}(2)\beta_{white}(2) +\alpha_{13}b_{while}(3)\beta_{white}(3) \\&=0.5*0.5*0.2461+0.2*0.6*0.2312+0.3*0.3*0.2577 \\&=0.112462 \end{aligned} $$
    > > 第一个观测红球来自2号盒：$$ \begin{aligned} \beta_{red}(2) &=\alpha_{21}b_{while}(1)\beta_{white}(1)+ \alpha_{22}b_{while}(2)\beta_{white}(2) +\alpha_{23}b_{while}(3)\beta_{white}(3) \\&=0.3*0.5*0.2461+0.5*0.6*0.2312+0.2*0.3*0.2577 \\&=0.121737 \end{aligned} $$
    > > 第一个观测红球来自3号盒：$$ \begin{aligned} \beta_{red}(3) &=\alpha_{31}b_{while}(1)\beta_{white}(1)+ \alpha_{32}b_{while}(2)\beta_{white}(2) +\alpha_{33}b_{while}(3)\beta_{white}(3) \\&=0.2*0.5*0.2461+0.3*0.6*0.2312+0.5*0.3*0.2577 \\&=0.104881 \end{aligned} $$
    >
    > 结合初始状态概率：
    > > 第一个观测红球来自1号盒(结合初始状态概率):$$ \beta_{red}^{'}(1)= \pi_1b_{red}(1)\beta_{red}(1)=0.2*0.5*0.112462=0.0112462 $$
    > > 第一个观测红球来自2号盒(结合初始状态概率):$$ \beta_{red}^{'}(2)= \pi_1b_{red}(2)\beta_{red}(2)=0.4*0.4*0.121737=0.0194779 $$
    > > 第一个观测红球来自3号盒(结合初始状态概率):$$ \beta_{red}^{'}(3)= \pi_1b_{red}(3)\beta_{red}(3)=0.4*0.7*0.104881=0.0293667 $$
    >
    > **终止：**$$ P(O \mid \lambda)=\beta_{red}^{'}(1)+\beta_{red}^{'}(2)+\beta_{red}^{'}(3)=0.0600908 $$
2. **题目2**
    > 第一个观测是红球：
    >> 第一个观测红球来自1号盒：$$ \delta_1(1)=\pi_1 b_{red}(1)=0.2*0.5=0.1 $$
    >>> 此时，最优路径为：1
    >
    >> 第一个观测红球来自2号盒：$$ \delta_1(2)=\pi_2 b_{red}(2)=0.4*0.4=0.16 $$
    >>> 此时，最优路径为：2
    >
    >> 第一个观测红球来自3号盒：$$ \delta_1(3)=\pi_3 b_{red}(3)=0.4*0.7=0.28 $$
    >>> 此时，最优路径为：3
    >
    > 第二个观测是白球：
    >> 第二个观测白球来自1号盒：$$ \begin{aligned} \delta_2(1) &=\max[\delta_1(1) \alpha_{11},\delta_1(2) \alpha_{21},\delta_1(3) \alpha_{31}]b_{white}(1) \\&=\max[0.1*0.5,0.16*0.3,0.28*0.2]*0.5 \\&=0.028 \end{aligned} $$
    >>> 此时，最优路径为：3->1
    >
    >> 第二个观测白球来自2号盒：$$ \begin{aligned} \delta_2(2) &=\max[\delta_1(1) \alpha_{12},\delta_1(2) \alpha_{22},\delta_1(3) \alpha_{32}]b_{white}(2) \\&=\max[0.1*0.2,0.16*0.5,0.28*0.3]*0.6 \\&=0.0504 \end{aligned} $$
    >>> 此时，最优路径为：3->2
    >
    >> 第二个观测白球来自3号盒：$$ \begin{aligned} \delta_2(3) &=\max[\delta_1(1) \alpha_{13},\delta_1(2) \alpha_{23},\delta_1(3) \alpha_{33}]b_{white}(3) \\&=\max[0.1*0.3,0.16*0.2,0.28*0.5]*0.3 \\&=0.042 \end{aligned} $$
    >>> 此时，最优路径为：3->3
    >
    > 第三个观测是红球：
    > > 第三个观测红球来自1号盒：$$ \begin{aligned} \delta_3(1) &=\max[\delta_2(1) \alpha_{11},\delta_2(2) \alpha_{21},\delta_2(3) \alpha_{31}]b_{red}(1) \\&=\max[0.028*0.5,0.0504*0.3,0.042*0.2]*0.5 \\&=0.00756 \end{aligned} $$
    >>> 此时，最优路径为：3->2->1
    >
    > > 第三个观测红球来自2号盒：$$ \begin{aligned} \delta_3(2) &=\max[\delta_2(1) \alpha_{12},\delta_2(2) \alpha_{22},\delta_2(3) \alpha_{32}]b_{red}(2) \\&=\max[0.028*0.2,0.0504*0.5,0.042*0.3]*0.4 \\&=0.01008 \end{aligned} $$
    >>> 此时，最优路径为：3->2->2
    >
    > > 第三个观测红球来自3号盒：$$ \begin{aligned} \delta_3(3) &=\max[\delta_2(1) \alpha_{13},\delta_2(2) \alpha_{23},\delta_2(3) \alpha_{33}]b_{red}(3) \\&=\max[0.028*0.3,0.0504*0.2,0.042*0.5]*0.5 \\&=0.0105 \end{aligned} $$
    >>> 此时，最优路径为：3->3->3
    >
    > 第四个观测是白球：
    > > 第四个观测白球来自1号盒：$$ \begin{aligned} \delta_4(1) &=\max[\delta_3(1) \alpha_{11},\delta_3(2) \alpha_{21},\delta_3(3) \alpha_{31}]b_{white}(1) \\&=\max[0.00756*0.5,0.01008*0.3,0.0105*0.2]*0.5 \\&=0.00189 \end{aligned} $$
    >>> 此时，最优路径为：3->2->1->1
    >
    > > 第四个观测白球来自2号盒：$$ \begin{aligned} \delta_4(2) &=\max[\delta_3(1) \alpha_{12},\delta_3(2) \alpha_{22},\delta_3(3) \alpha_{32}]b_{white}(2) \\&=\max[0.00756*0.2,0.01008*0.5,0.0105*0.3]*0.6 \\&=0.003024 \end{aligned} $$
    >>> 此时，最优路径为：3->2->2->2
    >
    > > 第四个观测白球来自3号盒：$$ \begin{aligned} \delta_4(3) &=\max[\delta_3(1) \alpha_{13},\delta_3(2) \alpha_{23},\delta_3(3) \alpha_{33}]b_{white}(3) \\&=\max[0.00756*0.3,0.01008*0.2,0.0105*0.5]*0.3 \\&=0.001575 \end{aligned} $$
    >>> 此时，最优路径为：3->3->3->3
    >
    >比较第四个观测白球在三个盒子中的概率：$$ \max[0.00189,0.003024,0.001575]=0.003024 $$
    > 因此，根据Viterbi算法，最优路径为：**3->2->2->2**

## 作业4
![题目1](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230531143240.png)
> 1. 点 $ X_a $ 与决策面距离大小：$$ d = \frac{W^T X_a + w_{n+1}}{\sqrt{\sum_{i=1}^n{w_i^2}}} $$
> 
> 2. 证明 $ X_p $ 是使 $ ||X-X_a|| $ 取值最小的 $ X $：
> > 取决策面上任意一点 $ X_r $，线段 $ X_rX_a $ 与决策面的夹角记为 $ \alpha, (\alpha \in [0, \frac{\pi}{2}]) $ ，那么线段 $ X_rX_a $ 在决策面上的投影线段大小为：$$ d_p = ||X_r-X_a||\cos\alpha $$
> > 使 $ ||X_r-X_a|| $ ,也就是使 $ d_p $最小,显然在 $ X_r $ 取 $ X_p $ 时满足条件。

![题目2](https://raw.githubusercontent.com/Hlfglimpse/PicGo/master/20230531154216.png)
> 类均值向量：$$ m_1= \begin{pmatrix} \frac{1}{2} \\ 1 \end{pmatrix},m_2= \begin{pmatrix} 2 \\ -\frac{1}{2} \end{pmatrix} $$
> 类内离散度矩阵：$$ S_1= \begin{pmatrix} \frac{1}{2} & 1 \\ 1 & 2 \end{pmatrix},S_2= \begin{pmatrix} 2 & 1 \\ 1 & \frac{1}{2} \end{pmatrix} $$
> 总类内离散度矩阵：$$ S_w=S_1+S_2=S_2= \begin{pmatrix} \frac{5}{2} & 2 \\ 2 & \frac{5}{2} \end{pmatrix} $$
> 显然， $ S_w $ 非奇异，那么最佳投影方向 $ w $ 为：$$ \begin{aligned} w&=S_w^{-1}(m_1-m_2) \\ &=\begin{pmatrix} \frac{10}{9} & -\frac{8}{9} \\ -\frac{8}{9} & \frac{10}{9} \end{pmatrix} \begin{pmatrix} -\frac{3}{2} \\ \frac{3}{2} \end{pmatrix} \\&=\begin{pmatrix} -\frac{8}{3} \\ \frac{8}{3} \end{pmatrix} \end{aligned} $$
>
> **类内总散度矩阵**表示从总体来看类内各个样本与类之间的离散度