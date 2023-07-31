## 0. 基本环境

CPU: AMD Ryzen 7 5800H
GPU: Nvidia GeForce RTX 3060 Laptop 6G
RAM: DDR4 3200 64G
OS: Win10 22H2
## 1. 工程文件准备

```cmd
git clone https://github.com/THUDM/ChatGLM2-6B
```

需要修改部分.py文件中（如`cli_demo.py web_demo.py api.py`等）的模型路径`THUDM/chatglm2-6b`为`..\\model`，此为windows环境下表示目录层级的双反斜杠，而非Linux下的单一斜杠`/`。

##  2.python环境

用conda创建环境，安装所有依赖的源

```conda
conda create -n chatglm python==3.8.2
conda activate chatglm
```

然后安装所有依赖

```conda
pip install -r requirements.txt
```

此时如果直接运行`python web_demo.py`会报错，必须先安装cuda和pytorch

## 3. cuda和pytorch的安装

以`torch-1.11.0`和`cuda-11.3`版本为例。

首先卸载本机上已有的更高版本的`cuda`，然后在[CUDA Toolkit 11.3 Downloads | NVIDIA Developer](https://developer.nvidia.com/cuda-11.3.0-download-archive)下载`Windows-x86_64-10-exe(local)/exe(network)`，并安装。

在[Previous PyTorch Versions | PyTorch](https://pytorch.org/get-started/previous-versions/)找到`pytorch v1.11.0`版本且对应`cuda v11.3`版本的命令，即

```conda
conda install pytorch==1.11.0 torchvision==0.12.0 torchaudio==0.11.0 cudatoolkit=11.3 -c pytorch
```

等待处理完毕即可。此时再运行`python web_demo.py`，应该会先下载模型到`.\model`文件夹，下载完毕后自动加载，即可使用。