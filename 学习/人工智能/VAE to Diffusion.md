图片生成模型的思路，抽象出过程就是将训练样本分布 (也就是图片) 映射到另一个分布 (如正态分布噪声)，推理过程就是从新分布中采样映射回原分布。

生成模型的难题就是判断生成分布与真实分布的相似度，因为我们只知道两者的采样结果，不知道它们的分布表达式。

[变分自编码器VAE - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/635826906)

[变分自编码器VAE：原来是这么一回事 | 附开源代码 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/34998569)

[从VAE到Diffusion Model：生成式模型初探 - 知乎 (zhihu.com)](https://zhuanlan.zhihu.com/p/659566348)

# VAE - 变分自编码器

Variational Auto-Encoder，变分自(动)编码器。

最终目的！产生与训练样本同分布但是没有出现过 (不一样) 的新样本。

重点是定义训练损失保证实现所想的功能。

![](https://pic3.zhimg.com/v2-d7a52f6f211594a0853993365f51cb82_r.jpg)

