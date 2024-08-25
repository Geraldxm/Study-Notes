图片生成模型的思路，抽象出过程就是将训练样本分布 (也就是图片) 映射到另一个分布 (如正态分布噪声)，推理过程就是从新分布中采样映射回原分布。

**生成模型的难题就是判断生成分布与真实分布的相似度，因为我们只知道两者的采样结果，不知道它们的分布表达式。**

[变分自编码器VAE - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/635826906)

[变分自编码器VAE：原来是这么一回事 | 附开源代码 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/34998569)

[从VAE到Diffusion Model：生成式模型初探 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/659566348)

# VAE - 变分自编码器

Variational Auto-Encoder，变分自(动)编码器。

最终目的！产生与训练样本**同分布**但是没有出现过 (不一样) 的新样本。

## 思考过程

我们有一组数据样本 ${x_i}$ ，如果能根据这组样本得到其概率分布 $p(X)$ ，那么我们直接可以对 $p(X)$ 进行采样，这样就能得到所有的 $X$ ，包括在我们已有数据集之外的内容。

退而求其次，我们可以很容易有一个标准正态分布 $Z$ ，以及其概率分布 $p(Z)$ ，那么如果满足如下条件：
$$
p(X)=\sum_{Z}{p(X|Z)p(Z)}
$$
那么我们可以采样一个 $z$ ，然后得到 $x$ ，也能生成。



假设一个正态分布，从中采样得到若干 $z_i$ ，对其做变换得到 $\hat{x_i}=g(z_i)$ ，如何判断构造出来的 $\hat{X}$ 的分布，和数据集中的 $X$ 是否一致？

这里的 **一致** ，其实就是需要寻找一个合适的度量。WGAN 的思路是，干脆使用神经网络训练这个度量。






# GAN - 生成式对抗神经网络

[PaperWeekly 第41期 | 互怼的艺术：从零直达 WGAN-GP (qq.com)](https://mp.weixin.qq.com/s?__biz=MzIwMTc4ODE0Mw==&mid=2247484880&idx=1&sn=4b2e976cc715c9fe2d022ff6923879a8&chksm=96e9da50a19e5346307b54f5ce172e355ccaba890aa157ce50fda68eeaccba6ea05425f6ad76&scene=21#wechat_redirect)

]