## ChatGLM2-6B Windows中配置方式

### 1.工程文件准备

```git clone https://github.com/THUDM/ChatGLM2-6B```

```
    需要修改.py文件中`THUDM/chatglm2-6b`为`..\\\model`，此为windows环境下表示目录层级的双反斜杠，而非Linux下的单一斜杠

### 2.python环境

    用conda创建环境，使用pip安装所有依赖的源

```conda
conda create -n chatglm
```

    然后使用pip安装所有依赖

```conda create -n chatglm```然后使用pip安装所有依赖

### 3.cuda和pytorch的安装

    以cuda11.3版本  
