## 0. 示意图

![yolov5s_structure](../../pics/yolov5s_structure.png)
## 1. 名词解释

### &emsp;YOLO v5

- Input 输入端
	- Mosaic数据增强
	- 自适应锚框计算
	- 自适应图片缩放

- Beckbone 骨干部分
	- Focus结构
	- CSP结构

- Neck 解码部分
	- FPN+PAN结构

- Prediction 预测部分
	- GIOU_Loss
