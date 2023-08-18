## 0. 超参数部分

```python
imgsz = (640, 640)  # 输入图片的大小  
conf_thres = 0.25  # object置信度阈值 默认0.25  
iou_thres = 0.45  # 做nms的iou阈值 默认0.45  
max_det = 1000  # 每张图片最多的目标数量  
device = 'cpu'  # 设置代码执行的设备  
classes = None  # 在nms中是否是只保留某些特定的类  
agnostic_nms = False  # 进行nms是否也除去不同类别之间的框  
augment = False  # 预测是否也要采用数据增强 TTAvisualize = False  # 特征图可视化 默认FALSE  
half = False  # 是否使用半精度 Float16 推理  
dnn = False  # 使用OpenCV DNN进行ONNX推理
```

超参数部分目前只能手动在 .py 文件中修改，后续使用 `argparse` 实现，使其能在命令行中修改参数。

## 1. 图片处理

关键部分就是图片的处理。

```python
def detect_(img):  
    im0 = img  
    # 调用 letterbox 函数对图像调整大小，以适应模型的输入尺寸  
    im = letterbox(im0)[0]  
    # 颜色通道转换  
    im = im.transpose((2, 0, 1))[::-1]  # HWC to CHW, BGR to RGB  
    # www 函数将一个内存不连续存储的数组转换为内存连续存储的数组，使得运行速度更快。  
    im = np.ascontiguousarray(im)  
    # 将 numpy 数组转换为 PyTorch 张量，并将其移动到指定的设备上（例如 CPU, GPU）。  
    im = from_numpy(im).to(device)  
    # uint8 to fp16/32  
    im = im.half() if half else im.float()  
    # 0 - 255 to 0.0 - 1.0  
    im /= 255  
    # 这行代码检查输入张量 im 的维度是否为 3。如果是，则在最前面添加一个轴以使其变成四维张量。 im.ndimension() 返回输入张量 im 的维度数。如果它的值为 3，则意味着张量是三维的。  
    # 在这种情况下，使用切片操作 [None] 来在最前面添加一个轴。这相当于使用 np.newaxis 或 None 来扩展张量的形状。例如，如果原始张量的形状为 (3, 4, 5)，则添加一个轴后，新的形状将变为 (1,    # 3, 4, 5)。  
    if im.ndimension() == 3:  
        im = im[None]  # 增加维度  
    # 使用模型对图像进行推理，并获取第一个输出  
    pred = model(im)[0]  
    # NMS 处理  
    pred = non_max_suppression(pred, conf_thres, iou_thres, classes, agnostic_nms, max_det=max_det)  
    # 用于存放结果  
    dett = []  
    for i, det in enumerate(pred):  # per image 每张图片  
        # 若有检测结果  
        if len(det):  
            # 调用 scale_boxes 函数将检测框的坐标转换为原始图像的坐标系，并对坐标进行四舍五入。  
            det[:, :4] = scale_boxes(im.shape[2:], det[:, :4], im0.shape).round()  
            # 遍历当前图像的所有检测框，计算出检测框的左上角和右下角坐标，并将其转换为整数类型；计算出检测框的中心点坐标，并将其添加到结果列表中。  
            for *xyxy, conf, cls in reversed(det):  
                # x1, y1, x2, y2 = int(xyxy[0].numpy()), int(xyxy[1].numpy()), int(xyxy[2].numpy()), int(xyxy[  
                # 3].numpy())                x1, y1, x2, y2 = xyxy[0].numpy(), xyxy[1].numpy(), xyxy[2].numpy(), xyxy[3].numpy()  
                # p1 = int((x1 + x2) / 2)  
                # p2 = int((y1 + y2) / 2)                p1 = (x1 + x2) / 2  
                p2 = (y1 + y2) / 2  
                dett.append((p1, p2))  
    return np.array(dett)
```

这部分代码将输入的图片继续处理，更改了色彩空间、通道、维度、范围，然后调用预训练模型处理图片，再使用 `NMS（非极大值抑制）` 处理，最后将图片中每一个检测结果的中心点添加到 `dett` 列表中。

## 2. 聚类计算

```python
if len(datas) >= 2:  
    # 计算数据点之间的欧几里得距离矩阵。  
    dists = getDistanceMatrix(datas)  
    # 计算dc  
    dc = select_dc(dists)  
    # 计算局部密度  
    rho = get_density(dists, dc, method="Gaussion")  
    # 计算密度距离  
    deltas, nearest_neiber = get_deltas(dists, rho)  
    # 获取聚类中心点  
    centers = find_centers_K(rho, deltas, 3)  
  
    labs = cluster_PD(rho, centers, nearest_neiber)  
    plt.cla()  
    K = np.shape(centers)[0]
```

这部分代码还没有完全读懂，具体的实现代码是有的，但是还在读逻辑，需要结合资料看。

而且需要去掉一部分的聚类分析，变为单纯识别人数的逻辑。

## 3. 画出目标并返回显示

```python
max_num = -1  
        for k in range(K):  
            sub_index = np.where(labs == k)  
            sub_datas = datas[sub_index]  
            max_num = max(max_num, len(sub_datas))  
            # 画数据点  
            for index, i in enumerate(sub_datas):  
                p1 = int(i[0])  
                p2 = int(i[1])  
                image = cv2.circle(image, (p1, p2), radius=3,  
                                   color=dic_colors[k],  
                                   thickness=6)  
        # 设置警报人数  
        if max_num > 10:  
            print(f"Warning, there are about {max_num} people!")  
        image = cv2.putText(image, 'num=' + str(max_num), (16, 16), cv2.FONT_HERSHEY_SIMPLEX, 0.5, (0, 0, 255),  
                        2)  
    cv2.imshow('Counting Person', image)  
    key = cv2.waitKey(1)  
    if key == ord('q'):  
        break  
  
capture.release()  
cv2.destroyAllWindows()
```

这部分较为简单，打算加入超参数部分，能够设置报警阈值等等。