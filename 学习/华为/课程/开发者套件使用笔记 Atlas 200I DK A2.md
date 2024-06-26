# 官方说明文档

**[说明文档-Atlas 200I DK A2开发者套件-文档首页-昇腾社区](https://www.hiascend.com/document/detail/zh/Atlas200IDKA2DeveloperKit/23.0.RC1/lg/lg_001.html)**

# Atlals 200I DK A2的主要规格和亮点

- 核心模组和扩展底盘组成
- 千兆网口、USB、HDMI、M.2、CSI、DSI、40Pin、USB3.0、TYPE-C等
- Soc集成CPU、GPU、4G内存
- 可运行Ubuntu、OpenEuler等
- 算力 8TOPS INT8

# 安装

1. 用TF卡，使用一键制卡工具完成一键制卡
2. 把TF卡插入套件，注意拨码开关如图![拨码开关图](https://www.hiascend.com/doc_center/source/zh/Atlas200IDKA2DeveloperKit/23.0.RC1/qs/figure/zh-cn_image_0000001647523913.png)
3. 使用网络登录，配置网络，即可SSH登录


# Atlas 200I DK A2的基本使用

 ## 使用串口方式连接开发板

1. 查看端口号
2. 打开IPOP，设置串口号，波特率为115200，然后连接

## 修改开发板默认IP

```bash
# cd /etc/netplan
# vi 01[tab]
```

编辑eth1的address（默认为`192.168.137.100` ）为 `192.168.137.xx` （不同于eth0），保存后退出

```bash
# netplan apply #使生效
```

回到PC打开命令行，检查能否连接

```cmd
ping 192.168.137.xx
```

## 共享PC的外网给开发板

1. 更改适配器设置
2. 选择连接外部网络的网络属性，勾选`允许其他网络用户通过此计算机的Internet连接来连接`
3. 以修改后的IP登录开发板
4. 以 `curl www.baidu.com` 测试联网是否成功
5. ==注意==，共享后 PC 的 IP 可能发生变化，如 PC 的 IP 从 192.168.137.101 变成了 192.168.137.1，那么需要将 开发板上的 /etc/netplan/01-netcfg.yaml 的 eth1 改为如图：![[atlas_200i_dk_a2_netcfg.jpg]]

## 路由器给开发板分配动态IP

1. 将开发板网口连接到路由器
2. 登录路由器管理页面
3. LAN口设置为自动
4. 打开DHCP服务，设置地址池的开始地址和结束地址

## 开发板接入USB摄像头

1. 登入开发板
2. `# lsusb` 查看是否已连接到摄像头
3. `# v4l2-ctl --all` 查看摄像头信息
	- 自动检测USB摄像头接入并创建设备节点"/dev/video0"
	- 可以通过 `sudo v4l2-ctl -d /dev/video0 --all` 来确认USB摄像头工作情况，若正常会回显帧率、分辨率等信息
4. 启动一个样例，测试摄像头是否可用
5. 运行jupyter中的infer_vdeo.ipynb，移动摄像头进行判断

## 开发板接入U盘

1. `# lsusb` 看到U盘在系统中生成的挂载点
2. `# fdisk -l` 查看容量等信息

## 两种登录方式

1. 开发板接口默认IP

![IP地址](https://www.hiascend.com/doc_center/source/zh/Atlas200IDKA2DeveloperKit/23.0.RC1/qs/figure/zh-cn_image_0000001623522381.png)

2. 本机显示模式

&emsp;&emsp;&emsp;用键鼠链接USB口，显示器链接HDMI口，接电源。

3. 远程登录模式

&emsp;&emsp;&emsp;用Type-C(套件)转RJ45(电脑)，或双RJ45连接电脑。==电脑端一定是RJ45连接==


# 配置Atlas 200I DK A2跑通第一个案例

1. TF卡连接到PC，下载安装制卡工具并将镜像烧录到TF卡上
2. 用RJ45网线连接电脑和开发板，给开发板通电
3. 开发板的网口地址为192.168.137.100，需要设置PC和开发板到同一网段，如192.168.137.1，子网掩码255.255.255.0。尝试ping 192.168.137.100
4. 使用SSH工具远程登录，账号root，密码Mind@123
5. 运行案例：
	1. \#cd /home/HwHiAiUser/sample/notebooks/
	2. \#./start_notebook.sh
	3. 进入提供的网页，打开resnet50脚本
	4. 多次点击`Run`
	5. 显示推理结果图像即说明运行正常
6. 模型适配工具：
	1. 预置的典型模型：
		- YOLO V7：目标检测模型
		- Mobilenet：图像分类场景
		- Unet++：图像分割场景
		- Alphapose：关键点检测
	2. UI操作界面，可上传数据集，支持标注
	3. 可以使用PC的CPU算力进行训练
	4. 可以对训练完成的模型进行打包
7. 模型适配工具的安装：
	1. 下载安装anaconda（添加到环境变量）
	2. 配置一个conda环境
		1. 通过文档中的链接下载环境包，解压到`...\Anaconda3\envs`中
		2. 查看是否配置成功`conda info -e`
	3. 通过文档中的链接下载模型适配工具，运行
8. 以图像分类模型为例子，使用模型适配工具
	1. 准备好数据集，注意格式(png, jpg, jpeg, bmp)、分辨率
	2. 选择制作数据集，进行标签分类、图像标注
	3. 标记完成所有图片，点击一键迁移，配置后开始训练
	4. 将打包好的模型压缩文件（.tar）上传到开发板，然后解压
	5. 进入解压的目录，运行模型转换脚本 `bash atc.sh` 
	6. 转换完成后进行推理 `bash run.sh` 