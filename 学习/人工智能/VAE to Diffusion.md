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

我们需要解决一个问题，重新采样生成的 $\hat{X_k}$ 与原来的 $X_k$ 是否对应，能否直接最小化 $D(\hat{X_k},X_k)$ ？我们需要找一个合适的度量，要确认一致。

	WGAN 的思路是，干脆使用神经网络训练这个度量。

## VAE 浮现

![](https://pic1.zhimg.com/80/v2-25f257b89b46996fdfaaf3935a9bfb48_720w.webp)

具体来说，给定一个真实样本 $x_k$ ，我们假设存在一个专属于 $x_k$ 的分布 $p(Z|x_k)$ ，并进一步假设这个分布是（独立的、多元的）正态分布。

我们还会训练一个生成器 $X=g(Z)$ ，希望能把分布 $p(Z|x_k)$ 中采样的一个 $z_k$ 还原为 $x_k$ 。

如果直接假设 $p(Z)$ 是正态分布，然后从中采样 $z_k$ ，很难对应到原来的真实 $x_k$ 。但是现在 $p(Z|x_k)$ 专属于 $x_k$ ，可以说从中采样出来的 $z_k$ 应该还原到 $x_k$ 中去。

如何得到 $p(Z|x_k)$ 这一个正态分布的均值和方差？粗暴的思路就是使用神经网络来拟合。

 构建两个神经网络 $\mu_k = f_1(x_k)$ ， $log{\sigma^2}=f_2(x_k)$ 。用 log 拟合的原因是 log 可正可负，而 $\sigma^2$ 总是非负的。

得到均值和方差后，就得到了这个正态分布，然后可以采样 $z_k$ ，经过一个生成器得到 $\hat{x}_k=g(z_k)$ 

现在可以进行最小化 $D^2(\hat{x}_k,x_k)$ 的操作。

![VAE结构示意图](https://pic1.zhimg.com/80/v2-36c7da0b2fe37bd021699532a2cff1e8_1440w.webp)

## 分布标准化

我们希望最小化 $D^2(\hat{x}_k,x_k)$ ，而重构得到 $z_k$ 会受到噪声的影响，因此神经网络可能会尽可能让方差为 0，但这样就会丧失随机性。

因此 VAE 希望所有的 $p(Z|X)$ 贴近标准正态分布，可以防止噪声为 0。

![](https://pic3.zhimg.com/80/v2-a3f264a40db57e010b7ebf0253198726_1440w.webp)

如何实现向 $\mathcal{N}(0,1)$ 看齐呢？最直接的方法就是加入loss
$$
\mathcal{L}_u=||f_1(X_k)||^2 \space和 \space\mathcal{L}_{log_{\sigma^2}}=||f_2(X_k)||^2
\tag{3}
$$

此时只要希望两者接近 0 即可。

两个 loss 需要调整合适的比例。作者通过添加另一个 loss，来避免比例的问题。

	计算了一般正态分布与标准正态分布的KL散度

![](https://pic4.zhimg.com/80/v2-af1049578e84eddf1c817422aa8a3bbf_1440w.webp)

![推导过程](https://pic3.zhimg.com/80/v2-7a3c7ea64e7f11c475cf35cd44fa3ca2_1440w.webp)
$$\begin{array}{l}
K L\left(N\left(\mu, \sigma^{2}\right) \| N(0,1)\right) \\
=\int \frac{1}{\sqrt{2 \pi \sigma^{2}}} e^{-(x-\mu)^{2} / 2 \sigma^{2}}\left(\log \frac{e^{-(x-\mu)^{2} / 2 \sigma^{2}} / \sqrt{2 \pi \sigma^{2}}}{e^{-x^{2} / 2} / \sqrt{2 \pi}}\right) d x \\
=\int \frac{1}{\sqrt{2 \pi \sigma^{2}}} e^{-(x-\mu)^{2} / 2 \sigma^{2}} \log \left\{\frac{1}{\sqrt{\sigma^{2}}} \exp \left\{\frac{1}{2}\left[x^{2}-(x-\mu)^{2} / \sigma^{2}\right]\right\}\right\} d x \\
=\frac{1}{2} \int \frac{1}{\sqrt{2 \pi \sigma^{2}}} e^{-(x-\mu)^{2} / 2 \sigma^{2}}\left[-\log \sigma^{2}+x^{2}-(x-\mu)^{2} / \sigma^{2}\right] d x
\end{array}$$

## 重参数技巧

我们希望所有的 $p(Z|X)$ 贴近标准正态分布。采样过程不可导，采样结果可导，通过参数变换，使采样的结果能够参与模型训练。

![](https://pic1.zhimg.com/80/v2-39d484abe79242a398d6f57ee3d7dc04_1440w.webp)

## 总结和直觉部分

![VAE的本质结构](https://pic1.zhimg.com/80/v2-784891edddff506ea1670c81767e993c_1440w.webp)

它本质上就是在我们常规的自编码器的基础上，对 encoder 的结果（在VAE中对应着计算均值的网络）加上了“[高斯噪声](https://www.zhihu.com/search?q=%E9%AB%98%E6%96%AF%E5%99%AA%E5%A3%B0&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A34998569%7D)”，使得结果 decoder 能够对噪声有[鲁棒性](https://www.zhihu.com/search?q=%E9%B2%81%E6%A3%92%E6%80%A7&search_source=Entity&hybrid_search_source=Entity&hybrid_search_extra=%7B%22sourceType%22%3A%22article%22%2C%22sourceId%22%3A34998569%7D)；而那个额外的 KL loss（目的是让均值为 0，方差为 1），事实上就是相当于对 encoder 的一个正则项，希望 encoder 出来的东西均有零均值。

另外一个 encoder（对应着计算方差的网络）的作用呢？它是用来**动态调节噪声的强度**的。

当 decoder 还没有训练好时（重构误差远大于 KL loss），就会适当降低噪声（KL loss 增加），使得拟合起来容易一些（重构误差开始下降）。

反之，如果 decoder 训练得还不错时（重构误差小于 KL loss），这时候噪声就会增加（KL loss 减少），使得拟合更加困难了（重构误差又开始增加），这时候 decoder 就要想办法提高它的生成能力了。

重构的过程是希望没噪声的，而 KL loss 则希望有高斯噪声的，两者是对立的。**所以，VAE 跟 GAN 一样，内部其实是包含了一个对抗的过程**，只不过它们两者是混合起来，共同进化的。

VAE 的名字中“变分”，是因为它的推导过程用到了 KL 散度及其性质。

## 条件 VAE

如果有标签数据，那么能不能把标签信息加进去辅助生成样本呢？

希望能够实现控制某个变量来实现生成某一类图像。叫做 **Conditional VAE**。

![](https://pica.zhimg.com/80/v2-d148bf520bb386c0c4bb11756e4798ee_720w.webp)

前面的讨论中，我们期望 $Z$ 的分布具有零均值和单位方差，我们通过了 KL Loss 来实现。

加入类别信息 $Y$ 后，我们只需让模型训练到同一个类的样本有一个对应的均值 $\mu_{y}$ 即可。这样，每一个类就对应一个正态分布，在生成时可以通过均值来控制生成图像的类别。

![](https://pic2.zhimg.com/80/v2-6cfa68ced2a4a089f8db3da7236f7129_720w.webp)


# GAN - 生成式对抗神经网络

[PaperWeekly 第41期 | 互怼的艺术：从零直达 WGAN-GP (qq.com)](https://mp.weixin.qq.com/s?__biz=MzIwMTc4ODE0Mw==&mid=2247484880&idx=1&sn=4b2e976cc715c9fe2d022ff6923879a8&chksm=96e9da50a19e5346307b54f5ce172e355ccaba890aa157ce50fda68eeaccba6ea05425f6ad76&scene=21#wechat_redirect)

# DDPM

