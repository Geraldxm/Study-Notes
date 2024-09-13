## 0. 示意图

![yolov5s_structure](../../pics/yolov5s_structure.png)
## 1. 名词解释

### &emsp;Yolo V3

- cfg文件网络图：可以用netron查看yolo的网络结构图，[网络可视化工具netron详细安装流程_pip install natten_江大白*的博客-CSDN博客](https://blog.csdn.net/nan355655600/article/details/106245563)
- yolo3的结构图如下![yolov4](../../../pics/yolov3_structure.png)
	- CBL、Res Unit、ResX 是三个基本组件
		- CBL：由 Conv、Batch Normalization、Leaky Relu 三个网络组成
			- Conv：卷积层，用于调整图像特征。**神经网络采用卷积操作是因为这样可以提取图像的局部特征，从而更好地进行图像分类、目标检测等任务。**对输入图像采用多个卷积核进行卷积操作，从而得到一组新的特征图。通过对输入图像和卷积核进行乘积和求和运算来实现的。
			- Batch Normalization：用于加速神经网络训练，使得同批次的各个特征分布相近，网络更加容易训练。它的实现方法是在每一层输出的时候做一遍归一化操作。直观上可以理解为对网络中间某一层的激活值进行标准化处理。
			- Leaky Relu：激活函数，用于增加神经网络的非线性性。它的实现方法是在激活函数中加入一个小的斜率，从而使得负数输入也有输出。
		- Residual Unit：残差单元
		- ResX：由一个**CBL**和**X**个残差组件构成，是Yolov3中的大组件
	- Concat 张量拼接，改变维度大小
	- add 张量相加，不改变维度大小
- one-stage：直接对输入图像应用算法并输出类别和相应的定位的目标检测方法。它只需要一个单一的网络就能够同时完成定位和分类两件事，例如YOLOv1和SSD。而 two-stage 是一种基于Region Proposal的目标检测算法，需要先使用启发式方法或者CNN网络产生Region Proposal，然后再在Region Proposal上做分类与回归。这类算法准确度高，但速度慢。
- Darknet-53：[Darknet-53是一种深度卷积神经网络模型，用于图像分类和目标检测任务。它是YOLOv3的骨干网络，由Joseph Redmon和Ali Farhadi等人在2018年提出。Darknet-53使用53个卷积层，包括52个3×3的卷积层和一个1×1的卷积层，以及5个Max Pooling层。](https://zhuanlan.zhihu.com/p/619820181)[1](https://zhuanlan.zhihu.com/p/619820181)[2](https://zhuanlan.zhihu.com/p/561831173)[3](https://wenku.csdn.net/answer/dc30f8638b124b3bbca8aa392b002a3b)
- anchor锚框：[anchor锚框是在目标检测中使用的一种参考框，用于预测框计算做参考。在目标检测中，常出现的anchor box是锚框，表示固定的参考框。锚框是以每个像素为中心，生成多个缩放比和宽高比不同的边界框。这些边界框被称为锚框（anchor box）。在训练阶段，是把anchor box作为训练样本，为了训练样本我们需要为每个锚框标注两类标签：一是锚框所含目标的类别；二是真实边界框相对锚框的偏移量。](https://zhuanlan.zhihu.com/p/63024247)[1](https://zhuanlan.zhihu.com/p/63024247)[2](https://zhuanlan.zhihu.com/p/55824651)[3](https://www.jianshu.com/p/39d5eed65552)[4](https://zhuanlan.zhihu.com/p/450451509)
- FPN结构：[FPN（Feature Pyramid Networks）是一种用于目标检测的神经网络结构，由两个部分组成：自底向上的特征提取网络和自顶向下的特征融合网络。它的主要思想是通过自底向上的特征提取网络和自顶向下的特征融合网络，将不同尺度的特征图进行融合，得到一个多尺度的特征金字塔，从而在不同尺度上检测出目标。FPN结构可以用于 Faster R-CNN、Mask R-CNN 等目标检测算法中。](https://blog.csdn.net/weixin_44751294/article/details/117638189)[1](https://blog.csdn.net/weixin_44751294/article/details/117638189)[2](https://www.cnblogs.com/hansjorn/p/14295889.html)[3](https://zhuanlan.zhihu.com/p/82746292)

### &emsp;Yolo v4
- 多了CSP结构，PAN结构，整体框架和 `Yolov3` 相同，使用新算法对各个子结构进行了改进，结构图如下![yolov4](../../../pics/yolov4_structure.webp)

### &emsp;Yolo v5

- Input 输入端
	- 单张图像，分为RGB三个通道，尺寸固定。
	- Mosaic数据增强
	- 自适应锚框计算
	- 自适应图片缩放
- Beckbone 骨干部分
	- Focus结构，主要用于降低图像分辨率，将一张4a * 4a的图像以像素为单位进行拆分，成为4个a * a的图像
	- CBL结构，即ConvBLock，由一个3x3卷积、一个BatchNorm层和一个LeakyRelu层构成
	- CSP结构，先过一个CBL，再过m层ResUnit，此为一个分支；另外一个分支是输入仅进行一次卷积。两个分支合并后，进行归一化、激活函数和CBL层产生输出，形成了一个CSP层。
- Neck 解码部分
	- FPN+PAN结构
- Prediction 预测部分
	- GIOU_Loss
- 输出部分：
	- (分类数 + 5(x坐标，y坐标，宽，高，置信度)) * n个anchor（n个尺度下）